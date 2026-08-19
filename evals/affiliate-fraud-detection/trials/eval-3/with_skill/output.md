# SignalCrate Affiliate Fraud Detection Rule Set

## 0. Do this before anything else — check the clock

You onboarded these two partners in June, and you hold commissions for 90 days. From today (Sept 12), **leads generated in early-to-mid June are at or past the 90-day mark and may already be releasing for payout.** Before reading further:

- **Freeze/extend the hold on both partners' pending balances now** (Hold & Investigate, see below) — this is a one-hour platform setting and it's the only reason a detection rule set is worth anything. A perfect rule set on money that already paid out is a clawback problem, not a detection problem.
- Confirm whether your contract has clawback / negative-balance carry-forward authority for anything that *already* cleared the hold. If it doesn't, that gap needs fixing in the contract regardless of what the rules below find — flag it to whoever owns partner terms today, not after this investigation closes.

## 1. Assumptions made to deliver this without a back-and-forth

You asked for the rule set directly, so I'm not running the interview question-by-question — I derived what I could from your prompt and made explicit, checkable assumptions for the rest. Confirm/correct these before you operationalize:

| Given | Assumed (confirm before relying on it) |
|---|---|
| $150/qualified lead, CPL, 44 partners, server-side postbacks, 90-day hold, B2B SaaS | Review capacity: unknown → I've assumed standard cadence (below) is staffable. If nobody has review hours, Hold & Investigate collapses to Watch + monthly batch, and the hold window carries the program alone. |
| Two June partners, high volume, ~50% no-answer rate per sales | Clawback authority (negative-balance carry-forward, chargeback/dispute reserve) not confirmed — check this now, it gates whether Suspend & Escalate can recover money already paid. |
| — | Permitted partner types/traffic sources not specified — rules below assume a standard B2B referral/content/paid-search partner mix, not coupon/cashback (rare in B2B CPL). If any of the 44 are agencies submitting leads on behalf of clients, flag that up front — it's a named false-positive risk below. |
| — | No historical confirmed-fraud incidents given → no backtest baseline exists yet. Per the Pass Threshold below, that's stated explicitly rather than pretending these thresholds are validated. |
| 44 active partners | Below the ~50-partner / $50K-month threshold where automated per-event scoring starts paying for itself → **manual review + IP/email validation is the right primary method today**, not a scoring model. Re-check if monthly commission spend is materially above $50K. |

## 2. Control ranking for this program

Four controls compete for your hours: hold window, clawback clauses, detection rules, new-partner terms. Given the timing above, this program's answer is a **cycle-level urgency**, which changes the default ranking:

1. **Hold window** — already exists at 90 days; the only action needed right now is *not letting it silently expire* on these two accounts.
2. **Detection rule set** (below) — names which of the two partners to act on and builds the evidence to act on it.
3. **Clawback clause set** — promote this above its normal (low) priority the moment you find confirmed fraud in money that already cleared the hold. Don't wait for that to happen to check whether the clause exists.
4. **New/high-risk partner terms** — apply net-60/90 and stricter filters to *future* new partners; it doesn't touch the June cohort retroactively.

## 3. Baseline (do this in parallel with the June-partner investigation)

Pull 90 days of per-partner data across all 44 partners: lead-to-contacted rate, lead-to-qualified rate, lead-to-demo-show rate, click-to-conversion time, refund/void rate. Compute program mean and standard deviation per metric. Flag partners beyond 2 SD from program norms [VENDOR — agency workflow, not a standard]. Re-derive quarterly.

With 44 partners you're just under the size where 2-SD math gets noisy — it's usable here, but treat any single-partner flag on a thin sample (under ~30 leads) as weak until volume builds.

## 4. What "half never answer the phone" actually is — and isn't

"Never answers the phone" is sales' informal name for a **lead-to-contacted rate collapse** — the dominant B2B CPL fraud tell, per the taxonomy: bots or click-farms submitting forms with invented, recycled, or stolen contact data. But by itself it is *not* proof of fraud — it's equally consistent with a legitimate partner sending real-but-poor-fit traffic (wrong ICP, incentivized clicks, a lead magnet that overpromises). Don't skip straight to enforcement; corroborate with the identity and behavioral signals below before moving past Hold & Investigate.

## 5. Detection rule set

