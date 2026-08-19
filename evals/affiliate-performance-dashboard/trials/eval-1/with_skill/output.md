Two things before the spec: no canonical affiliate-dashboard framework exists (this borrows from incrementality testing, the ROAS/ROI split, sourced-vs-influenced convention, and Lean Analytics' good-metric criteria — not a branded methodology), and I answered the skill's interview from what you gave me rather than asking it turn-by-turn, since you asked for the finished deliverable. Every gap I had to guess at is called out in Open Items at the end, not silently assumed.

The one-line diagnosis: your CFO's question is unanswerable today because nothing on your slide is reconciled to money. Clicks, signups, EPC, and gross commissions all come from the network's own claimant numbers — none of them touch your billing system, none of them net out fees, and "gross commission" is definitionally the most expensive-looking, most favorable number your program can report. Your $95K/month commission spend at 20% implies roughly **$475K/month of partner-sourced recurring revenue is currently sitting inside its commission window** — that figure, netted against true cost, is what should be on the slide instead. Right now it isn't computed anywhere.

```
DASHBOARD SPEC — Thrivelane Affiliate Program

Header
  Program        : Thrivelane (B2B project-ops SaaS), 410 active partners,
                   20% recurring commission capped at 12 months, ~$95K/mo commission spend
  Audiences      : CFO (monthly, profitability + risk) · Program owner/you (weekly, operations)
  Source of truth: Billing system (Stripe/subscription ledger), network platform
                   reconciled to it — NOT the network dashboard alone
  Data foundation: Billing/orders spine, chosen because (a) the live decision — "is this
                   profitable" — is unanswerable without net revenue and fees, which only
                   billing has; (b) it's ~a week of reconciliation work vs. a quarter for
                   a full CRM join; (c) all four floor metrics compute off it. The CRM join
                   (new-to-file, trial-to-paid, partner type) is Phase 2 — promote it once
                   partner ID is stamped at trial/account creation (see Open Items).
  Period conventions: timezone, currency, validation window length, and clawback policy
                   — TBD, see Open Items. Do not report a headline number until these
                   are fixed; changing them later invalidates every prior period.
```

**Metrics**

| Metric | Definition (formula · window · counting method) | Tier | Source | Decision it drives | Target | Alert |
|---|---|---|---|---|---|---|
| **Net program contribution** | Attributed net billing revenue from partner-sourced accounts − (validated commission + network platform fee + agency fee, if any), monthly, validated-only | Business (floor) | Billing | Is the program profitable — the CFO's actual question | > $0, growing | 2 consecutive down months |
| **Cost of sale** | (validated commission + network fee + agency fee + bonuses) / attributed net revenue, monthly | Business (floor) | Billing | Whether commission rate/cap is sustainable | Own baseline [DERIVE] | > baseline + 5pt |
| **Top-5 / top-10% partner concentration** | Revenue from top-5 (and top-decile) active partners / total validated program revenue, quarterly | Business (floor) | Billing | Whether the program can survive losing its biggest partner | < 50% for top-5 [working threshold, VENDOR] | ≥ 50% |
| **Partner-sourced MRR** | MRR from partner-sourced accounts, billing-interval normalized, monthly | Business (floor) | Billing+CRM | What "the program" is actually worth before any cost is subtracted | Growth trend | −10% MoM |
| **Reversal / churn rate on referred accounts** | (referred accounts churned or downgraded within their 12-mo commission window) / total referred accounts on validation basis, monthly | Health | Billing | Whether a period's numbers are even comparable; whether to hold a partner's payout | Own band [DERIVE] | > baseline + significant jump |
| **Active-partner rate** | Partners with ≥1 validated referred conversion in a fixed window / 410 enrolled, monthly | Health | Network+Billing | Recruit more partners vs. activate the ones signed | Own band [DERIVE] | < baseline |
| **Trial-to-paid rate by partner** *(pending data — see Open Items)* | Referred trials converting to paid / referred trials started, per monthly cohort | Input | Product analytics | Which partners send qualified vs. junk traffic — no other metric catches this | Own baseline [DERIVE] | −2 SD vs 6-mo mean |
| **New-to-file share** *(Phase 2 — CRM join)* | Referred accounts with no prior Thrivelane relationship / total referred accounts, monthly | Input | CRM join | Whether checkout-adjacent/low-effort partners get repriced | ≥ baseline [DERIVE] | below baseline |
| **Churn-adjusted partner LTV : payout ratio** *(promote conditionally)* | 24-month referred revenue net of churn / cumulative payout to that partner over the same window, by partner type | Health | Billing | Whether the 20%/12-month cap itself is the right architecture | ≥ 4x, own band [SYNTH calibration 4.2–9.5x] | < 3x |
| Click-to-conversion by stage, EPC | Diagnostic only — kept off the headline view, in the operator leaderboard | Input | Network | Is one partner's traffic worth its clicks | Own baseline | n/a (diagnostic) |

Never sum sourced and influenced revenue if you later add an influenced-revenue tile — report as two separate, capped numbers, sourced taking precedence. Never headline gross commission or the network's own "total commissions earned" number again.

**Views**

```
CFO VIEW (monthly)
+---------------------------------------------------------------------+
| NET CONTRIBUTION   | COST OF SALE  | TOP-5 SHARE   | PARTNER-SOURCED |
| $___  (Δ vs P-1)   | __% (Δ)       | __%           | MRR  (Δ)        |
+---------------------------------------------------------------------+
|  Net contribution trend (13 mo)     |  Revenue by partner (top 20)  |
+--------------------------------------+-------------------------------+
|  ALERTS: concentration breach? reversal trend? cap-window impact?   |
+---------------------------------------------------------------------+

OPERATOR VIEW (weekly — you)
+---------------------------------------------------------------------+
| ACTIVE-PARTNER %  | TRIAL-TO-PAID | REVERSAL %    | 1-PARTNER SHARE |
| (vs 90d)          | (cohort)      | (vs band)     |                 |
+---------------------------------------------------------------------+
|  Weekly referred trials + conversions   |  Reversals by reason      |
+------------------------------------------+----------------------------+
|  Partner leaderboard: sourced MRR | trial-to-paid | reversal% |      |
|  months-remaining-on-cap  (sortable, full 410)                      |
+---------------------------------------------------------------------+
|  ALERT STRIP: reversal spike | single-partner share spike           |
+---------------------------------------------------------------------+
```

Every tile: value + delta vs. a *stated* prior period, never a bare number.

**Dimensions** (build in this order as data allows): partner (free today) → product/plan (already in billing) → partner type (Open item — not confirmed captured) → geography (Open item, lower priority for B2B).

**Cadence**

| Cadence | Reviewed | Drives |
|---|---|---|
| Weekly | Active-partner rate, trial-to-paid cohort movement, reversal % | Activation effort, payout holds |
| Monthly | Net contribution, cost of sale, partner-sourced MRR | The CFO conversation itself |
| Quarterly | Top-5/10% concentration, churn-adjusted LTV:payout, partner-type mix (once captured) | Whether the 20%/12-month structure changes |

Realistic starting point: you currently produce this monthly by hand. Build the monthly and quarterly bands first; add the weekly band once the billing reconciliation is running on its own rather than manually.

**Alerts** (ship in this order, stop when it's too much to keep reading)

| Alert | Trigger | Owner | Channel | Response time |
|---|---|---|---|---|
| Reversal-rate spike | > 2 SD vs 30-day rolling mean | You | Email/Slack | 24h |
| Single-partner concentration spike | Top partner +10pt share in 30 days | You | Email/Slack | 24h |

Everything else in the skill's alert catalogue (click-to-conversion anomaly, EPC drop, brand-bidding flag) is deleted for now, not parked silently — see Open Items.

**Open items**

- **Validation window and clawback policy**: not stated. Fix this before any headline number is trusted — comparing periods with different validation windows produces a false trend either direction.
- **Cookie window / attribution model**: not stated; B2B SaaS commission-structure ranges (typically 60–180 days) live outside this skill — confirm against your actual program terms.
- **Partner ID reaching billing**: not confirmed. Net program contribution, cost of sale, and partner-sourced MRR all require this join; if it doesn't exist yet, this is the single highest-leverage engineering ask you can make this quarter.
- **Trial-to-paid partner tagging**: not confirmed whether product analytics carries the referring partner ID at trial start. Without it, the metric most likely to catch "high volume, low quality" partners can't be built.
- **Partner type / promotional method**: not confirmed captured per partner. Highest-value slice for repricing decisions; not free — needs standing classification maintenance — but worth building once the billing join exists.
- **What "410 active partners" means**: the network's own "active" definition (login, live placement, a conversion) may differ from this spec's active-partner definition (≥1 validated conversion in a fixed window). Reconcile before using 410 as your denominator.
- **Program age**: not stated. Churn-adjusted LTV:payout needs ~24 months of referred-account billing history net of churn; if Thrivelane's affiliate program is younger than that, this metric stays aspirational until the history exists.
- **Scale for incrementality testing**: not enough traffic/volume data given to know if a holdout test could reach significance. Start with the new-to-file screen only (once the CRM join exists); don't run a heavier test on a program too small for its arm to read.
- **PPC/brand-bidding exposure**: not mentioned whether any partners bid on your brand terms. If none do, the brand-bidding alert stays deleted; if any do, promote it immediately rather than after the first trademark complaint.
- **Standing analyst/data ownership**: not stated who would own the billing reconciliation going forward. This determines whether the weekly band is sustainable or whether monthly/quarterly is the realistic ceiling.