# PAYOUT AUDIT — Verdanta Labs partner program

_Method note, stated plainly per firm policy: this isn't a platform-branded process — it's account reconciliation (preparer/reviewer), three-way match, and segregation-of-duties applied to a commission run._

```
PAYOUT AUDIT - Verdanta Labs partner program, run 2026-05, period 2026-05-01..2026-06-01 (TIMEZONE UNCONFIRMED, date basis UNCONFIRMED)
Scope     : 318 lines, proposed total ~$44,000 (USD/EUR/GBP, all settled to USD); sources: platform export ONLY —
            no billing/CRM source-of-truth export identified yet
```

## Checks

| #   | Check                               | Status                                                                                                                                                                                                                                                                                                                |
| --- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Freeze run scope                    | **PARTIAL** — run ID, exact period dates, timezone, and date basis (transaction vs. validation vs. amendment) not yet confirmed. Also unconfirmed: is this run already paid? It's a May run being audited in September — assume **already disbursed** unless told otherwise, which changes remediation options below. |
| 2   | Pull exports                        | **PARTIAL** — platform export in hand (318 lines). No internal billing/CRM extract mentioned — needed for check 4.                                                                                                                                                                                                    |
| 3   | Comparability gate                  | N/A pending 2                                                                                                                                                                                                                                                                                                         |
| 4   | Reconcile to source of truth        | **NOT DONE** — blocking. Nothing here confirms the platform's 318 lines and ~$44K match what your billing/CRM system says was actually sold/subscribed in the period.                                                                                                                                                 |
| 5   | Exception queue                     | N/A pending 4                                                                                                                                                                                                                                                                                                         |
| 6   | Dedupe                              | **NOT ASSESSED** — no data on duplicate keys or overlap with the April run's key set                                                                                                                                                                                                                                  |
| 7   | Rate/tier recompute                 | **NOT DONE** — commission structure (rate model, tier method, overrides) not stated                                                                                                                                                                                                                                   |
| 8   | Lifecycle state                     | **UNKNOWN** — validation window and paid/unpaid status not confirmed                                                                                                                                                                                                                                                  |
| 9   | Currency, rounding, tax, thresholds | **FAIL** — see F-1 through F-5 below                                                                                                                                                                                                                                                                                  |
| 10  | Coverage method                     | Not yet chosen — see recommendation below                                                                                                                                                                                                                                                                             |
| 12  | Maker-checker                       | **UNCONFIRMED** — calculator/releaser identities not given                                                                                                                                                                                                                                                            |

## Findings

**F-1 | blocker | $ at risk: unquantified, treat as material until sized | all EUR lines (count unknown out of 318)**
No platform documentation states which date the FX conversion strikes on (conversion, approval, or payout date — three different amounts). Independently, 5/5 EUR lines you spot-checked came in ~1.8% off the ECB rate for that day, **in the same direction every time**. A one-directional spread across 100% of a sample is not noise — it's the signature of either an undisclosed platform margin or a wrong/stale strike date. It cannot be waved through as rounding.
_Action:_ (a) get the strike-date policy from the platform in writing, or infer it by recomputing 1–2 known lines against conversion/approval/payout date and see which matches the platform's output; (b) confirm the direction — is Verdanta over- or under-paying relative to ECB; (c) check the partner terms for a disclosed FX margin. If undocumented/undisclosed, this is not a per-line error, it's a currency-class error — it needs a recompute of **100% of EUR lines** (and GBP lines, once ruled in or out) at the correct rate, not a sample.

**F-2 | blocker | $ at risk: ~2 payees' last known balance (estimate only, see note) | 2 payees**
Two payees who sat below the $50 minimum in last month's export are **absent entirely** from this month's file — not carried forward, not shown as paid, not shown as churned. Sub-threshold balances must roll forward and never vanish; a payee disappearing from the file is the named failure mode for exactly this. This is worse than F-4 below because it isn't "still under threshold," it's "gone."
_Action:_ HOLD. Pull last month's export, confirm the two payees' balances, and determine whether they were (a) paid out because they crossed threshold on other activity, (b) deactivated/churned with a balance the terms do or don't allow forfeiting, or (c) dropped by a broken carry-forward join. Restore the balance to this run or next before anything releases. Do not estimate this away — get the actual prior-month figures.

**F-3 | minor | $3.87 | run-wide, every line off by a cent or two**
This matches ordinary per-step rounding drift compounding across 318 lines — industry-normal, and $3.87 is far below your $250 materiality threshold.
*Action:* absorb and document. Confirm rounding happens once, at the end of each line's calculation, not at each intermediate step, and that one rounding policy applies to every line (not some truncated, some rounded).
**Important:** this $3.87 was computed against the platform's _own_ FX rates. It is a separate, smaller issue from F-1 and must not be treated as "the" unexplained variance — once F-1 is sized, the true residual variance will be different (likely larger, on the EUR lines).

**F-4 | informational | $148.22 | 4 payees**
Four payees currently sit below the $50 minimum, combined $148.22. On its own this is routine — verify these four specifically reappear with intact balances in the June export. This finding is really a checkpoint on whether F-2's carry-forward mechanism works at all; don't close it independently of F-2.

**F-5 | informational (process) | $0 this run | control gap**
The FX strike-date policy being undocumented is itself a finding, independent of whether the 1.8% turns out to be a disclosed margin or an error. _Action:_ fix-it-forward — get it in writing from the platform and file it in the program terms, so future runs check against a stated policy instead of re-inferring it every time.

## Exceptions

None can be built yet — the platform-vs-billing exception queue depends on check 4, which hasn't been run. Treat this as an open item, not "no exceptions found."

## Variance

Recomputed total: **cannot be certified yet.** The $3.87 you found is real but only reflects rate/tier-and-rounding accuracy against the platform's own FX — it is not the full unexplained variance. The EUR-line repricing under F-1 has to happen before any total can be trusted. Do not report "~$4 off, close enough" — that's the exact shortcut the skill's negative example exists to condemn, and here it would also be wrong on the facts, since F-1 hasn't been sized yet.

## Cleared

**Nothing clears yet.** Recommend holding the full run pending F-1 and F-2. Given this is a May run being reviewed in September, first confirm whether it's already been disbursed:

- **If still unpaid:** correct F-1 and F-2 before release (full recovery, no relationship cost).
- **If already paid** (likely, given the timing): F-1's correction becomes a forward-period negative or positive adjustment against future commission per payee; F-2's restored balance gets added to the next payable run for those two payees. Direct recovery (invoicing partners) should only be on the table if F-1 turns out to be a large, one-directional overpayment and finance/legal sign off — not by default.

## Coverage method for the recompute

Spot-checking 5 EUR lines already surfaced a systemic issue — that's exactly the case for **100% of EUR lines** (and a check of GBP lines too, currency-class risk), plus **100% of anything touching F-2/F-4** (near-threshold and prior-month sub-threshold payees), plus a random sample of the remainder sized against the $250 materiality. If you can execute code over the export, a full-population recompute is an hour once and near-zero every run after — worth building given this is a recurring monthly run.

## Sign-off

Not available — need: (1) who calculated this run vs. who would release it (must be different people — no confirmation given), (2) exact period boundaries/timezone/date basis, (3) confirmation of paid/unpaid status, (4) a billing/CRM extract to run check 4. **The run cannot pass until F-1 and F-2 are resolved and checks 1, 2, 4, 7, and 12 are completed** — everything else in this report stands regardless of those answers.
