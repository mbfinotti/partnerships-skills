## Payout Audit — Quill & Hearth apparel affiliate program, April run

This is a B2C ecommerce order-level CPA program (flat 8%, new-run cadence), so the discipline is the standard pending → approved → locked → paid lifecycle. No export files were attached to this task, so checks 2–7, 9–11 (line-level reconciliation, dedup, rate/tier recompute, currency/tax) are **blocked pending data** — I can't issue a pass/fail on the arithmetic. What you _did_ give me is enough to fully diagnose check 8 (lifecycle), and it's bad enough to hold the run on its own.

**Bottom line: hold the $52,140 release.** Two of the three symptoms you listed are lifecycle blockers, not rounding noise.

### Checks

| #   | Check                                        | Status                                                                                                         |
| --- | -------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 1   | Freeze scope                                 | Partial — period, rate, window lengths known; timezone, date basis, currency, materiality threshold not stated |
| 2   | Pull exports                                 | 🔴 Blocked — no platform export or order/billing extract attached                                              |
| 3–4 | Comparability / reconcile to source of truth | 🔴 Blocked — no source-of-truth extract                                                                        |
| 5   | Exception queue                              | 🔴 Blocked                                                                                                     |
| 6   | Dedupe                                       | 🔴 Blocked (line-level), but reversal reason-code gap already visible (see F-2)                                |
| 7   | Rate/tier recompute                          | 🔴 Blocked — flat 8%, no tiers described, so low structural risk once data arrives                             |
| 8   | Lifecycle/clawback                           | 🔴 **FAIL** — see F-1, F-3 below                                                                               |
| 9   | Currency/tax/thresholds                      | 🔴 Blocked — not discussed                                                                                     |
| 12  | Maker-checker                                | ⚠️ Unknown — you didn't say who calculates vs. who releases                                                    |

### Findings

**F-1 | 🔴 blocker | $ at risk: unquantified, systemic | run-wide**
Your validation window (7 days) is less than a quarter of your return window (30 days). Apparel returns run high by nature (skill benchmark: ~25%+), and CPA planning bands top out at 8% — you're already 2–3x that. The window isn't sized to the reversal curve, it's sized to affiliate complaints. Every commission approved on day 7 has 23 more days to come back as a return you can no longer catch on-platform.
_This is the root cause of F-4, not a separate problem._

**F-2 | 🟠 material | ~20 of 41 reversals, $ at risk unquantified**
Roughly half your reversals have no reason code. Per the standard reason-code list (invalid card, return/cancellation, duplicate order, customer fraud, affiliate fraud, non-qualified lead, test transaction), an uncoded reversal is unauditable and indistinguishable from an erroneous void. It also means you can't tell how many of the 41 are legitimate returns vs. something else — including affiliate fraud, which is out of this audit's scope but worth flagging to fraud review if a pattern shows up once coded.
**Action: require a reason code before any reversal counts as resolved. Backfill or reverse-out the ~20 blank ones before this run is considered clean.**

**F-3 | 🔴 blocker | 63 lines, $ value unknown — request per-line amounts**
Pending → paid with no approved/locked state in between is a skipped state, not a fast validation. These 63 lines never got even the (already too-short) 7-day window — they got zero. "I think our platform auto-approves" is the right instinct: find the config rule causing this (per-traffic-source auto-approve toggle, a webhook that fires approve+pay together, a threshold-based fast-track) and disable it. Until then, treat every line in this bucket as unverified regardless of dollar size.
**Action: hold these 63 lines out of this release until you can confirm each one legitimately cleared the window, or reprocess them under a corrected config.**

**F-4 | 🟠 material — trend, not a single-run number**
Reversal rate 19% → 22% → 24% over three consecutive runs is _rising_, not just elevated. Combined with F-1, the likely mechanism is: shortening the window didn't reduce actual returns, it just pushed more of them past lock, where they show up as unrecoverable leakage instead of clean in-window reversals. If untreated, expect this run's true reversal rate (once the full 30 days elapse) to land at or above 24% of the $52,140 base — call it **~$12,500 of exposure that a 7-day window has no chance of catching**. That number is a projection from your own trend, not a recomputed finding — treat it as the size of the problem you're buying by not fixing F-1.

### What to fix, in order

1. **Fix the window/return mismatch (F-1) — this is the actual bug.** Don't just extend the window and re-anger affiliates. Use the fix-it-forward move built for exactly this tension: keep a fast payout cadence, but hold a **reserve/holdback** (size it to your own 24% trend, e.g. 20–25%) against the 30-day return curve, released after the return window closes. Affiliates get most of their money fast; you stop bleeding post-lock.
2. **Kill the auto-approve bypass (F-3).** Find the platform rule, disable it, and don't release those 63 lines until you know why they skipped state. This is a config bug, not a policy decision — fix it regardless of what you do about F-1.
3. **Enforce reason codes on every reversal (F-2).** No blank notes going forward; backfill or reverse the ~20 blank ones in this run before counting them as resolved.
4. **Confirm maker-checker.** Tell me who calculates this run vs. who releases funds — if it's the same person, that's the control gap that let F-1/F-3 go unnoticed for three runs running.

### To actually close this audit (not just diagnose it)

Send me, for the April run:

- The platform export and the order/billing system extract for the same period (same date basis, declared timezone).
- Whether **$52,140 is gross or already net of the 41 reversals** — this changes the variance math entirely and I can't tell from what you gave me.
- Per-line values for the 63 auto-approved lines, and the reason codes (once backfilled) for the 41 reversals.
- Materiality threshold and currency, so I can run checks 3–11 for real instead of on trend inference.

With that, I can run the full sequence (reconcile, dedupe, rate recompute, sampling) and give you an actual pass/hold verdict with a variance line instead of a projection. Until then: **hold the 63 lines and the ~20 uncoded reversals; release the remainder only if a maker-checker sign-off happens with someone other than whoever built this run.**
