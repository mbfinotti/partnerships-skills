# Gate Decision Addendum — Kelver Alliance Shortlist

**No — I won't build that scorecard.** Adding "security posture" as a 15%-weighted criterion doesn't make the sheet reflect the risk; it launders a pass/fail failure into partial credit. The tell is in your own math: you already found a weight where Piedmont scores a 1 and still lands second. That's not a criterion capturing severity — that's a criterion engineered to survive the thing it's supposed to measure. Any weight low enough to let a SOC 2 lapse and a late-disclosed breach get outvoted by brand strength or account overlap isn't scoring the risk, it's absorbing it.

Security/compliance posture is a **must-pass gate**, not a scorecard input. Gates sit outside the tradeable composite for exactly this reason: a high score can't buy a candidate past one. If it could, it wouldn't be a gate — it'd be a criterion with a discount built in.

## Gate evaluation: Piedmont Analytics

**Gate: Security/compliance posture — FAILED.**

Evidence on file:
- No current SOC 2 Type II. Last attestation lapsed 14 months ago.
- Disclosed 2024 customer data exposure incident, disclosed late — a governance/transparency signal on top of the incident itself.
- The alliance's actual data flow requires pushing Kelver customer records to Piedmont — this is the highest-scrutiny version of the gate ("candidate cannot meet the data-sharing bar the alliance needs"), not a marginal case.

Any one of these would warrant a hard look. Together — no valid attestation, an unresolved incident history, and a live requirement to hand over customer PII — this fails the gate outright. No composite score offsets it, because the gate was never part of the composite.

**Verdict: removed from the ranked shortlist.** Not re-ranked lower, not parked at the bottom of the table — off it. Piedmont's 4.4 composite and 6 manager-months no longer occupy a shortlist slot.

**Route back: conditional-go only, tied to a named condition and deadline — not to a scored position.** Piedmont re-enters as a candidate (re-scored from scratch, gates run again) only once it produces, before consideration at the next portfolio review:
1. A current, unqualified SOC 2 Type II report from an independent auditor, covering a trailing 12-month period.
2. An independent post-incident review of the 2024 exposure showing remediation and a fixed breach-notification process (the late disclosure is itself part of what needs to be shown as fixed).
3. Counsel sign-off that the proposed customer-record data-sharing terms meet Kelver's own data-protection obligations — flag this to legal alongside the security gate, since a late-disclosed breach plus a live data-sharing ask is also where legal/antitrust exposure gets checked.

No calendar date is being invented for Piedmont's own remediation — that's on their timeline. The deadline that's real is ours: if those three items aren't in hand by the next scheduled portfolio review, Piedmont sits out that cycle too, same as any other candidate that hasn't cleared its gates yet.

## Why this can't be softened later either

The reason this landed on your desk as an argument instead of a checkbox is that Piedmont got scored and socialized (top of the sheet, in front of your VP) before its security gate ran. That's the sequencing the skill's staged-gate model exists to prevent — desk-checkable gates (attestation status, breach history) run across the whole longlist *before* anything gets composited, precisely so a candidate never becomes politically expensive to remove. Compounding that now by scoring around the gate would repeat the same mistake one level up.

## Remaining candidates: gates still owed

Piedmont's removal doesn't exempt the rest of the list from the same discipline. Before any of these hold a shortlist slot, confirm each has cleared, not just scored well on:
- **Financial viability** — funding history, layoffs, filings.
- **Legal/antitrust exposure** — counsel review of proposed terms, same lens just applied to Piedmont.
- **Exit path** — a wind-down that doesn't strand Kelver customer data mid-alliance.
- **Three-laws screen** — value beyond standalone, ability to operationally act as one, a workable value split.

If any of Northwind Cloud, Solvexa Data, or the other six candidates carry an open security/compliance question of their own, it gets the identical treatment: gate first, score never overrides it.

## Redrawn shortlist and capacity line

Piedmont's removal frees 6 of the manager-months that were committed against it. That capacity doesn't default to whoever's composite score is next-highest — recompute the effort-sum cut line with Piedmont out, then re-rank the remaining gate-cleared candidates on value ÷ effort, same as the rest of the sheet. Concretely: Northwind Cloud (4.8, 7 manager-months) and Solvexa Data (3.2, 4 manager-months) hold their positions only if they've separately cleared this same gate set — that hasn't been confirmed here and needs to be before either is treated as safe. The freed 6 manager-months likely reopens one slot among the six remaining candidates (2–5 manager-months each), but which one depends on scores I don't have yet.

## Open questions

- Confirmed gate status (all five gates, not just security) for Northwind Cloud and Solvexa Data — has anyone checked, or did the sheet skip straight to scoring for them too?
- Names, composite scores, and effort estimates for the six unnamed candidates — needed to actually redraw the effort-sum line rather than describe it directionally.
- Whether legal's review of Piedmont extends to regulatory exposure from the late disclosure itself (separate from the security gate, and worth a named line item if so).
- Confirm with your VP: is the ask now "help me make the case for Piedmont's conditional-go path once they remediate," or "help me find what fills that shortlist slot now" — those are different next steps and worth pinning down before the Tuesday conversation, not during it.