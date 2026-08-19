I looked at the repo for relevant context (steering clear of `skill-wip/` as instructed) — nothing there relates to Ferra Analytics, so this is a self-contained build. Here's the complete deliverable.

---

# Ferra Analytics — Affiliate Fraud Watch

## The one insight that makes this work

You said there's no way to add a validation delay because commissions **approve** the instant an order lands. That's fine — don't touch approval. Add a gate one step later, at **payout**.

Every affiliate program pays out on some cadence (weekly/biweekly/monthly), even a homegrown one — nobody wire-transfers commission the same second it's approved. That gap is your review window, and it costs you nothing to add:

- Add one column: `commissions.held_for_review boolean default false`.
- Your payout batch job excludes rows where `held_for_review = true`.
- The weekly scan below sets that flag on suspicious commissions before the batch runs.
- Approval stays instant, exactly as it is today. Nothing upstream changes.

This is the entire trick. Everything else below is what decides which rows get held.

---

## Fraud signals (tuned for 14 affiliates / ~$9K MRR — no ML, no vendor tool needed at this scale)

| Signal | What it catches | Weight |
|---|---|---|
| **Self-referral** | Customer email matches the affiliate's own account email | 40 |
| **New-affiliate burst** | ≥5 orders in week 1 from an affiliate <30 days old | 30 |
| **IP reuse across "unique" customers** | Same affiliate, same customer IP, ≥3 distinct emails in 30 days | 25 |
| **Refund/chargeback rate spike** | Affiliate's 30-day refund rate >2x site average (min 5 orders) | 25 |
| **Repeat-customer abuse** | Same email re-appears as a "new" commissioned order for the same affiliate within 90 days | 20 |
| **Volume spike (established affiliate)** | This week's orders >3x their trailing 4-week average | 20 |
| **Timing clustering** | ≥5 orders with near-identical spacing (stddev <5s) — scripted, not human | 15 |
| **Disposable email domain** | Customer email at mailinator/guerrillamail/etc. | 15 |
| **Value clustering** | ≥4 orders at the exact same amount from one affiliate | 10 |

Score per order = sum of triggered weights. Score per affiliate = sum over the week. **Review threshold: 30.** At 14 affiliates you should see 0–2 flagged per week — that's the point, this is built to stay inside your 2-hour budget, not to flag everything.

---

## SQL — `fraud_scan.sql`

Adjust the table/column names in the CTEs to your actual schema. Assumed minimum shape:

```
affiliates(id, name, email, status, created_at)
orders(id, affiliate_id, customer_email, customer_ip, amount_cents, status, created_at)
```

