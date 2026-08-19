# Detection rules for Vellum & Thread's affiliate program

## First: the stat that got you here

Park the 17% / $3.4B number. It's a single anti-fraud vendor's marketing study, circularly cited across the industry — nobody has independently reproduced it, and it's usually paired with "$3.4B lost" style figures (also vendor-sourced: 8-15% of commissions, IVT ~40% of web traffic) that don't agree with each other by methodology. It's not wrong to be alarmed by fraud; it's wrong to size your response off a number nobody can audit. Use your own data instead — that's what the rest of this does.

## The bigger problem than any rule below

**Your 14-day hold window is shorter than the chargeback windows that create most of your unrecoverable fraud loss.** Standard Visa/Mastercard chargebacks have a 120-day filing window from the transaction. Services-not-received / not-as-described claims run 120 days from expected delivery, capped at 540 days from the transaction. A stolen-card purchase run through an affiliate link looks completely legitimate at day 14 — the chargeback lands 60-180+ days later, by which point you've already paid the commission.

This is the single highest-leverage fix available to you, and it costs about an hour (one platform setting) versus a week to build the rule set below. It does carry a notice obligation to existing affiliates since it changes terms they already accepted, so it can't be silently applied retroactively to orders already in the 14-day clock — but you can extend it for new orders starting now, with notice.

