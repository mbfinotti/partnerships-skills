# Cadence Studio — Affiliate Fraud Response

## What actually happened

Month-11 and month-14 disputes on annual subscriptions, concentrated on two affiliates, is the **stolen-card transaction fraud** pattern: the fraudster builds a legitimate-looking signup through their own link, the card gets disputed months later, and the commission has long since paid out. This is not cookie stuffing or fake leads — those surface in days-to-weeks. It's the pattern no hold window reaches.

Your 60-day hold didn't fail — it was never built to reach month 11–14. Two dispute-code clocks apply to a card dispute: standard fraud/unauthorized-charge claims file within 120 days of the transaction, but services-not-received / not-as-described claims (which is how "I didn't want this renewal" or "I never used this" disputes usually get coded) run 120 days from the *expected delivery date*, capped at 540 days from the transaction. On an annual subscription, "delivery" is ongoing — a month-14 dispute is still squarely inside that window. **No realistic hold window covers this tail.** [ACADEMIC/regulatory: Visa/Mastercard filing-limit rules]

## Re-ranking the controls for this program specifically

The default order (hold window > detection rules > new-partner terms > clawback clause set) is ranked by cost-to-value ratio, not by what recovers money already gone. That default is overridden here by two conditions that both apply to Cadence Studio: **you sell subscriptions**, and **you have already paid out on a chargeback**. When either is true, the clawback clause set — the one control the efficiency ranking buries at the bottom — is the only thing that touches money that's already left the building, so it moves to the top.

**New order for this program: clawback clause set → hold-window tuning → new/high-risk partner terms → detection rule set.** Detection rules still get built (below), but they're not what stops this bleed.

## Immediate: the two affiliates

Stolen-card chargebacks are one of the three named triggers (alongside confirmed technical evidence and reoffense) that skip straight to **Suspend & Escalate** — don't route this through the default Hold & Investigate tier.

Open a dossier per affiliate now, before contact:

| Field | Action |
|---|---|
| Rule triggered | Chargeback concentration: 2 of ~120 affiliates account for $18K in one month |
| Evidence to pull | Payment/CRM records for every disputed customer; registration IP/device/billing on the "customer" account cross-checked against the affiliate account (self-referral check); redirect-chain and referrer audit; declared vs. observed traffic source |
| Financial exposure | Commissions paid on the disputed accounts (already gone); any commissions still in the 60-day hold on these two affiliates (throttle those to $0 immediately, today, regardless of what happens next) |
| Recommendation | Suspend both; void anything still held; claw back paid amounts *if your contract currently authorizes it* — see gap below |
| Reviewer | Program owner, not the analyst who found the concentration |
| Appeals | Neutral wording only ("commissions under review pending a routine quality check"), 14-day published window, reviewed by someone other than the detecting analyst |

**Check this before you try to claw anything back:** does the affiliate agreement currently give you clawback authority and negative-balance carry-forward? If it doesn't, reversing already-paid commissions is itself a breach of the terms the affiliate accepted — you cannot claw back what the contract never authorized you to claw back. If that's the gap, the $18K is very likely a sunk loss, and the entire point of what follows is to make sure the *next* $18K isn't.

Cross-referencing IP/device/billing to check self-referral is personal-data processing. Before running it: state your lawful basis, retention period, and who can see the matched records, and route the design to counsel. "We needed it to catch fraud" is not a basis on its own.

## Fix the money mechanics (this is the actual deliverable)

1. **Clawback authority + negative-balance carry-forward + chargeback reserve** — draft this now. Concretely:
   - Clawback clause: commissions paid on transactions later charged back are recoverable.
   - Negative-balance carry-forward: a clawed-back amount deducts from the affiliate's *future* payouts until offset, rather than requiring a separate collection action.
   - Chargeback reserve: hold back 10–15% of every affiliate's commission, released quarterly as long as their rolling chargeback rate stays under a threshold (e.g., 3%). [VENDOR rule of thumb — tune once you have your own 90-day chargeback-rate baseline per affiliate]
   - This changes terms affiliates already accepted, so it needs a notice period and, given the scale of the change, counsel review before you ship it to 120 partners.
2. **Hold window**: at 60 days you're already mid-range for a non-subscription program; for an annual-subscription, chargeback-exposed vertical, push it to 90 days [VENDOR: subscription/high-chargeback verticals sit at the long end]. Say explicitly to your own team why: 90 days still doesn't reach month 11–14, it only buys a bit more runway against faster-surfacing fraud. Don't let anyone read the 90-day move as "the chargeback problem is solved."
3. **New/high-risk partner terms**: find out now whether these two affiliates were recent signups. If so, apply net-60/90 payout terms and stricter application filters (free-email domains, generic phone, no real site) to new affiliates going forward — first-incident fraud concentrates in the new-partner cohort.

## Detection rule set

At ~120 affiliates and (based on $890/year × 120 partners at full volume) commission spend well under the ~$50K/month threshold where automated scoring starts to pay for itself, **manual review + IP/email validation beats building a scoring pipeline** here — put analyst hours into this, not tooling procurement.

| # | Signal | Threshold | Band | Action | Legitimate trip risk |
|---|---|---|---|---|---|
| 1 | Chargeback rate per affiliate | >3% rolling 30 days [VENDOR] | Suspend & Escalate | Suspend; reverse held commissions; dossier to network | Product-quality issue hitting many affiliates evenly — check whether the rate is program-wide before pinning it on one partner |
| 2 | Shared registration IP/device/billing between affiliate and "customer" accounts | Any match, confirmed | Suspend & Escalate | Self-referral — suspend, claw back if contract allows | None once confirmed — but the check itself needs the `[LEGAL REVIEW]` sign-off above |
| 3 | Conversion-rate outlier | >2 SD above your 90-day program mean, sustained 2+ weeks [VENDOR→tune to your data] | Watch | Log; weekly triage | Genuinely strong content partner — check traffic mix before anything else |
| 4 | New affiliate: no traffic, then a spike | Define your own spike threshold from actual data [DERIVE] | Watch | Manual review; keep on net-90 terms | Seasonal creator launch — check content publish dates |
| 5 | Declared vs. observed traffic source mismatch | Any material mismatch [DERIVE] | Hold & Investigate | Throttle; referrer audit | None — this is a direct cross-check, not a behavioral proxy |

You don't have 90 days of baseline data yet, and you only have one confirmed incident to backtest against. Say that plainly rather than pretending these thresholds are validated: schedule the first quarterly review as the point where you check catch rate ≥80% and false-positive rate ≤5% against sampled flags, and tune from there.

## Process going forward

- **Cadence**: weekly anomaly triage against the chargeback-rate and conversion-outlier rules; monthly reversed-commission/denied-affiliate report to finance.
- **KPIs**: chargeback rate per affiliate, confirmed-fraud rate, reversed-commission share, dollars recovered via clawback. Report in dollars, not risk language.
- **Escalate the program itself** if chargeback concentration recurs next quarter — that's the signal to revisit the reserve percentage and hold-window length again, not just re-run the same rules.

## What I assumed / what you should confirm

- Whether your current affiliate terms already contain any clawback or negative-balance language — this decides whether the $18K is recoverable at all.
- Whether the two affiliates are new signups or established partners with prior history.
- Whether tracking is server-side postback or client-side pixel — the self-referral cross-check needs server-side data to be trustworthy.
- Review capacity (who has the hours for weekly triage and dossier review) — if the answer is "nobody," the Hold & Investigate 24–48h review collapses to the weekly Watch triage, and the hold window carries more of the load by default.