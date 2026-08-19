## Redesigned alerting for the affiliate program

**Root cause of today's problem:** one static absolute threshold ($10k/day revenue) against a metric that has strong seasonality. It's not an alerting bug, it's a baseline bug — fix the baseline, not the number.

### 1. Kill the single alert, split into 4 alert types

| # | What it catches | Who owns it | Channel |
|---|---|---|---|
| 1 | Tracking/pixel outage | Engineering on-call | Page, 24/7 |
| 2 | Program-wide revenue anomaly | Affiliate ops lead | Slack (warning) / Page (critical) |
| 3 | Single-affiliate anomaly (top earners) | Affiliate manager for that account | Slack, business hours |
| 4 | PPC-partner risk (spend, fraud, brand bidding) | Affiliate manager + finance | Slack/email, same-day |

Stop emailing the whole team for everything — that's *why* it gets filtered. Only #1 and a critical #2 justify waking someone up.

### 2. Alert 1 — Tracking dead (replaces nothing, this doesn't exist today and is the highest-value addition)

- Trigger: **0 clicks or 0 conversions network-wide for 60 consecutive minutes** during hours where the trailing baseline says you should have >0.
- This catches pixel/postback failures, a broken redirect, a payment webhook outage — the actual cause of most "revenue is $0" scares, independent of season.
- Page engineering immediately, 24/7. This should almost never fire in a healthy system, so no noise tolerance needed.

### 3. Alert 2 — Program-wide revenue, seasonally baselined (this replaces your $10k rule)

Stop comparing to a fixed number. Compare **today's revenue to the median of the same weekday over the trailing 6 weeks**, and check it **intraday** (cumulative-so-far vs. baseline cumulative-so-far at the same hour), not just at midnight — so you catch a bad day by 2pm, not the next morning.

- **Warning** (Slack, business hours digest): actual < **70%** of baseline for 1 day, or < 80% for 2 consecutive days.
- **Critical** (page on-call): actual < **50%** of baseline on a single day, or < 70% for 3 consecutive days running.
- Exclude your own promo calendar (Black Friday, site-wide sales, planned maintenance) from the baseline window and from firing — those are expected deviations, not anomalies. Feed known event dates into a calendar exception list.
- Require 2 consecutive breaches before firing (hysteresis) to stop single-hour noise from paging anyone, and send an explicit "resolved" notification once back above 90% of baseline for a full day — silence isn't a signal that it's fixed.

This naturally solves both halves of your current problem: in January, the baseline is January-level, so a normal soft month doesn't fire; in Q4, the baseline is Q4-level, so a real 40% drop on Black Friday finally does fire, even though $10k/day would still look "healthy" in absolute terms.

If you want a number to sanity-check the model with instead of pure percentiles: pull your last 12 months of daily revenue, compute trailing-6-week-median vs. actual for every day, and confirm the 70%/50% cuts would have fired on your known bad days (a tracking outage, a site incident) and *not* fired in a normal January. Tune from there — the percentages matter more than getting them exactly right on day one.

### 4. Alert 3 — Single-affiliate drop (new, protects the concentration risk)

With 1,200 affiliates, revenue is almost certainly Pareto-concentrated — a handful of partners likely drive 50-80% of volume, and a program-wide baseline will never move enough to flag one of them going dark.

- Track your **top 20 affiliates by trailing-30-day revenue** individually.
- Fire if any of them drops **>50% day-over-day vs. their own trailing 7-day average**, or goes to **literal zero for >24h**.
- Route to the affiliate manager who owns that relationship, not the whole team — it's almost always a dead link, an expired coupon, or their site being down, and it's a relationship fix, not an incident.

### 5. Alert 4 — PPC partner risk (new, specific to "a handful of PPC partners")

PPC affiliates carry different failure modes than content/loyalty affiliates: margin cannibalization, brand bidding, and click fraud — none of which a revenue-drop alert would ever catch (they often show as revenue going *up*).

- **Margin cap:** commission cost ÷ order value for any PPC partner exceeds the contracted cap (e.g., set at whatever your negotiated max is) → alert finance same day.
- **Click/conversion divergence:** a PPC partner's click volume up **>200% day-over-day** without a matching lift in conversions → likely bot traffic or click fraud → alert + auto-pause pending review.
- **Brand bidding:** any PPC partner's landing page or ad copy referencing your trademarked terms → immediate compliance alert; this is usually a contract violation, treat separately from performance alerts.
- **Conversion-rate collapse:** a PPC partner's conversion rate drops below **50% of their own trailing baseline** → likely ad disapproval or landing page break, not a demand problem — worth a fast nudge before you lose a week of their spend.

### 6. Cadence

- Real-time: Alert 1 (tracking), Alert 2 critical, Alert 4 fraud/brand-bidding.
- Daily digest (Slack, morning): Alert 2 warnings, Alert 3.
- Weekly digest (email, to the team that currently gets everything): full alert history + trend, so there's still one place with visibility without it being the thing everyone filters out.