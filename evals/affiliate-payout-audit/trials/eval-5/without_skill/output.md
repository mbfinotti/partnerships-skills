## Audit verdict: Northbeam Outfitters — March payout ($27,880)

**❌ Not good to go.** Four issues stack on top of each other, and one of them (the manual line-moving) invalidates the reconciliation itself, not just a few line items.

### 🔴 Critical — manually moved 22 lines to match the order DB count
Forcing the network export to match your order database's row count is not reconciliation, it's making the two numbers agree by construction. It doesn't tell you the 22 lines belong in March — it tells you where you put them.

- Revert this before anything else.
- Re-derive any date mismatch from the actual transaction data, not from "which bucket makes the totals line up."
- If the counts still don't match after fixing the date-field issue below, that's the real signal to investigate — missing orders, cancelled orders, or a network reporting gap.

### 🔴 Critical — wrong date field, so the two systems don't measure the same thing
You exported on **validation date**, not transaction date. Validation date is when the network approves the transaction, which can lag the actual order by days or weeks. Your order database presumably keys off order/transaction date. Comparing a validation-date export against a transaction-date database means:

- Some March-validated transactions belong to February (or earlier) orders — inflating March.
- Some March orders haven't validated yet and are simply absent from this export — deflating March.

Fix: re-export on **transaction date** (or whatever field matches your order DB's semantics), then re-run the comparison from scratch.

### 🟠 High — timezone boundaries are not actually aligned
Three clocks, three offsets, and DST doesn't move on the same day in the US and EU:

- US DST starts Sun **Mar 8, 2026** (Chicago: CST UTC-6 → CDT UTC-5).
- EU DST starts Sun **Mar 29, 2026** (Berlin: CET UTC+1 → CEST UTC+2).
- Network timestamps are UTC throughout.

"1 March 00:00 through 31 March 23:59:59" is meaningless until you say *in which timezone*. If that's naive/UTC, it's wrong for both other systems — and even converting once isn't enough, because the Berlin offset at the start of March (+1) differs from the offset at the end of March (+2). E.g. "March 1 00:00 Berlin" = Feb 28 23:00 UTC, but "March 31 23:59:59 Berlin" = March 31 21:59:59 UTC.

Fix: pick one authoritative calendar (Berlin, since that's what the order DB uses) and convert the network's UTC window and the program calendar's Chicago window to match it explicitly, offset-by-offset, not with a single fixed delta for the whole month.

### 🟠 High — 14 order IDs duplicated across the Feb and March runs
These came from the re-export after a late batch. If they were already paid in the February run, including them again in March's $27,880 double-pays them.

- Pull the February payout file and confirm whether those 14 IDs were paid there.
- If yes: exclude them from March entirely.
- If no (Feb run excluded them and this is their first appearance): keep them in March, but document why, so the next audit doesn't flag them as new duplicates.

### What "good to go" requires
1. Revert the 22 manually-moved lines.
2. Re-export using transaction date.
3. Re-apply the March window using one consistent timezone reference, respecting the differing US/EU DST transition dates.
4. Reconcile the 14 cross-period order IDs against the February payout, excluding any already paid.
5. Recompute the total. $27,880 has no evidentiary value until steps 1–4 are done — treat it as provisional, not approvable.