**Before Thursday**, I'd:
1. Not touch the hold window for orders already in this cycle (notice hasn't gone out).
2. Send affiliates notice today that the validation window is extending — 30 days minimum, 45-60 days is safer given your chargeback exposure — effective for orders placed from a stated date forward.
3. Confirm with whoever owns your contract terms whether you have clawback / negative-balance carry-forward authority today. If not, that's your top priority after Thursday — it's the only control that recovers money already paid, and it's the sole cover for the 120-540 day chargeback tail no hold window reaches.

## What I assumed, since there wasn't time for a full interview before Thursday

You gave me: 340 affiliates, ~$58K/month, last-click, 30-day cookie, 14-day hold. I don't know the following, and they change the rule set materially — flag corrections and I'll re-tune:

- **Tracking method** (client-side pixel vs. server-side postback). Assumed unknown/mixed. This matters a lot: cookie-stuffing detection *requires* server-side signal capture — a client-side pixel literally cannot distinguish a stuffed cookie from an organic one. If you're pixel-only, rule C2 below is compromised until you add postbacks.
- **Permitted partner types** — coupon, cashback, loyalty, extensions, brand-bidding, email. Assumed a normal DTC mix including coupon/cashback/extension partners, since nothing said otherwise.
- **Review capacity** — who has hours to review flagged cases weekly. Assumed at least an affiliate manager + finance can do a 24-48h review; if that's wrong, everything below collapses to Watch + monthly batch review, and the hold window has to carry the program alone.
- **Existing clawback authority** in your affiliate terms. Assumed none, given no mention.
- **Historical incidents.** Assumed none confirmed yet — this affects whether the rule set can be backtested (see Pass Threshold below).
- **One-off vs. standing**: I'm treating this as a standing control, not a one-time cleanup, since you asked what you "should be running."

## Control ranking for your situation

Four controls compete for your time; rank before writing rules:

| Control | Value | Effort | Status for you |
|---|---|---|---|
| Hold window extension | Stops most fraud before it pays out (Edelman & Brandi, *JMR* 2015: delaying payment 2-4 months eliminated 70%+ of fraud with no profit loss) | ~1 hour, notice required | **Do first**, starting post-Thursday |
| Clawback clause + reserve | Only control that recovers money already paid; only thing that reaches the 120-540 day chargeback tail | A quarter — legal drafting, partner re-assent | **Start drafting this week**; you have no evidence you have this today |
| Detection rule set | Tells you *which* partner to act on, produces evidence enforcement can stand on | A week to baseline + build, then a standing job | This is the deliverable below |
| New/high-risk partner terms (net-60/90) | Narrows exposure from the cohort that produces most first-incident fraud | ~1 hour | Apply to any new affiliate approved from now on |

A rule set sitting on a 14-day hold with no clawback flags fraud you can't actually act on financially. Fix the top two rows; the rule set below is necessary but not sufficient on its own.

## Step 1 — Baseline (do this before trusting any threshold)

Pull 90 days of per-affiliate data: conversion rate, click-to-conversion time, session duration, refund/chargeback rate. Compute program mean and standard deviation per metric. Flag affiliates >2 SD from norm as your watchlist starting point ([VENDOR] agency workflow — a sane starting definition, not a standard). Re-derive quarterly.

At 340 affiliates and $58K/month, you're well past the ~50-affiliate / $50K threshold where manual-only review stops scaling — layer automated per-event scoring on top of manual review rather than relying on manual alone.

## Step 2 — The rule set (B2C ecommerce)

You're DTC ecommerce, not lead-gen, so this is the B2C rule family only — don't apply form-fill/lead-quality rules, they're for B2B lead-gen and will misfire here.

| # | Signal | Threshold (provenance) | Band | Action | Legitimate trip risk |
|---|---|---|---|---|---|
| V1 | Data-center ASN / declared bot / non-browser UA | Any — GIVT list filter | — | Filter pre-commission, no case opened | None — list-based, no judgment call |
| V2 | Time on merchant site after cookie set | < 2s [ACADEMIC — Snyder & Kanich 2016] | Hold & Investigate | Throttle; run cookie-drop reproduction (clean browser, visit suspect page, check if cookie sets without a click) | Deep-linked flash-sale/email traffic — check landing page. **Needs server-side postback data to be reliable — flag if you're pixel-only** |
| V3 | Conversion rate | > 2 SD above program mean, sustained 2+ weeks [VENDOR → tune with your data] | Watch | Log; weekly triage | Genuinely strong content partner — check traffic mix before escalating |
| V4 | Chargeback rate | > 3% rolling 30 days [VENDOR] | Suspend & Escalate | Suspend; reverse violation-period commissions; dossier to network | Product-quality issue, not fraud — compare against other affiliates' rate first |
| V5 | High clicks, near-zero conversions | > 5x your program's click-to-sale ratio [DERIVE from your data] | Hold & Investigate | Throttle; referrer + redirect-chain audit | Top-of-funnel content partner — check engagement metrics |
| V6 | Extension/toolbar flips last-click seconds before checkout | Attribution change < 60s pre-purchase, recurring [DERIVE] | Hold & Investigate | Stand-down audit; check contract terms | Permitted coupon/cashback extension — your terms decide this, not the rule. High last-click share alone is never fraud evidence — it's a repricing question |
| V7 | Branded-search ad traced to an affiliate | Any, if your terms prohibit brand bidding | Suspend & Escalate | Timestamped SERP screenshots across geos; warn once, then suspend | Whitelisted partner — check the whitelist before acting |
| V8 | New affiliate: silent 2 weeks, then spikes | > 50 conversions in week 3 from cold start [DERIVE] | Watch | Manual review; hold to net-90 terms | Seasonal creator launch, or a real campaign date — check content calendar |
| V9 | Self-referral | Shared registration IP/device/billing between affiliate and "customer" accounts [DERIVE] | Suspend & Escalate | Suspend; reverse; dossier | None credible once confirmed — but confirm the match before acting, not on IP alone |
| V10 | Multi-account ring | Shared device fingerprint, IP, or payout destination across "unrelated" accounts [DERIVE] | Suspend & Escalate | Suspend; dossier; clawback | Household/office sharing a connection — corroborate with a second signal before acting |

**`[LEGAL REVIEW]` on V9 and V10**: matching device fingerprints, IPs, or payout details across accounts is personal-data processing. State your lawful basis and retention period, and route the rule design to counsel before it goes live — "we needed it to catch fraud" is not a lawful basis on its own.

Every row above already carries its false-positive check inline — that's deliberate; it's the cheapest control you have and kills the most common false positive before anyone gets flagged.

## Step 3 — Operating procedure

**Bands** (default new rules to Hold & Investigate; move down to Watch if a legitimate cause is plausible; move up to Suspend & Escalate only on confirmed technical evidence, chargebacks, or repeat offense):

- **Watch** — log, keep paying, weekly triage. Near-zero cost.
- **Hold & Investigate** — throttle new commissions to zero, open a dossier, cross-functional review (affiliate manager + finance, legal on call) within 24-48h. Reversible — pay it and the partner is made whole.
- **Suspend & Escalate** — suspend, reverse/void period commissions, clawback if authorized, dossier to network compliance, legal if warranted. Least reversible; do this only on solid evidence.

**Cadence**: daily tracking-health check + new-affiliate review; weekly anomaly triage + 10-15 affiliate spot-check; monthly/quarterly performance and reversed-commission audit for finance.

**Dossier fields per case**: affiliate/network ID, rules triggered with timestamps, baseline vs. observed values, evidence artifacts (cookie-drop repro, redirect-chain capture, screenshots, logs), financial exposure, declared vs. observed traffic source, prior history, recommended action + reviewer, appeal status/deadline.

**Communication**: never say "fraud" to the flagged affiliate — "your commissions are under review pending a routine quality check, expect an update by [date]." Give a 14-day appeal window reviewed by someone other than the flagging analyst.

**Never rely on the network to police this.** Networks are paid on commission volume — their compliance is reactive to evidence-backed complaints, not proactive surveillance of your program.

## Step 4 — This Thursday, specifically

1. Run V1 (list filtration) against the whole batch — zero judgment, zero cost, do it regardless of anything else.
2. Run V4 and V9/V10 against anything with chargeback or duplicate-identity signals already visible in this cycle's data — these are your highest-confidence, fastest checks.
3. Anything tripping Hold & Investigate: throttle it out of Thursday's run, open a dossier, pay everyone else on schedule. Don't hold the whole payout hostage to a handful of suspect accounts.
4. Anything tripping Watch: pay it, log it, review at next week's triage — don't let an unvalidated rule delay real partners' money.

## Pass/fail check before you trust this rule set

Backtest against confirmed incidents (if you have any) plus a manual sample of flagged and unflagged affiliates. Target: ≥80% of known incidents fire at Hold & Investigate or above, ≤5% of sampled flags are false positives. **You told me nothing about historical incidents** — if you have none confirmed, say so explicitly to your team and schedule this as a first-quarterly-review gate on sampled flags rather than treating any threshold above as validated yet.

## KPIs to report

Flagged rate, confirmed-fraud rate, false-positive rate (sampled), reversed-commission share, recovered spend. Report in commission-dollars saved/recovered, not "risk" language. If confirmed-fraud or reversed-commission share climbs quarter over quarter, that's a signal to revisit the hold window and vetting — not just tune the rules.

## After Thursday — the next 90 days

1. **This week**: notice-and-extend the hold window (target 45-60 days given your DTC/no-subscription profile — you don't need the 90-day subscription-vertical end, but 14 is far too short).
2. **This week**: confirm/draft clawback + negative-balance carry-forward + a chargeback reserve (10-15% of commissions, released quarterly while chargeback rate stays under threshold) into your affiliate terms.
3. **This month**: confirm tracking (pixel vs. postback) — if pixel-only, prioritize adding server-side postbacks; your cookie-stuffing detection is otherwise unreliable.
4. **This month**: classify your partner roster by type (content, coupon, cashback, loyalty, extension, brand-search) so V6/V8 don't misfire on legitimate checkout-moment partners.
5. **Ongoing**: re-derive baselines quarterly; retire any rule that only ever produces false positives.