Signal → threshold (provenance) → band → action → the legitimate behavior that could trip it.

| # | Signal | Threshold | Band | Action | Legitimate trip risk |
|---|---|---|---|---|---|
| R1 | **Lead-to-contacted rate** (sales actually reaches a live person) | Sustained <50% of program norm over 30+ leads [DERIVE from your 90-day baseline — this directly formalizes the sales complaint] | Hold & Investigate | Throttle new commissions to zero; sample-call 10 leads from the flagged partner | Wrong-ICP targeting or bad phone-number capture UX — check other partners' contact rate on the same landing page/form |
| R2 | Lead-to-qualified rate | <half program norm over 30+ leads [DERIVE] | Hold & Investigate | Throttle; CRM outcome export into dossier | Untrained SDR routing that period — check other partners' rate over the same window |
| R3 | Lead-to-demo-show rate | Near zero over 20+ booked [DERIVE] | Suspend & Escalate | Suspend; reverse unlocked leads | Wrong-timezone booking flow — check actual booked times before concluding |
| R4 | Disposable/role-account email domains | >10% of partner's leads [VENDOR, tune to your program] | Hold & Investigate | Throttle; validate remaining leads manually | Privacy-conscious ICP (security/eng buyers) — cross-check against R2 before acting |
| R5 | Duplicate contact data (phone/email/device fingerprint) across a partner's "different" leads | Same identifier, 3+ distinct company names [DERIVE] — **`[LEGAL REVIEW]`**: state lawful basis, retention period, who can see matched records before this rule ships | Suspend & Escalate | Suspend; dossier; clawback | Agency submitting leads for multiple clients — verify against the partner's signed profile before concluding fraud |
| R6 | Form-fill completion time | <3s, no pointer movement, identical field-skip pattern [VENDOR] | Hold & Investigate | Throttle; pair with R1/R4 before acting | Autofill power users — never act on this signal alone |
| R7 | Conversion velocity | 3+ leads/minute, or metronomic ~30s spacing, repeated | Hold & Investigate | Throttle; server-log review of the postback batch | Legitimate webinar/conference lead-list upload — check event calendar first |
| R8 | New-partner cold-start spike | Approved, quiet for the first weeks, then a volume spike — **directly relevant to your two June partners** | Watch on approval → escalates to Hold if paired with R1/R2 | Manual review; hold to net-90 terms regardless | Seasonal campaign launch — check the partner's own content/campaign dates |
| R9 | Declared traffic source vs. observed referrer | Meaningful, sustained mismatch [DERIVE] | Watch → Hold if paired with any signal above | Referrer audit; compare to application declaration | Server-side postback with blank referrer is normal for some legitimate integrations — confirm it's not just a tracking gap |
| R10 | Volume up, zero closed-won customers downstream | 90 days, 50+ leads, no closed-won [DERIVE] | Watch → Hold at quarterly review | Reprice-or-exit conversation, not automatic enforcement | Long enterprise sales cycle — match the review window to your actual cycle length, not a fixed 90 days |
| R11 | Data-center ASN / declared bot / non-browser UA on the click layer | Any (GIVT) | — (list filter) | Filter pre-commission, no case opened | None — list-based, no judgment call |

**Do not build:** B2C click-timing/cookie-stuffing rules (sub-2-second CTIT, session duration) — those defend the click layer of ecommerce programs and produce false positives if applied to a B2B CPL motion with server-side postbacks. Your fraud surface here is the conversion/account layer (R1–R8), not the click layer.

**On R5 specifically**: this is the rule most likely to turn "half don't answer the phone" into an actionable case, because it's the one signal AI-generated synthetic lead-gen can't easily fake — duplicate identity across "different" leads. Run it on the two June partners first.

## 6. Immediate action on the two June partners

This is a one-off investigation riding on top of the standing rule set above, not a separate process:

1. Pull each partner's full lead list since onboarding: contact data, form-fill timestamps, referrer, CRM outcome (contacted/qualified/demo-booked/closed).
2. Run R1, R2, R4, R5, R6 against each partner's own leads (baseline doesn't need 90 days for a one-off case — compare directly against the 44-partner program average).
3. Sample-call 10–15 "no answer" leads per partner yourself; note dead numbers, wrong numbers, disconnected numbers, correct-but-uninterested numbers (the last is a targeting problem, not fraud).
4. Open one dossier per partner:

