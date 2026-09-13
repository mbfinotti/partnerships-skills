# Ashgrove Media payout audit — Tuesday afternoon → Thursday release

**Core risk in one sentence:** you switched commission logic mid-period (flat 12% → tiered) inside a run that spans both regimes. Almost all of your exposure sits at that boundary. Everything else is secondary.

Total budget: ~6 hours. No scripts, spreadsheet only (pivot tables, SUMIFS/COUNTIFS, XLOOKUP, conditional formatting, helper columns).

## 🔴 Run these (non-negotiable, ~4h)

1. **Nail down the boundary definition before touching data (20 min).**
   Confirm with the actual written policy (not memory): is the cutover based on _conversion/order date_, _click date_, or _approval date_? Networks often report by approval date, which lags the order date by days — a 30 April order approved 3 May can silently get the wrong rate either direction. This single ambiguity is your biggest failure mode.

2. **Get an independent total from the network (10 min).**
   Export or screenshot the network's own summary total for the period. Compare against your $88,400. If your file and their dashboard disagree before you've changed anything, stop and find out why first — don't audit a file that's already wrong at the source.

3. **Boundary-correctness check, every row (90 min).**
   Add a helper column: `=IF(order_date<DATE(2026,5,1),0.12,XLOOKUP(volume_tier,tier_table))`. Compare it to whatever rate the export actually applied. Filter to mismatches only.
   - Pivot rate-applied × date (bucketed pre/post 1 May) — any tiered rate before 1 May, or flat 12% on/after 1 May, is a hard flag.
   - Pay special attention to the 3–5 days around 1 May — that's where date-field ambiguity (point 1) actually bites.

4. **Tier-assignment logic check, post-1 May rows only (45 min).**
   Confirm what volume the tier is computed on: per-affiliate cumulative volume for the _whole_ period, or just the partial 1–15 May window. A partial-month volume base will systematically under-tier high-volume affiliates. Spot-check the 5–10 highest-volume affiliates by hand against the signed tier table (not a draft copy).

5. **Duplicate check (20 min).**
   Pivot: count of rows by transaction/order ID. Anything >1 gets a flag. Affiliate payout duplicates are the classic "pay twice" error and trivial to catch with a pivot.

6. **Reconciliation to $88,400 (15 min).**
   SUM the commission column, tie to the proposed total. Then SUMIFS split pre-/post-1 May — sanity check that the post-May tiered total isn't just "12% with extra steps" (a sign the tier table wasn't actually applied) and isn't wildly higher than the pre-May run-rate would predict either.

7. **Clawback/refund handling across the cutover (30 min).**
   Filter for negative amounts / status = refunded/cancelled. Confirm refunds on orders originally commissioned at 12% are clawed back at 12%, not at the new tiered rate (and vice versa for later orders). This is an easy miss because it requires matching the _original_ commission event's rate, not the _refund_ event's date.

8. **Pareto pass on dollar exposure (45 min).**
   Sort descending by commission amount. With 1,930 lines you cannot eyeball all of them in the time you have, but the top ~50 lines by $ almost certainly account for a large share of the $88,400. Manually sanity-check those — order value × correct rate = commission, correct affiliate, correct currency. This buys you the most risk-reduction per minute of anything on this list.

9. **Paper trail, even though finance can't review (20 min).**
   Before releasing, save: the tier table version you used, the boundary-date rule you assumed, the pivot showing 0 mismatches (or the flagged list you decided to hold back), and the network's total vs your total. This isn't optional — it's what lets finance audit _after_ the fact instead of _before_, which is the actual mitigation for "nobody can look at this before Thursday."

## 🟠 Do only if steps 1–9 finish early / or the flagged count is high

- **New/changed bank details flag** — if the export has a "payment details last updated" field, filter for changes in the last 30 days and hand-check those affiliates specifically (BEC/fraud vector, disproportionate to file size).
- **Currency consistency check** — pivot currency column, confirm no affiliate is mixing currencies mid-period from a data-entry slip.

## ✅ Skip, deliberately, and say so in your handoff note

- **Row-by-row manual verification of all 1,930 lines.** Not feasible in spreadsheets-only in 6h, and the Pareto pass (step 8) captures most of the dollar risk anyway. Don't pretend you did full coverage — say you did top-N + systematic checks.
- **Click-to-conversion fraud audit.** That's the network's control, not something a rate/tier reconciliation should be re-litigating under deadline.
- **Per-affiliate contract re-verification that the new tiered structure legitimately applies to them** (vs. a grandfathered flat-rate deal). Only spot-check this for the top-50 Pareto affiliates, not all of them — full coverage is a finance-review-time task, not a Tuesday-afternoon task.
- **Tax/withholding recomputation.** Unless withholding literally can't be corrected next cycle, defer — don't let it block Thursday's release.
- **Historical trend/anomaly analysis vs. prior runs.** Useful, not urgent; the boundary-date bug is a known, specific risk — spend the time there, not on general anomaly hunting.

## If you find mismatches in step 3

Don't try to hand-patch 1,930 rows under time pressure. Instead:

- **Split the run**: release everything that passes the boundary/tier/duplicate checks clean now, and hold back only the flagged lines (should be a small subset if the network's logic is mostly right) for a fast follow-up once finance can actually look.
- Communicate the holdback to affected affiliates as "processing" rather than silently late — cheaper than clawing back an overpayment later.

This gets you a defensible Thursday release even without finance eyes on it: the highest-dollar risk (the rate cutover) gets full coverage, the highest-dollar exposure (top-N) gets manual review, and everything you didn't fully check is explicitly logged rather than silently assumed fine.