```sql
-- fraud_scan.sql — run weekly. $1 = lookback interval, e.g. '7 days'
WITH window_orders AS (
  SELECT * FROM orders WHERE created_at >= now() - $1::interval
),
disposable_domains(domain) AS (
  VALUES ('mailinator.com'), ('guerrillamail.com'), ('10minutemail.com'),
         ('tempmail.com'), ('yopmail.com'), ('trashmail.com'),
         ('sharklasers.com'), ('throwawaymail.com'), ('getnada.com'),
         ('dispostable.com')
),
self_referral AS (
  SELECT wo.id AS order_id
  FROM window_orders wo
  JOIN affiliates a ON a.id = wo.affiliate_id
  WHERE lower(wo.customer_email) = lower(a.email)
),
disposable_email AS (
  SELECT wo.id AS order_id
  FROM window_orders wo
  JOIN disposable_domains d ON lower(split_part(wo.customer_email, '@', 2)) = d.domain
),
ip_reuse AS (
  SELECT wo.id AS order_id
  FROM window_orders wo
  WHERE (
    SELECT count(DISTINCT o2.customer_email) FROM orders o2
    WHERE o2.affiliate_id = wo.affiliate_id
      AND o2.customer_ip = wo.customer_ip
      AND o2.created_at >= wo.created_at - interval '30 days'
  ) >= 3
),
repeat_customer AS (
  SELECT wo.id AS order_id
  FROM window_orders wo
  WHERE (
    SELECT count(*) FROM orders o2
    WHERE o2.affiliate_id = wo.affiliate_id
      AND o2.customer_email = wo.customer_email
      AND o2.created_at >= wo.created_at - interval '90 days'
      AND o2.status <> 'refunded'
  ) >= 2
),
affiliate_refund_rate AS (
  SELECT affiliate_id,
         avg((status IN ('refunded','chargeback'))::int) AS refund_rate,
         count(*) AS n
  FROM orders WHERE created_at >= now() - interval '30 days'
  GROUP BY affiliate_id
),
site_refund_rate AS (
  SELECT avg((status IN ('refunded','chargeback'))::int) AS refund_rate
  FROM orders WHERE created_at >= now() - interval '30 days'
),
new_affiliate_burst AS (
  SELECT o.affiliate_id, count(*) AS n
  FROM orders o JOIN affiliates a ON a.id = o.affiliate_id
  WHERE o.created_at >= now() - interval '7 days'
    AND a.created_at >= now() - interval '30 days'
  GROUP BY o.affiliate_id HAVING count(*) >= 5
),
volume_spike AS (
  SELECT affiliate_id,
         count(*) FILTER (WHERE created_at >= now() - interval '7 days') AS last_7d,
         count(*) FILTER (WHERE created_at >= now() - interval '35 days'
                             AND created_at < now() - interval '7 days') / 4.0 AS avg_prior_week
  FROM orders GROUP BY affiliate_id
),
value_clustering AS (
  SELECT affiliate_id, amount_cents, count(*) AS n
  FROM window_orders GROUP BY affiliate_id, amount_cents HAVING count(*) >= 4
),
timing_gaps AS (
  SELECT affiliate_id, id AS order_id,
         extract(epoch FROM (created_at - lag(created_at) OVER (PARTITION BY affiliate_id ORDER BY created_at))) AS gap_seconds
  FROM window_orders
),
timing_clustering AS (
  SELECT affiliate_id FROM timing_gaps
  WHERE gap_seconds IS NOT NULL
  GROUP BY affiliate_id HAVING count(*) >= 5 AND stddev(gap_seconds) < 5
)
SELECT
  wo.id AS order_id, wo.affiliate_id, a.name AS affiliate_name,
  wo.customer_email, wo.amount_cents, wo.created_at,
  (sr.order_id IS NOT NULL)  AS flag_self_referral,
  (de.order_id IS NOT NULL)  AS flag_disposable_email,
  (ir.order_id IS NOT NULL)  AS flag_ip_reuse,
  (rc.order_id IS NOT NULL)  AS flag_repeat_customer,
  (arr.refund_rate > 2 * srr.refund_rate AND arr.n >= 5) AS flag_refund_rate,
  (nab.affiliate_id IS NOT NULL) AS flag_new_affiliate_burst,
  (vs.last_7d >= 3 AND vs.avg_prior_week > 0 AND vs.last_7d > 3 * vs.avg_prior_week) AS flag_volume_spike,
  (vc.n IS NOT NULL) AS flag_value_clustering,
  (tc.affiliate_id IS NOT NULL) AS flag_timing_clustering,
  ( (sr.order_id IS NOT NULL)::int * 40
  + (nab.affiliate_id IS NOT NULL)::int * 30
  + (ir.order_id IS NOT NULL)::int * 25
  + (arr.refund_rate > 2 * srr.refund_rate AND arr.n >= 5)::int * 25
  + (rc.order_id IS NOT NULL)::int * 20
  + (vs.last_7d >= 3 AND vs.avg_prior_week > 0 AND vs.last_7d > 3 * vs.avg_prior_week)::int * 20
  + (tc.affiliate_id IS NOT NULL)::int * 15
  + (de.order_id IS NOT NULL)::int * 15
  + (vc.n IS NOT NULL)::int * 10
  ) AS order_risk_score
FROM window_orders wo
JOIN affiliates a ON a.id = wo.affiliate_id
LEFT JOIN self_referral sr ON sr.order_id = wo.id
LEFT JOIN disposable_email de ON de.order_id = wo.id
LEFT JOIN ip_reuse ir ON ir.order_id = wo.id
LEFT JOIN repeat_customer rc ON rc.order_id = wo.id
LEFT JOIN affiliate_refund_rate arr ON arr.affiliate_id = wo.affiliate_id
CROSS JOIN site_refund_rate srr
LEFT JOIN new_affiliate_burst nab ON nab.affiliate_id = wo.affiliate_id
LEFT JOIN volume_spike vs ON vs.affiliate_id = wo.affiliate_id
LEFT JOIN value_clustering vc ON vc.affiliate_id = wo.affiliate_id AND vc.amount_cents = wo.amount_cents
LEFT JOIN timing_clustering tc ON tc.affiliate_id = wo.affiliate_id
ORDER BY order_risk_score DESC, wo.created_at DESC;
```

