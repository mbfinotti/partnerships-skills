# Formwork Analytics — Affiliate Commission Ladder

## The conflict this request sits on top of

Two rules this skill applies collide here, and you should see both before locking anything:

- **Tiers on zero data**: with no affiliates and no live program, there is no performance distribution to place a breakpoint against. The default is to launch flat and add tiers once 1-2 quarters of real data exist.
- **Your stated reason (recruiting pitch)** is a legitimate override, not a mistake — a ladder gives recruiting copy a target a flat rate can't. Overriding the default is fine; what's not fine is dressing up invented breakpoints as if they came from performance data they can't yet reflect.

So the ladder below is real and usable, but its breakpoints are **volume targets, not earned percentiles** — labeled that way in the spec, with a recalibration date already on the calendar. That's the honest version of what you asked for.

**Second gap: no unit economics were given.** No plan price, margin, churn, LTV, or CAC for Formwork Analytics. Without them I can't derive a real ceiling — I can only show you the ceiling math with placeholder inputs so you can drop your real numbers into the same formulas in under a minute. Treat every dollar figure below as a placeholder until you swap in your own. I need these four numbers to lock the final spec:

1. Entry-plan price (monthly)
2. Gross margin %
3. Monthly churn % (or average customer tenure)
4. Current blended CAC

## The three rates and breakpoints (headline answer)

Marginal tiers (each rate applies only to net-new customers _above_ the threshold that quarter — not retroactive to the whole period, which avoids the cliff-gaming a retroactive ladder invites on a brand-new, unvetted partner base):

| Tier      | Net-new paying customers / quarter | Recurring rate | 12-month cap, per customer* |
| --------- | ---------------------------------- | -------------- | --------------------------- |
| 🥉 Bronze | 1–3                                | 20%            | $597.60                     |
| 🥈 Silver | 4–8                                | 25%            | $747.00                     |
| 🥇 Gold   | 9+                                 | 30%            | $896.40                     |

*computed on a placeholder $249/mo entry plan — replace with your real entry price and re-run: `rate × plan price × 12`.

Why these three numbers, not others:

- 20/25/30% sits inside the B2B SaaS convergent range (20-30% recurring baseline; "20%, 25%, and 30% the best-performing offer ranges" per PartnerStack network data), and 30% for a niche vertical tool is consistent with the higher end reserved for ERP-type/vertical products.
- At a placeholder $249/mo × 40-month tenure ($9,960 revenue LTV, 78% margin), even the Gold cap lands at 9.0% of LTV — inside the 5-15% band with room to spare, so the headline can absorb your real numbers coming in higher or lower without blowing the ceiling.
- Quarterly measurement window (not monthly) — smooths a brand-new program's inevitable lumpy first quarters and needs only one reset cadence to administer.

**Breakpoint honesty label**: 1-3 / 4-8 / 9+ are targets, not "70-80% of affiliates already clear tier 1" — that claim requires affiliate history you don't have yet. Recalibrate against real distribution after 2 full quarters live, per the tier design default.

## Full Commission Structure Spec

```
COMMISSION STRUCTURE - Formwork Analytics, 2026-09-12
Rate model        : recurring revenue share, marginal tiers - B2B SaaS, subscription product
Headline rates    : Bronze 20% / Silver 25% / Gold 30% recurring, all capped 12 months
                    - marginal, not retroactive: rate applies only to customers above
                      that quarter's threshold, protects against cliff-gaming on an
                      unvetted new partner base
Tiers             : Bronze 1-3 net-new customers/quarter, Silver 4-8, Gold 9+
                    - PROVISIONAL: set from volume targets, not performance history
                      (none exists pre-launch) - recalibrate after 2 full quarters live
                      to the 70-80%-reach-tier-1 / 10-20%-reach-top-tier rule
                    - measurement window: quarterly, resets each quarter
                    - threshold metric: net-new paying customers now (no revenue
                      attribution live yet); migrate to net-new customer revenue
                      once tracking supports it - do not let count-based
                      thresholds become permanent
Recurring duration: capped at 12 months from day one - do not open with lifetime;
                    revisit a taper or renewal bonus once churn data exists
Attribution       : 90-day cookie (placeholder - B2B SaaS default band is 60-180 days;
                    tighten or widen to your actual sales-cycle length)
                    - gate to new customers if/when coupon/cashback partners join;
                    content and review partners get the standard window
Validation        : 45-day lock (placeholder = trial-to-paid window + 30-day refund
                    window - replace with your real trial length)
Payment           : net-30, $50 minimum threshold; clawback on refund/chargeback/
                    in-window cancellation, negative balance carried forward
Economics         : PLACEHOLDER INPUTS - $249/mo entry plan, 78% gross margin,
                    40-month avg tenure ($9,960 revenue LTV)
                    Gold ceiling = 30% x $249 x 12 = $896.40/customer
                    = 9.0% of LTV (inside 5-15% band), well inside 30-40% margin cap
                    projected cost per incremental customer (+15% platform fee,
                    80% assumed incrementality) ≈ $1,289 - BORDERLINE against a
                    placeholder $1,200 CAC. Cannot confirm PASS without your real
                    blended CAC - this is the one number most likely to move the
                    headline rate once you supply it.
Validation plan   : 30-day holdout on any coupon/cashback partners before granting
                    standard rates, once such partners exist; track new-customer
                    share from month 1 even pre-tier-recalibration
KPIs              : cost per incremental affiliate customer vs blended CAC,
                    effective commission rate, new-customer share, reversal/
                    clawback rate, revenue share of top 10% partners
```

## What to do before this goes live in 6 weeks

1. Send the four missing numbers (plan price, margin, churn, CAC) — I'll re-run the ceiling math and the rates likely shift.
2. Confirm your attribution tooling can actually count "net-new paying customers per quarter" per partner from day one — the whole ladder depends on that being trackable at launch, not aspirational.
3. Put the 2-quarter tier recalibration date on a calendar now, before recruiting starts, so it's a planned adjustment rather than a rate cut that needs 60 days' notice and grandfathering later.