```
DOSSIER <date> — partner "<name>" (platform ID <id>)
Rules triggered  : R1 (<contacted %> vs <program norm>%), R4 (<duplicate-domain %>),
                   R5 (<N> leads across <N> device fingerprints, if confirmed — this is
                   the rule a Suspend recommendation should rest on, not R1 alone)
Baseline vs seen : lead-to-contacted <norm>% → <observed>%; lead-to-qualified <norm>% → <observed>%
Evidence         : CRM export (<N> leads, outcomes); <N>/<N> sample calls dead/invalid numbers;
                   postback log — duplicate identifiers found: <yes/no, detail>
Exposure         : $<held> held (<N> leads × $150); $<paid> already paid prior cycle (if hold
                   already lapsed on early-June leads — check this first per §0)
Declared vs seen : declared source "<x>"; observed referrers <finding>
Prior history    : onboarded <June date>, <N> weeks active, no prior flags
Recommendation   : <Hold & Investigate | Suspend & Escalate> — reviewer: <name, not the
                   detecting analyst>
Appeal           : notified <date>, neutral wording ("commissions under review pending a
                   routine quality check" — never use the word "fraud" to the partner),
                   14-day window
```

5. Band assignment: **R1+R2 alone → Hold & Investigate.** Only move to Suspend & Escalate once R4 or R5 confirms fabricated/duplicated identity data, or the partner reoffends after a warning. High no-answer rate with clean, non-duplicated, real-looking contact data is a targeting/quality problem — route it to commission repricing or a partner-fit conversation, not enforcement.

## 7. Investigation & enforcement — standing procedure

**Cadence:** daily tracking-health check (postback fires, reconciliation); weekly anomaly triage against baselines + spot-check 10–15 campaigns; monthly/quarterly performance audit and reversed-commission report for finance.

**Escalation ladder:**

| Band | Owner | Timeline | What it does |
|---|---|---|---|
| Watch | Affiliate ops analyst | Weekly triage | Log, keep paying — soft anomalies, first offenses |
| Hold & Investigate | Affiliate manager + finance (legal on call) | 24–48h | Throttle new commissions to zero pending review, open dossier — preserves evidence, reversible |
| Suspend & Escalate | Program owner + legal | Immediate | Suspend, reverse/void violation-period commissions, clawback paid amounts, terminate, report to network, legal referral if warranted |

Assign every new rule to Hold & Investigate by default. Move down to Watch only when the signal alone has a plausible legitimate cause. Move up to Suspend & Escalate only on confirmed technical evidence (duplicate identity, stolen data) or reoffense after warning — never on first flag, since instant bans destroy the evidence a network or legal escalation needs.

**Due process:** external communication stays neutral — "your commissions are under review pending a routine quality check" — never the word "fraud" to the partner. Published appeals path, 14-day window, reviewed by someone other than the detecting analyst.

## 8. Pass threshold — before you trust these numbers

You have no confirmed-incident history yet, so these thresholds are **starting points, not validated rules.** Backtest requirement: ≥80% of known incidents fire at Hold & Investigate or above, and ≤5% of a manually-reviewed sample of flagged partners are false positives. Since you have no incident history to backtest against yet, **say so explicitly and schedule this as the first-quarterly-review gate** on whatever the rules flag in the next 90 days — don't ship these as final until that review runs.

## 9. KPIs to report

Track together, never catch-rate alone: flagged rate, confirmed-fraud rate, false-positive rate (from sampled manual review), reversed-commission share, recovered spend. Report to leadership in commission-dollars saved/recovered, not risk language. If confirmed-fraud rate or reversed-commission share climbs quarter over quarter, that's a signal to revisit the hold window and new-partner vetting — not just tune the rules harder.

## 10. Out of scope here

- Whether the $150 rate itself is right, or whether to reprice non-incremental-but-legitimate partners → commission-structure work, not this rule set.
- Writing the prohibited-tactics clause and enforcement ladder into the partner contract → contract-terms work; this rule set only detects operational violations of terms that already exist.
- Confirming clawback/negative-balance authority is actually in your current contracts → check this today given §0; if it isn't there, that's the highest-priority gap this whole exercise surfaced.