---

## Go CLI — `main.go`

One command, run from cron every Monday. Scans, holds the flagged commissions, writes a CSV, prints a console summary.

```go
package main

import (
	_ "embed"
	"context"
	"encoding/csv"
	"flag"
	"fmt"
	"log/slog"
	"os"
	"strconv"
	"text/tabwriter"
	"time"

	"github.com/jackc/pgx/v5"
	"github.com/jackc/pgx/v5/pgxpool"
	"github.com/samber/lo"
)

//go:embed fraud_scan.sql
var fraudScanSQL string

type orderRow struct {
	OrderID          int64     `db:"order_id"`
	AffiliateID      int64     `db:"affiliate_id"`
	AffiliateName    string    `db:"affiliate_name"`
	CustomerEmail    string    `db:"customer_email"`
	AmountCents      int64     `db:"amount_cents"`
	CreatedAt        time.Time `db:"created_at"`
	FlagSelfReferral bool      `db:"flag_self_referral"`
	FlagDisposable   bool      `db:"flag_disposable_email"`
	FlagIPReuse      bool      `db:"flag_ip_reuse"`
	FlagRepeat       bool      `db:"flag_repeat_customer"`
	FlagRefundRate   bool      `db:"flag_refund_rate"`
	FlagNewBurst     bool      `db:"flag_new_affiliate_burst"`
	FlagVolumeSpike  bool      `db:"flag_volume_spike"`
	FlagValueCluster bool      `db:"flag_value_clustering"`
	FlagTiming       bool      `db:"flag_timing_clustering"`
	OrderRiskScore   int       `db:"order_risk_score"`
}

func main() {
	dsn := flag.String("dsn", os.Getenv("FERRA_DB_DSN"), "postgres connection string")
	since := flag.Duration("since", 7*24*time.Hour, "lookback window")
	threshold := flag.Int("threshold", 30, "affiliate weekly score that triggers a hold")
	out := flag.String("out", fmt.Sprintf("fraud-report-%s.csv", time.Now().Format("2006-01-02")), "CSV output path")
	dryRun := flag.Bool("dry-run", false, "scan and report only, do not set held_for_review")
	flag.Parse()

	log := slog.New(slog.NewJSONHandler(os.Stdout, nil))
	ctx := context.Background()

	pool, err := pgxpool.New(ctx, *dsn)
	if err != nil {
		log.Error("connect failed", "err", err)
		os.Exit(1)
	}
	defer pool.Close()

	rows, err := pool.Query(ctx, fraudScanSQL, *since)
	if err != nil {
		log.Error("scan query failed", "err", err)
		os.Exit(1)
	}
	orders, err := pgx.CollectRows(rows, pgx.RowToStructByName[orderRow])
	if err != nil {
		log.Error("row scan failed", "err", err)
		os.Exit(1)
	}

	byAffiliate := lo.GroupBy(orders, func(o orderRow) int64 { return o.AffiliateID })
	type affiliateSummary struct {
		Name         string
		FlaggedCount int
		TotalScore   int
	}
	summaries := make(map[int64]affiliateSummary, len(byAffiliate))
	for affID, os_ := range byAffiliate {
		name := os_[0].AffiliateName
		total := lo.SumBy(os_, func(o orderRow) int { return o.OrderRiskScore })
		flagged := lo.CountBy(os_, func(o orderRow) bool { return o.OrderRiskScore > 0 })
		summaries[affID] = affiliateSummary{Name: name, FlaggedCount: flagged, TotalScore: total}
	}

	if err := writeCSV(*out, orders); err != nil {
		log.Error("csv write failed", "err", err)
		os.Exit(1)
	}

	tw := tabwriter.NewWriter(os.Stdout, 0, 2, 2, ' ', 0)
	fmt.Fprintln(tw, "AFFILIATE\tFLAGGED ORDERS\tWEEKLY SCORE\tACTION")
	held := 0
	for affID, s := range summaries {
		if s.TotalScore < *threshold {
			continue
		}
		action := "review"
		if !*dryRun {
			n, err := holdCommissions(ctx, pool, affID, *since)
			if err != nil {
				log.Error("hold failed", "affiliate_id", affID, "err", err)
			} else {
				held += n
				action = fmt.Sprintf("held %d commission(s)", n)
			}
		}
		fmt.Fprintf(tw, "%s\t%d\t%d\t%s\n", s.Name, s.FlaggedCount, s.TotalScore, action)
	}
	tw.Flush()

	log.Info("fraud scan complete",
		"orders_scanned", len(orders),
		"affiliates_flagged", lo.CountBy(lo.Values(summaries), func(s affiliateSummary) bool { return s.TotalScore >= *threshold }),
		"commissions_held", held,
		"csv", *out,
	)
}

func holdCommissions(ctx context.Context, pool *pgxpool.Pool, affiliateID int64, since time.Duration) (int, error) {
	tag, err := pool.Exec(ctx, `
		UPDATE commissions
		SET held_for_review = true
		WHERE affiliate_id = $1
		  AND created_at >= now() - $2::interval
		  AND paid_at IS NULL`,
		affiliateID, since)
	if err != nil {
		return 0, err
	}
	return int(tag.RowsAffected()), nil
}

func writeCSV(path string, orders []orderRow) error {
	f, err := os.Create(path)
	if err != nil {
		return err
	}
	defer f.Close()

	w := csv.NewWriter(f)
	defer w.Flush()

	w.Write([]string{
		"order_id", "affiliate_id", "affiliate_name", "customer_email", "amount_cents",
		"created_at", "self_referral", "disposable_email", "ip_reuse", "repeat_customer",
		"refund_rate", "new_affiliate_burst", "volume_spike", "value_clustering",
		"timing_clustering", "risk_score",
	})
	for _, o := range orders {
		if o.OrderRiskScore == 0 {
			continue
		}
		w.Write([]string{
			strconv.FormatInt(o.OrderID, 10), strconv.FormatInt(o.AffiliateID, 10), o.AffiliateName,
			o.CustomerEmail, strconv.FormatInt(o.AmountCents, 10), o.CreatedAt.Format(time.RFC3339),
			strconv.FormatBool(o.FlagSelfReferral), strconv.FormatBool(o.FlagDisposable),
			strconv.FormatBool(o.FlagIPReuse), strconv.FormatBool(o.FlagRepeat),
			strconv.FormatBool(o.FlagRefundRate), strconv.FormatBool(o.FlagNewBurst),
			strconv.FormatBool(o.FlagVolumeSpike), strconv.FormatBool(o.FlagValueCluster),
			strconv.FormatBool(o.FlagTiming), strconv.Itoa(o.OrderRiskScore),
		})
	}
	return nil
}
```

