This is a business/finance analysis task, not a coding task — I'm answering directly, without touching skill-wip/ or anything else in the repo.

# What your affiliate dashboard should actually measure

Clicks, signups, EPC and total commissions tell you the program is _active_. They don't tell you whether it's _profitable_, because none of them touch retention, margin, or fraud. Here's what to replace them with.

## 1. The one number the CFO actually wants: Partner Program ROI

```
ROI = (Gross margin from affiliate-sourced customers − Total commissions paid) / Total commissions paid
```

Not "commissions vs. revenue" — commissions vs. **gross margin**, and only counting margin actually collected, not booked at signup. At 20% recurring commission capped at 12 months, a customer needs to stay far past month 12 to be profitable, so this metric is meaningless without a cohort/LTV view (below). Report it monthly, but computed on a **rolling 12-month cohort basis**, not on the current month's cash commission payout — otherwise you're comparing this month's costs to last year's customers' revenue and the number is noise.

## 2. Cohort LTV:CAC by acquisition month, affiliate-sourced vs. all other channels

This is the core of the deck. For each signup cohort (grouped by month they converted through an affiliate):

- Track cumulative gross margin at month 3, 6, 12, 18, 24
- Track cumulative commission paid to the referring partner for that cohort
- Plot LTV:CAC ratio over cohort age, affiliate-sourced line vs. non-affiliate line

Why this matters specifically for you: the 12-month commission cap means the _cost_ of an affiliate customer is front-loaded and finite, while the _value_ compounds indefinitely after month 12. If churn is concentrated in months 1–12 (i.e., people leave right around when their referrer stops getting paid — a real risk with recurring-commission structures if partners aren't incentivized on retention), affiliate LTV can look fine in aggregate while actually being worse than organic. You cannot see this in "total commissions earned." You can only see it cohort-by-cohort.

## 3. Retention/churn of affiliate-sourced customers vs. all other channels, side by side

- Gross revenue churn and logo churn, affiliate vs. direct/other channels, same time window
- Net revenue retention (NRR) by channel
- If affiliate-sourced churn is meaningfully worse than direct, you're paying 20% recurring commission to acquire customers who are _more_ likely to leave before month 12 — that's the single most damaging pattern this program could have, and the current dashboard cannot detect it at all.

## 4. Contribution margin per partner, not per program

Aggregate numbers hide a power-law distribution that almost certainly exists in a 410-partner program. Break out:

- Revenue and margin contributed per partner (not just clicks/signups per partner)
- % of total commission paid to top 10 / top 20 partners, and their margin contribution in return
- A per-partner "payback flag": partners whose referred customers haven't reached breakeven margin (commission paid vs. margin earned) — this identifies specific relationships that are actively losing money, which is far more actionable than a program-wide average.

Expect (and design for) a finding like "top 40 partners drive 80% of profitable volume, bottom 200 are break-even or negative" — that's normal and it's the basis for a partner-tiering or pruning decision, not a reason to kill the program.

## 5. Fraud / quality-adjusted signups

EPC and signup counts are gameable in any recurring-commission affiliate program, especially at $95K/month in payouts flowing to 410 uncontrolled parties. Add:

- **Signup → paid conversion rate** by partner (a partner driving lots of "signups" that never convert to paying is a red flag, cost-free noise, or worse, incentivized self-referral/fraud)
- **Trial-to-paid or paid-to-still-active-at-day-90** rate by partner, to catch commission farming (fake or churned-fast signups designed solely to trigger the recurring payout before cancellation)
- Refund/chargeback rate on affiliate-sourced revenue vs. baseline
- Time-to-churn distribution for affiliate signups — a cluster of cancellations right after commission-relevant milestones is a tell

## 6. Incrementality — the honest version, admit the limitation

The hardest and most important question: are these customers _net-new_, or would a meaningful share have signed up anyway (brand search, direct, existing pipeline) and the affiliate just intercepted last-click credit? You almost certainly don't have a clean way to measure this without a holdout or geo experiment, and building one is a separate project. For the dashboard itself, the practical proxy:

- % of affiliate-attributed signups that also show organic/direct/branded-search touchpoints earlier in the journey (if your attribution stack captures multi-touch) — a high number means you're paying 20% commission for demand you'd have gotten free
- Flag this explicitly as a known blind spot to the CFO rather than pretending EPC answers it — that's more credible than presenting a number you can't defend under questioning.

## 7. Payback period

Months for an affiliate-sourced customer's cumulative gross margin to exceed the total commission paid on them. Report the distribution (median, and the % of customers who never cross breakeven before churning) — a single average payback period hides the customers who never pay back at all, which is exactly the group #3 and #5 are designed to surface.

---

## What to put on one slide for the CFO

| Metric                                          | Why it answers "does this make money"                |
| ----------------------------------------------- | ---------------------------------------------------- |
| Program ROI (margin − commission, cohort-based) | The bottom-line answer                               |
| LTV:CAC, affiliate vs. other channels           | Is this channel actually competitive                 |
| Churn/NRR, affiliate vs. other channels         | Are we buying worse customers                        |
| Margin contribution by partner decile           | Where the money actually comes from                  |
| Signup→paid conversion by partner               | Is spend going to real customers or noise            |
| Payback period distribution                     | How long capital is tied up, and who never pays back |

## Data you'll need that the network dashboard doesn't give you

Your affiliate network shows top-of-funnel (clicks, signups, EPC) because that's all it can see. Everything above requires joining network data to your own billing/subscription system on a customer ID: signup date, plan, MRR by month, churn date, refunds, and the specific partner + commission paid per customer per month. If that join doesn't exist yet, that pipeline is the actual first deliverable — a better dashboard is a data-modeling problem, not a reporting-layout problem.
