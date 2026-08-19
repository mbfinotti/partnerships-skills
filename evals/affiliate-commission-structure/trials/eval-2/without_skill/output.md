## The numbers

**Inputs:** $89/mo, 84% gross margin, 3.3% monthly churn → average customer lifetime ≈ 1/0.033 ≈ 30.3 months.

**Per-customer economics (expected value over full lifetime):**

| | 25% (current) | 12% (proposed) |
|---|---|---|
| Expected lifetime revenue | $2,697 | $2,697 |
| Expected lifetime gross profit (84%) | $2,266 | $2,266 |
| Total commission paid | $674 | $324 |
| Commission as % of lifetime **gross profit** | 29.7% | 14.3% |
| Net margin retained (gross margin − commission %) | 59% of revenue | 72% of revenue |
| Net contribution per customer, lifetime | $1,591 | $1,942 |

Because commission is a flat % of every payment, "% of revenue" is trivially the headline rate — the number that matters is **% of lifetime gross profit consumed**, and that's where the CFO's complaint lands: at 25%, affiliates are eating **~30% of the gross profit** a customer ever generates, before you've paid for support, hosting, sales, anything else. That's roughly double what's normal for a single acquisition channel (healthy SaaS targets keep *total* blended CAC around 30–35% of gross-profit LTV — 25% recurring-for-life on affiliates alone already burns nearly that entire budget).

**Why it "feels" worse than it looks month to month:** this isn't a one-time bounty, it's a standing liability that compounds with scale. At steady state, your monthly affiliate commission bill converges to `rate × (average lifetime in months) × (new affiliate-sourced MRR that month)` — with a 30-month average lifetime, every $1 of new affiliate MRR eventually carries ~30 months of commission liability behind it. At 25% that's a much heavier permanent drag on cash than it looks like from any single cohort.

## Does 12% actually fix it, or is it cosmetic?

It's a real fix, not just a headline number. Cutting 25%→12% is a **52% reduction** in the ongoing revenue share, and it moves the "% of lifetime gross profit given away" from ~30% down to ~14% — solidly in the sustainable range for one channel. Net contribution margin per customer goes from 59%→72% of revenue, or +$351 in extra profit per affiliate-sourced customer over its life.

## Does "keep it lifetime" undercut that, or is the recruiting story still real?

No — duration doesn't change the cost math (cost is always `rate × revenue collected`, regardless of how long it runs), so keeping "lifetime" instead of capping to 12/24 months costs the company nothing extra versus a capped structure at the same rate. And the recruiting pitch holds up better than it might seem: a typical competitor offering, say, 30% capped at 12 months, pays out an *expected* ~$268 per referred customer (accounting for churn during that window) — less than the **$324 expected** under 12%-for-life. So "12% for life" isn't a weaker offer than a flashier-looking capped rate; it's arguably better in real expected-earnings terms, and it's genuinely differentiated (most competitors cap duration).

## Recommendation

**Go to 12%, keep it lifetime.** It cuts the affiliate cost from an unsustainable ~30% of lifetime gross profit to a normal ~14%, it doesn't cost anything extra to keep the lifetime framing, and the lifetime structure still out-earns many higher-headline, capped-duration competitor programs in expectation.

Two things worth deciding alongside this, not covered by the math above:
1. **Existing affiliates on the 25% deal** — grandfather them or reprice retroactively? That's a relationship/legal call, not a numbers one.
2. **Perception risk** — affiliates anchor on the headline number, not lifetime EV. Pair the cut with an "average customer stays 30 months" earnings illustration so the pitch doesn't just read as "we cut your rate in half."