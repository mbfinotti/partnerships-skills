# Ferra Analytics — Affiliate Fraud Control Set

14 affiliates, ~$9K/month, homegrown tracking, instant commission approval, solo operator, ~2 hrs/week. That combination rules out the single highest-leverage control this skill would normally lead with (a hold window), so the plan below is built around what's actually available to you, not a generic template.

## One thing I need you to check before this is complete

"Approves instantly" — does that mean the money physically leaves your account the moment an order lands, or does it just mark the commission as payable in your ledger, with actual disbursement still happening on some cycle (weekly/monthly/net-X)?

This matters because if there's _any_ gap between "approved" and "paid out," you have an undeclared hold window sitting in your payout cadence, even without touching the approval logic. Check this yourself — I'm not blocking the rest of the plan on it, because the actions below work either way, but it changes how much of a flagged commission is actually recoverable without a clawback fight.

## Assumptions I made from your message — correct any that are wrong

- "Order" implies purchase-based commissions (CPA/CPS), not lead-gen (CPL). The rules below are the skill's B2C/purchase-mechanics family — cookie-stuffing, chargebacks, self-referral, last-click poaching. If you also pay for leads/trials/signups separately, tell me and I'll add the B2B lead-quality rules (they key off completely different signals — lead-to-qualified rate, form-fill speed — and mixing the two families produces false positives).
- "Ferra Analytics" reads as a subscription SaaS product. If commissions are recurring (affiliate earns on every renewal, not just the first order), that's good news for clawback mechanics — see below. If it's one-time-purchase, say so.
- You have order-level data today (affiliate ID, customer info, amount, timestamp) but probably not separate click/session logs, since nothing in your message mentions tracking clicks apart from orders. The rule set below is split into what works on order data alone (usable this week) and what needs a small one-time logging addition (not the same ask as a validation delay — logging a click timestamp doesn't touch your payment path).
- No clawback authority and no historical fraud incidents mentioned — I'm treating both as true. Tell me if either is wrong.

## Why the plan is shaped this way

With 14 affiliates, statistical outlier detection (2 standard deviations, automated per-event scoring) is false precision — you have too few data points per affiliate for it to mean anything, and reading 14 rows by eye every month is faster than building a model to do it. Skip the tooling; read the list.

With no hold window and 2 hours a week, two of the four usual controls are gone before you start: the hold window can't exist, and a real cross-functional review (the thing "Hold & Investigate" normally leans on) doesn't exist either — it's just you. That leaves detection rules, new-partner terms, and clawback authority to do all the work. Because the hold window — the thing that normally recovers >70% of fraud for free — isn't available, **the clawback clause stops being optional**. It's the only mechanism left that gets money back once it's out the door, and if Ferra bills subscriptions, the chargeback dispute window runs 120–540 days past the transaction — no realistic hold window would have covered that tail anyway, so this isn't really a downgrade, it's the control this business always needed most.

## Action #0 — before any rule fires (one-time, ~2–3 hrs total, do this first)

Add to your affiliate terms, sent to all 14:

- **Clawback authority**: confirmed fraud or a chargeback lets you reverse the commission.
- **Negative-balance carry-forward**: if there's nothing to reverse it from, deduct from that affiliate's future commissions until offset. This only works if commissions are recurring/ongoing — if they're one-time bounties, you need a direct invoice/collection fallback instead, and you should decide now which affiliates that applies to.
- **Chargeback reserve**: hold back 10–15% of a new or already-flagged affiliate's commission until their chargeback rate proves clean for a quarter. Cheap to write, no engineering.
- **Stricter terms for any new affiliate**: net-45 payout instead of instant, until they have a track record. This doesn't touch your approval logic — it only delays when _you_ disburse, which you control regardless of tracking system.

This is a short addendum, not a renegotiation — with 14 partners this is an afternoon of drafting plus sending it out, not the "quarter" this normally takes at scale. Do it before anything below fires, because a rule with no clawback behind it just tells you who defrauded you after the money's already gone.

## The rule set

**Phase 1 — usable today, order data only:**

| #   | Signal                                                     | Threshold                                                                                                                          | Band                                   | Action                                                                                                                       | Legitimate trip risk                                                                             |
| --- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| R1  | Refund/chargeback rate                                     | >3% rolling 30 days [VENDOR — tune once you have 90 days of your own numbers]                                                      | Suspend & Escalate                     | Pause the affiliate's link immediately (stops new exposure); invoke clawback/negative-balance on the flagged period; dossier | Product-quality issue hitting everyone — check the other 13 affiliates' rate first               |
| R2  | Self-referral                                              | Customer's email, name, address, or payment fingerprint matches the affiliate's own account [DERIVE]                               | Suspend & Escalate                     | Pause link; claw back that order's commission; this one doesn't need an investigation window, it's binary                    | None credible — this is deliberately checked, not a coincidence signal                           |
| R3  | Duplicate customer identity within one affiliate's orders  | Same phone/address/name pattern across "different" customers [DERIVE]                                                              | Hold & Investigate                     | Pause link on new orders; manually call 2–3 of the flagged customers to confirm they're real                                 | Legitimate reseller/agency placing orders for multiple clients — ask them directly before acting |
| R4  | Order-volume spike vs the affiliate's own trailing average | 3x+ their normal weekly volume, sustained, no announced campaign [DERIVE]                                                          | Watch → Hold if it holds a second week | Pause link if Hold; otherwise log and check next month                                                                       | Real campaign or seasonal push — check if they told you about one                                |
| R5  | Sales concentration                                        | ~80%+ of monthly commission from 1–2 of your 14 affiliates [VENDOR — practitioner heuristic, re-verify]                            | Watch                                  | Audit only, never enforce — this is normal affiliate power-law distribution                                                  | This is the expected shape for a 14-affiliate program, not itself suspicious                     |
| R6  | New affiliate: silent, then a sudden burst                 | No orders for 2+ weeks after approval, then a large first batch [DERIVE]                                                           | Hold & Investigate                     | Pause link; manually review the first batch of orders before releasing further commissions                                   | Slow-starting creator/partner who just launched content — check what changed                     |
| R7  | Declared traffic source vs what you can see                | You said "social" but every order's referrer is blank or unrelated — only usable if your checkout captures referrer today [DERIVE] | Watch                                  | Log; ask the affiliate to explain at monthly review                                                                          | Referrer stripped by the customer's browser/privacy tool — common and not evidence alone         |

**Phase 2 — needs one small logging addition (recording a click timestamp + referrer when the affiliate cookie is set — a few hours of dev work, unrelated to your payment/approval path, so it doesn't touch the "no validation delay" constraint):**

| #   | Signal                                        | Threshold                                                                                                                | Band               | Action                                                                                                                      | Legitimate trip risk                                                                 |
| --- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| R8  | Time between click and order                  | Order lands in under ~2 seconds of the click, or a cookie appears with no click at all [ACADEMIC — Snyder & Kanich 2016] | Hold & Investigate | Pause link; reproduce in a clean browser (visit their page, check if a cookie drops with no click)                          | Deep link from an ad straight to checkout — check the landing page before concluding |
| R9  | Data-center ASN / bot user-agent on the click | Any match                                                                                                                | — (list filter)    | Discard pre-commission automatically if your host/CDN already tags this (many do for free — check before building anything) | None — this is list-based, not a judgment call                                       |
| R10 | Redirect chain / referrer domain              | Traffic arrives via a misspelled version of your own domain or an unfamiliar intermediate domain [DERIVE]                | Hold & Investigate | Pause link; screenshot the redirect chain                                                                                   | None credible if confirmed — this is a specific technical tell                       |

Thresholds tagged [DERIVE] are placeholders until you've watched your own 14 affiliates for a stretch — you don't need 90 days of formal baselining at this scale, a spreadsheet with 14 rows updated monthly is enough to know what "normal" looks like for each partner.

## Weekly/monthly operating rhythm (fits inside 2 hrs/week)

- **Weekly, ~20 min**: scan the last 7 days of orders for R1, R2, R4 — the fast, high-signal checks that don't need a full data pull. This is where you catch something before a second week of bad orders piles up.
- **Monthly, ~60–90 min**: full pass — update the 14-row baseline sheet, check R3, R5, R6, R7 across the month, review anything sitting on Watch to decide if it graduates.
- **Recurring load: ~35–40 min/week average** — leaves you real headroom inside your 2-hour budget for the weeks something actually trips and needs a proper look.

## What "Hold & Investigate" means for you specifically

Since you can't delay approval, treat it as two actions, not one:

1. **Pause the affiliate's tracking link immediately** — stops new fraud accruing regardless of what's already approved. This you can always do.
2. **Flag already-approved commissions as disputed** if your ledger has any status separate from "approved" that blocks the next disbursement. If it doesn't, that money's recoverability now depends entirely on the clawback clause from Action #0 — another reason that comes first.

## Escalation ladder — solo-adapted

| Band               | Who decides                                                                                      | Timeline                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| Watch              | You, at the weekly/monthly scan                                                                  | Log it, revisit next cycle                                                            |
| Hold & Investigate | You                                                                                              | Same day you spot it — pause the link, spend up to an hour confirming before deciding |
| Suspend & Escalate | You (call a lawyer for an hour if it's a real dollar amount or a stolen-card chargeback pattern) | Immediate suspension, dossier written before you contact the affiliate                |

## Dossier — one page, per case

```
Affiliate: [name / ID]         Date opened: [date]
Rule(s) triggered: [R#, with the actual numbers vs your baseline]
Evidence: [order export, chargeback notice, reproduction screenshot, etc.]
Exposure: [$ approved, $ already paid, $ recoverable via clawback]
Declared vs observed: [what they said their traffic was vs what you saw]
Prior history: [none / warned on date X]
Action taken: [pause / clawback invoked / suspended]
Appeal: notified [date], neutral wording, 14-day window
```

Contact wording, always: "your commissions are under review pending a routine quality check." Never the word "fraud" to the affiliate — that's for your own notes.

## Tracking whether this is working

Track monthly, in dollars not risk language: flagged count, confirmed-fraud count, false positives found on review, commission $ reversed, $ actually recovered via clawback. You have no incident history to backtest against yet — say that's the case and treat your first full quarter of data as the calibration point for whether these thresholds are too loose or too tight, rather than shipping them as final today.

## Two things this doesn't cover

- Repricing a coupon/cashback partner who's legitimately just winning last-click at checkout isn't fraud — don't enforce on high conversion rate alone (R4/R5 exist to route you to a look, not a suspension). That's a commission-structure question, not a fraud one.
- The contract language above is enforcement plumbing, not full terms. If you want the prohibited-tactics clauses and enforcement ladder written into the actual agreement, that's a short follow-up, not part of this.
