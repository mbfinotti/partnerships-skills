# PAYOUT AUDIT — Thistlewood Home affiliate program

**Run:** February payout · **Period:** _not yet declared_ · **Timezone:** _not yet declared_ · **Date basis:** _not yet declared_
**Proposed release:** Friday · **Proposed total:** $31,406.18 · **Sources cited:** network export (1,904 conv., 7‑day window) vs. in‑house tracker (1,671 conv., 30‑day window)

This uses the affiliate-payout-audit methodology (account reconciliation / three-way match / segregation of duties). I'm giving you the checker's read, not a rubber stamp — and the numbers you described trip three blockers before any line-level math is even needed.

## Checks

| #   | Check                        | Result                                                                                                                                                      |
| --- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Scope frozen                 | **FAIL** — no period start/end, timezone, or date basis given                                                                                               |
| 2   | Exports pulled               | Partial — two source _summaries_ given, no line-level export                                                                                                |
| 3   | Comparability gate           | **FAIL** — 7-day vs. 30-day attribution window is a different event definition; the two counts are not addable                                              |
| 4   | Reconcile to source of truth | **FAIL** — no declared source of truth (network / in-house / order-billing system); four different numbers on the table with no reconciliation between them |
| 5   | Exception queue              | Cannot build without matched keys                                                                                                                           |
| 6   | Dedupe                       | **FAIL** — two tracking systems, not collapsed to one canonical source                                                                                      |
| 7   | Rate/tier recompute          | Blocked — commission structure not provided                                                                                                                 |
| 8   | Lifecycle/clawback           | Blocked — validation window and lock event not stated                                                                                                       |
| 9   | Currency/tax/thresholds      | Blocked — no data given                                                                                                                                     |
| 10  | Coverage method              | N/A until real exports exist                                                                                                                                |
| 12  | Maker-checker                | **FAIL** — same person calculates and releases                                                                                                              |

## Findings

**F-1 | BLOCKER | comparability violation, "3,575 conversions"**
The network's 1,904 (7-day window) and the tracker's 1,671 (30-day window) are two overlapping claims about the same underlying conversions, not two additive populations — they use different attribution windows, so a conversion the tracker credits on day 20 simply never appears in the network's 7-day count, and vice versa. Summing them into 3,575 double-counts an unknown but likely large share of orders. **Action:** retract the 3,575 figure already given to the exec team; pick one canonical source (normally whichever one is contractually payable — usually the network export — with the in-house tracker used only as a QA cross-check, never as a second payable count); dedupe on order/transaction ID before any total is reported again.

**F-2 | BLOCKER | unexplained variance $2,906.18 (9.3% of payout)**
$31,406.18 proposed vs. $28,500 internal estimate is not tracking noise — it's 9.3% of the run, and every dollar in it is either an overpay or underpay to a real partner. A $2,900 gap only looks small next to a $31K total; measured against any sane materiality threshold for a program this size it's almost certainly a hold-the-run gap, not a rounding footnote. **Action:** drive this to $0 unexplained (or to a documented, line-itemized set of findings) before release — not "close enough."

**F-3 | BLOCKER | no maker-checker**
You calculate the run and release it yourself. On a four-person team this is the cheapest fix available and the one control that catches everything else on this list — it costs one scheduling ask, not a rebuild. **Action:** before Friday, hand the recomputed run to one of the other three people for sign-off; do not release on your own signature. This is non-negotiable regardless of team size — small teams still need the roles to differ, they just rotate who plays which role.

**F-4 | INFORMATIONAL, pending data | rate/tier and lifecycle unverified**
Nothing here confirms $31,406.18 traces to a real per-line calculation, and nothing confirms February refunds/reversals were applied before lock. This is exactly the "refund lands after lock, gets dropped" failure mode — worth an explicit check even if you have no reason yet to suspect it. **Action:** needs a line-level export to check at all.

## Variance

| Figure            | Value                       | Status                                                   |
| ----------------- | --------------------------- | -------------------------------------------------------- |
| Network export    | 1,904 conv. (7-day window)  | one claimant                                             |
| In-house tracker  | 1,671 conv. (30-day window) | second claimant, not additive                            |
| Reported to exec  | 3,575 conv.                 | **invalid — retract**                                    |
| Proposed payout   | $31,406.18                  | unverified against any per-line source                   |
| Internal estimate | $28,500.00                  | unverified methodology                                   |
| Unexplained delta | $2,906.18                   | **above any plausible materiality bar — FAIL, not PASS** |

Recomputed total: **cannot be produced** until a real line-level export exists. Nothing below is safe to release on the current basis.

## Cleared

**0 lines.** Nothing has been reconciled to a source of truth yet — there is no basis to clear anything for Friday as currently proposed.

## Sign-off

Preparer: you. Checker: **must be a different person on the team** — not yet assigned. Release decision: **HOLD the run as proposed.**

## What to fix before Friday (ranked for a tight deadline)

Given the deadline and a 4-person team, tackle in this order — dedup and reconciliation catch the most dollars per hour of work:

1. **Declare one canonical source** and dedupe network vs. tracker on order/transaction ID (near-zero effort if you can run a join over both exports; this alone likely resolves most of the "3,575" problem).
2. **Reconcile the deduped total against your actual order/billing system** — not a spreadsheet estimate — to get a real source of truth, not a third guess.
3. **Get a second person to check the recomputed run** before you release anything. Trivial cost, blocks every error above from shipping.
4. If time remains: spot-check rate/tier on your top-earning affiliates and confirm no February refunds landed after the commission locked.

I need four things to finish this properly: the period start/end + timezone + date basis you're using, which system is your actual source of truth, the commission structure (rate/tier rules), and your materiality threshold. Send those and I'll turn this into a real pass/fail with a recomputed total instead of a hold notice.
