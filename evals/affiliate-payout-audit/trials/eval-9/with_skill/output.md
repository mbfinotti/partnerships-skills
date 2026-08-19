# Ashgrove Media payout audit — Tuesday, 6 hours, spreadsheets only

## Bottom line

Run 7 of 12 gates in full, run 3 more in a cut-down form, skip 2 entirely. The rate/tier recompute (gate 7) is not just "in scope" — it's promoted to the top of the queue, because your mid-period structure change matches the skill's own trigger for promotion, and it's the one check no spreadsheet shortcut can skip. "No code" does **not** mean "no full-population recompute" — it means you build the recompute as fill-down formulas instead of a script. That distinction is what makes this schedule fit in 6 hours.

## Three things reshaping the standard sequence

- **Hard Thursday release, Tuesday afternoon start** → drop full-population *script* recompute (you don't have it anyway), keep everything cheap-and-high-value.
- **Spreadsheets only, no scripts** → deletes nothing from gate 7 itself. A helper-column formula applied to all 1,930 rows *is* full-population coverage — it's just Excel/Sheets, not a script. Use it.
- **Nobody in finance before Thursday** → deletes *direct recovery* as a remediation option this run (no legal/finance sign-off available), and forces a workaround on maker-checker (see below). It does **not** delete the checker requirement itself.

## Before touching a single row (15 min, non-negotiable)

Pin these four facts — they block gate 7 specifically, and a wrong guess here corrupts every downstream number:

1. **Tier method**: marginal or retroactive on the new card. Same volume, different dollars — this is the single highest-leverage fact in the whole audit.
2. **Boundary operator**: does the threshold dollar itself earn the old tier or the new one (`>=` vs `>`)?
3. **Timezone + date basis** for the 1 May cutover and the 15 Apr–15 May window (transaction date, not payout/validation date — you need to classify each line as pre- or post-change by when the sale happened, not when it was reported).
4. **Materiality threshold**. If nobody's set one, use 0.5–1% of run value ($440–$880) as a placeholder and flag it as assumed in the report header.

If you genuinely can't get answers to #1 and #2 in the next 15 minutes, that alone is a blocker finding — say so in the report rather than guessing.

## Run in full

| Gate | What you actually do in a spreadsheet | Time |
|---|---|---|
| 1. Freeze scope | Write down run ID, period (half-open: `2026-04-15 <= t < 2026-05-15`), timezone, date basis, currency, materiality, both source files. | 10 min |
| 2–3. Pull + comparability | Load network export + internal source-of-truth extract for the same window. Before summing anything, confirm both use the same event definition, date basis, timezone, currency, counting method. If the network export defaults to validation date, re-pull on transaction date — don't hand-adjust. | 20 min |
| 4–5. Reconcile + exceptions | `SUMIFS`/`COUNTIFS` totals, network vs source of truth. Any gap → line-by-line, never "close enough." Build the exception queue with `COUNTIF`/`VLOOKUP` on order/transaction ID: in-network-not-in-billing = hold (over-credit risk); in-billing-not-in-network = expect a dispute, decide credit policy explicitly. | 45 min |
| 6. Dedupe | `COUNTIF` on the transaction ID column, flag >1. Quarantine blanks/malformed IDs rather than letting them collapse silently. If you can get last run's key list, `MATCH` against it to catch period-straddle double-pay; if you can't export that, note it as an unchecked limitation, don't skip the in-run dedupe. | 20 min |
| **7. Rate/tier recompute** | **See below — this is the core of the 6 hours.** | ~2.5 hrs |
| 9. Tax forms | `VLOOKUP` every payee against your tax-form status list. Missing/expired W-9 or W-8BEN = payee-level blocker, hold that payee regardless of everything else. This is cheap and the compliance cost of skipping it is disproportionate. | 20 min |
| 11–12. Report + sign-off | See templates below. | 45 min |

## Run cut-down

- **8. Lifecycle window** — don't audit every reversal rule. Filter for lines dated in the last ~10 days before 15 May (still inside a plausible validation window) and hold those pending clearance. Spot-check that any refund/cancellation flag in the export is reflected as a negative line, not silently absent. Skip a full clawback-policy review.
- **9 (rest). Rounding/thresholds** — one spot check that rounding is applied at the end of the line calc, not per-step (pick 5 lines with decimals, verify by hand). Skip a full rounding-policy audit. Sub-threshold carry-forward: only check if you can pull last run's under-threshold payee list in under 10 minutes; otherwise flag as unchecked, don't silently assume it's fine.
- **10. Coverage method** — full-population via formula for reconciliation, dedup, and rate/tier (all three are formula-doable across all 1,930 rows). Manual eyeball only for the lines your formulas flag as mismatched, plus every line within 48h of the 1 May cutover and every line crossing a tier breakpoint — that's a targeted 100% review of a small high-risk slice, not a random sample.

## Skip entirely, and say so in the report

- **FX strike-date verification** — skip if the program runs a single currency (confirm in 30 seconds; if $88,400 is genuinely multi-currency, this moves back into "run").
- **Direct recovery** as a remediation option this run — no finance/legal sign-off available before Thursday. If gate 7 finds an overpay, your only levers are: correct-before-release (if unpaid), hold, or absorb-and-document. Don't invoice anyone off a solo review.
- **VAT/self-billing review** — skip unless you know some payees are foreign entities; if so, a 2-minute check of which payees are cross-border is worth it, the full self-billing audit is not.
- **Sub-affiliate override audit, buyout-clause check** — skip unless Ashgrove's program actually has sub-affiliates or known bought-out partners. Confirm with a yes/no from memory, don't investigate blind.
- **Fix-it-forward design** (reserve policy, longer validation window, standing recompute script) — defer past Thursday. Note it as a recommendation if gate 7 shows the tier change is producing systematic errors, don't build it now.

## Gate 7 in detail — the part that actually decides this run

The trigger for promoting this gate is explicit: *the structure changed mid-period.* Every line dated 15 Apr–30 Apr owes flat 12%. Every line dated 1 May–15 May owes the tiered card, computed on **that partner's post-1-May volume only** — not their volume for the whole 15 Apr–15 May window. If the export or the payout tool computed tiers against the full-period volume, every partner who did any business before 1 May got their tier boundary pushed by pre-change revenue that was never supposed to count toward it. That's the failure mode to hunt for first.

Build these helper columns and fill down across all 1,930 rows:

1. Transaction date (from the export, not payout date).
2. Regime flag: `IF(date < 2026-05-01, "flat", "tiered")` in your declared timezone.
3. Running post-1-May volume per partner (a `SUMIFS` keyed on partner ID and date ≥ 1 May, evaluated as of each line — only needed for tiered lines).
4. Expected commission: flat lines = `0.12 * amount`; tiered lines = the marginal-or-retroactive formula per whichever method you pinned above, applied to the post-1-May running volume, with the boundary operator you pinned above.
5. Diff: `expected - proposed`. Filter for any nonzero diff — that's your finding list, at full population, no sampling error.
6. Separately flag: every line dated within 48h of 1 May (timezone/cutover risk), and every tiered line whose post-1-May cumulative volume sits within 5% of a tier breakpoint (a small date or amount error flips these lines by a lot — retroactive cliffs especially).

Everything the formula flags gets a manual look before it's classed as a finding; everything it doesn't flag is cleared at full-population confidence for a fraction of the manual-sample effort.

## Maker-checker, without finance

The requirement isn't "a finance person reviews it" — it's "the preparer isn't the releaser." If genuinely no one at all is available before Thursday:

- Release only the lines with zero findings and zero flags from gate 7.
- Hold every line touched by any finding, the exception queue, or a cutover/breakpoint flag — carry them to next run rather than release on your own sign-off.
- Get literally any other person — a manager, another ops lead, anyone not you — to read the finished report and totals for 15 minutes before you release, even if they can't re-derive the math. That's the minimum bar; skipping it entirely is the exact failure mode that ships every error at once.
- Record the gap in the report as an informational finding on the process, and schedule a real finance review for immediately after release, with authority to correct via forward-period offset if it turns anything up.

## Report to deliver Thursday morning

```
PAYOUT AUDIT - Ashgrove Media, run <id>, period 2026-04-15..2026-05-15 (<tz>, transaction date)
Scope     : 1,930 lines, proposed total $88,400 USD; sources: <network export> vs <source of truth>
Structure : flat 12% through 2026-04-30, tiered card from 2026-05-01 (marginal/retroactive: <confirm>)
Checks    : 1 pass | 2-3 pass/normalized | 4 totals: <pass/fail $X> | 5 exceptions: <N> | 6 dedup: <pass/fail>
            7 rate/tier: <pass/fail, N findings> | 8 lifecycle: spot-checked, <N held> | 9 tax: <N payees blocked>
            10 coverage: full-population formula recompute (gates 4,6,7) + targeted 100% on cutover/breakpoint lines
Findings  : F-1 ... severity | $ at risk | affected lines | action
Exceptions: <one-sided records, direction, resolution>
Variance  : recomputed total vs $88,400; findings must account for the gap to the cent, or the residual is its own finding
Cleared   : <lines, $ value> cleared for release at corrected values
Sign-off  : preparer <you> | checker <name, not you> | 2026-09-16 | RELEASE cleared lines only
Limitations: <prior-run key diff not checked / sub-threshold carry-forward not verified / whatever you skipped>
```

Pass only if every line is reconciled or on the exception list, unexplained variance is at or below materiality, and zero blocker findings remain outstanding — hold anything that doesn't clear that bar rather than releasing with a note.