`go.mod` requires: `github.com/jackc/pgx/v5` and `github.com/samber/lo`. Keep `fraud_scan.sql` next to `main.go` (it's `go:embed`ded).

Run it: `FERRA_DB_DSN=postgres://... go run . -threshold 30` — add `-dry-run` the first few weeks until you trust the thresholds, then drop it so holds apply automatically.

One schema change needed beyond the trick above: `ALTER TABLE commissions ADD COLUMN held_for_review boolean NOT NULL DEFAULT false;` and your payout batch adds `AND held_for_review = false` to whatever query selects what to pay.

---

## Your weekly 2 hours

1. **Monday, 5 min** — cron already ran the scan overnight; open the console log and CSV.
2. **10–30 min** — for each affiliate at/above threshold (expect 0–2 of your 14), spot-check 3–5 flagged rows in the CSV: does the email/IP pattern actually look fake, or is it a coincidence (shared office, one big customer)?
3. **Action ladder** (don't skip straight to termination — most weeks it's a false positive):
   - **First flag, score 30–59**: leave the hold in place, no accusation, quietly wait one more payout cycle. Most resolve themselves as noise.
   - **Score 60+, or flagged two weeks running**: hold everything pending, message the affiliate asking about the pattern you see, review their full history.
   - **Confirmed** (self-referral proven, obviously fake emails): terminate, void held commissions, claw back anything already paid per your affiliate agreement.
4. **5 min** — log affiliate / week / score / action in a plain spreadsheet. This is what lets you tune thresholds later and what backs you up if an affiliate disputes a clawback.

That's the full budget. The script does the counting; you only ever look at a short, pre-filtered list.

---

## Two things outside the code, worth doing once

- **Affiliate agreement**: add a line reserving the right to withhold or claw back commissions under fraud review, and to terminate without owing pending balances. Without this, the `held_for_review` flag has no legal teeth if someone pushes back.
- **Don't buy a fraud SaaS at this scale.** Vendor affiliate-fraud tools (Everflow, Affise add-ons, Anura, etc.) are priced for programs doing 10–100x your volume. At $9K/month in commissions, this script is proportionate; a $500+/month tool wouldn't be.