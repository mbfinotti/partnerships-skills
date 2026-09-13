# Alert Redesign — Affiliate Program

## Why the current one fails

One static floor ($10,000/day) blasted to the whole team, no owner, no channel discipline, no response SLA. It's the exact failure mode this space calls out: a fixed dollar threshold ignores your seasonal curve, so it fires all through your trough (January) and sleeps through your peak (Q4) — training everyone to filter it out. It also conflates five unrelated root causes (a tracking outage, a reversal spike, a partner going walkabout, genuine seasonal demand, brand-bid cannibalization) into one undifferentiated number, so even when it does fire, nobody knows what to do with it.

Fix: retire the single floor. Replace it with a small register of cause-specific alerts, each on a rolling baseline (not an absolute number), each with one owner, one channel, one SLA.

## Redesigned alert register

Ranked by value for a B2C program of your shape (1,200 affiliates, some PPC spend — that last fact promotes the brand-bidding flag straight to #2, ahead of where it'd sit by build-cost alone):

| #   | Alert                                     | Trigger (starting number — rebaseline from your own history)                                                                                                                                                                                         | Owner                                                     | Channel                      | Response                                                                                                                                       |
| --- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Reversal-rate spike**                   | Reversal rate (returns+chargebacks / total conversions, validation-date basis) > 2 SD above its trailing 30-day mean, 2 consecutive days. Hard ceiling until you have enough history: 10%.                                                           | Affiliate manager                                         | Ops chat channel             | Same day                                                                                                                                       |
| 2   | **Brand-bidding / trademark flag**        | Any PPC partner bids on your brand terms (exact/phrase match + close variants), detected via SERP/brand-auction monitoring — binary event, not a rate. If any PPC partner spend on brand terms is contractually barred, threshold is zero-tolerance. | Affiliate manager + paid-search lead (joint)              | Email (needs a paper trail)  | 48h — investigate, then hand to the fraud/compliance rule set if confirmed                                                                     |
| 3   | **Single-partner (or top-5) share spike** | One partner's share of rolling-7-day validated revenue jumps +10pp in 7 days, OR top-5-partner share of trailing-30-day revenue crosses 50%.                                                                                                         | Program owner                                             | Ops chat channel             | 24h to assess (growth vs. fraud vs. dependency risk — never throttle on sight)                                                                 |
| 4   | **Click-to-conversion anomaly**           | Program-level click-to-conversion deviates > 2 SD from its trailing 30-day mean, 2 consecutive days.                                                                                                                                                 | Affiliate manager (loop in eng if tracking is implicated) | Ops chat channel             | Same day — this is your tracking-outage tripwire; it catches "revenue looks dead" for a plumbing reason before the revenue number itself moves |
| 5   | **EPC drop**                              | Program-level EPC (validated commission / unique clicks) down > 2 SD vs. trailing 30-day mean.                                                                                                                                                       | Affiliate manager                                         | Weekly digest, not real-time | Reviewed at the next weekly ops review — diagnostic only, first thing to cut if attention runs out                                             |

Ship 1–3 immediately; 4 and 5 are worth adding but tie on cost and are the first to drop if the team's bandwidth for a new alert strip is thin.

## What happens to "daily revenue"

Total revenue doesn't disappear — it stops being an alert and becomes a **KPI tile**: value + delta vs. same weekday, trailing 4-week average (this is what actually neutralizes your Jan/Q4 swing, since the comparison baseline moves with the season instead of sitting at a fixed dollar line).

Keep exactly one revenue-level guardrail, at monthly cadence, not daily: **net program contribution down 2 consecutive months vs. a seasonally-adjusted baseline → program owner, monthly business review.** A whole-team email was never the right channel for a business-health signal anyway — a monthly review with a named owner is.

## Why this actually gets read

- No more all-team blast — each alert has exactly one accountable owner and a scoped channel.
- Dynamic baselines instead of an absolute number: the trigger rides your seasonal curve instead of fighting it.
- Each alert answers a different question, so when one fires, the recipient already knows which problem it is — no more one alarm meaning five different things.

## Open items — confirm before locking exact numbers

- **Reversal/EPC/click-to-conversion bands above are starting points, not derived ones.** You need 2–3 months of your own daily history to compute real 30-day rolling means and SDs; the 10% reversal ceiling and the ±2 SD rule are calibration scaffolding until then, per the rule that vendor/generic numbers never become the program's actual baseline.
- **Brand-bidding flag needs a build decision.** It requires standing SERP/brand-term monitoring or a licensed tool — you don't get it for free from your affiliate platform export. Confirm whether that tooling exists or needs procuring; until then this alert can't actually fire, only be designed.
- **Validation window length** (how long before a conversion is "final") isn't stated — the reversal-rate alert is only meaningful on the validation-date basis, so this needs to be fixed before the alert goes live.
- **Contract language on brand bidding** — confirm whether your PPC affiliate terms explicitly prohibit brand-term bidding. That determines whether alert #2 is zero-tolerance or a spend-cap threshold.
- **Top-5 concentration baseline** — the 50% figure is an industry-derived review trigger, not your number. Compute your actual top-5/top-10% share now so alert #3's second leg starts from your real distribution, not a borrowed one.
