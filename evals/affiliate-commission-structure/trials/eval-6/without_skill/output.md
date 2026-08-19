## Sanity check on cutting the hold to 10 days

**Don't do 10 days.** That's not a fix for the cash-flow complaint — it's a different, worse risk.

The validation hold exists to cover the window in which a sale can still unwind: customer return, refund, or chargeback. For a DTC cookware brand, that window is almost certainly 30+ days (most cookware brands run 30–100 day trial/return policies, sometimes longer for warranty-adjacent claims). If your return window is longer than 10 days — which it very likely is — cutting the hold to 10 days means:

- You pay commission on orders that later get returned or charged back.
- You now have to claw back money you already sent affiliates, which is worse for cash flow and worse for relationships than the current delay ever was — collecting money back from an affiliate is far more friction than making them wait for it.
- The two affiliates who left over cash flow will not come back for this; they'll come back for money arriving faster and more predictably, not for a term that quietly creates a future dispute.

**The actual problem isn't the hold — it's the stack.** Validation hold (60d) + net-45 payment + $250 minimum threshold can combine into 100+ days before an affiliate sees cash, and if they don't clear $250 in a cycle it rolls further. That's the thing affiliates are reacting to, not the hold specifically.

**One thing I need from you before finalizing a number:** what's Beltram Goods' actual return/refund window (and any warranty-claim window that generates chargebacks)? The hold should be set at that window plus a small buffer (5–10 days for processing lag), never shorter than it. Everything below uses a placeholder of 30 days — swap it for the real number.

## New payout terms

| Term | Old | New | Why |
|---|---|---|---|
| Validation hold | 60 days | **Return window + 10 days** (placeholder: 30 → 40 days if return window is 30d) | Must stay ≥ return/chargeback window. Only shrink if the real return window is shorter than 50 days — confirm before publishing. |
| Payment terms | Net-45 | **Net-15** after validation clears | This is the actual lever for "money moves faster" — cuts total latency without reopening clawback risk. |
| Minimum payout threshold | $250 | **$100** | $250 disproportionately hurts mid-size affiliates (the segment that just left) by making them wait multiple cycles to clear the floor. |
| Payout frequency | Monthly | **Bi-weekly payout runs** | Once validation clears, don't batch into one monthly run — shortens the average wait further at no fraud-exposure cost. |
| Fast-track tier (new) | — | Affiliates with 6+ months history and a return/chargeback rate below program average get hold cut to **return window + 3 days** | Rewards proven low-risk affiliates directly instead of loosening the policy for everyone, including new/unvetted accounts. |

**Net effect vs. today:** total time from sale to cash drops from ~105 days (60 + 45) to roughly ~55 days (40 + 15) for standard affiliates, and further for the fast-track tier — without shortening the hold below the return/chargeback exposure window.

**Still needed from you:** the confirmed return/refund window (and any separate warranty/chargeback window) so I can lock the exact hold-day number instead of the 30-day placeholder.