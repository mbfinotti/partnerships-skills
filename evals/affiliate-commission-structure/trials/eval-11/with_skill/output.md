## Verdict: the $29.66 vs $41 comparison is comparing the wrong things. Once you correct for it, the affiliate channel is likely *more* expensive than your other channels, not 28% cheaper — reverse your ask before it goes to the board.

### 1. The arithmetic you did is correct, as far as it goes

- $86,000 ÷ 2,900 orders = **$29.66/order**. ✓
- $29.66 vs $41 CAC → 1 − (29.66/41) = 27.7% ≈ **28% cheaper**. ✓ (correctly rounded)

The error isn't in this division. It's in what the numerator and denominator represent.

### 2. Why the comparison itself is invalid

Two problems, both structural to affiliate attribution, not to your calculator:

**(a) Order ≠ incremental customer.** CAC on your other channels measures cost per *acquired* customer. Your $29.66 measures cost per *attributed order* — including orders from shoppers who were already going to buy and just clicked a cashback/coupon link on the way to checkout to collect a rebate. That's last-click credit on demand you already created, not demand the affiliate created.

**(b) You told me the partner mix, and it's the worst-case mix for this exact problem.** 46% of your order volume sits with two cashback partners and a coupon aggregator — precisely the partner types that research consistently shows run **66-71% non-incremental** (cashback/coupon/loyalty capture last-click credit on demand others created; cashback sites also rebate 30-70% of their commission straight back to the shopper, which is why shoppers seek them out regardless of your affiliate spend). Content sites and creators, by contrast, run **78-82% incremental** — they actually create demand.

A blended cost-per-order figure averages a channel that's mostly real (content/creators) with a channel that's mostly *not* (cashback/coupon), and the 46% concentration in the non-incremental bucket means the blend is doing a lot of hiding.

### 3. Re-running the number with incrementality applied

Correct formula: cost per incremental customer = total spend ÷ (orders × incrementality share), applied per partner-type bucket, not blended.

| Bucket | Orders (46%/54% split of 2,900) | Incrementality range | Incremental orders (low–high) |
|---|---|---|---|
| Cashback ×2 + coupon aggregator | 1,334 | 29–34% | 387 – 454 |
| Content + creators | 1,566 | 78–82% | 1,222 – 1,284 |
| **Total** | 2,900 | — | **1,608 – 1,738** |

True cost per incremental order = $86,000 ÷ (1,608 to 1,738) = **$49.49 – $53.47**

Compared to your $41 blended CAC, that's **not 28% cheaper — it's roughly 21% to 30% *more expensive*.** The midpoint (~$52) is 27% above CAC — almost the exact mirror image of the number in your draft. A ~55-percentage-point swing, entirely from correcting one assumption.

This uses published industry incrementality bands as a stand-in because you haven't measured your own yet — which is the next problem.

### 4. Two things to pull before this goes anywhere near the board

1. **A new-customer flag on affiliate orders**, if your platform tracks it. If a meaningful share of that 46% cashback/coupon volume is repeat customers rebooking through a cashback portal, your true new-customer CAC on that bucket is worse than even the range above — the order count itself is inflated, separate from the incrementality discount.
2. **Actual dollars paid per partner type**, not just order share. I assumed the $86K is spread proportionally to order volume across buckets. If your cashback/coupon partners are on a lower rate than content partners (standard practice, and worth confirming you're already doing it), the true skew is smaller than my estimate and the number lands toward the better end of the range. If they're on a flat CPA that overpays small orders, it's worse. Either way, don't present board math built on an assumption you can check with your own data in an afternoon.
3. **Run a 30-day holdout on the two cashback partners and the coupon aggregator** before the board date: pause them, watch whether total site conversion volume holds flat (they were harvesting existing demand — keep them capped) or drops (they were incremental after all — restore and document). This converts your board case from "industry-average incrementality bands say maybe" to "we tested it and here's what happened," which is a materially stronger thing to put in front of a board than either version of the blended number.

### 5. What I'd actually take to the board instead of "double the budget"

Doubling spend uniformly right now doubles the $86K flowing through the same 46%-non-incremental mix — you'd scale the part of the program that's least likely to be buying you anything before you've confirmed how bad it is.

Reorder the ask instead, cheapest and most reversible lever first:

1. **Cap or gate the two cashback partners and the coupon aggregator now** (new-customer gate if you have the flag; a straight rate cap below content/creator rates if you don't). This is a same-day rate-card change, not a renegotiation.
2. **Run the holdout test in parallel** to get your own incrementality number instead of an industry range.
3. **Then take the board ask specifically to content and creator partners** — that 54% of volume, at 78-82% incremental, is the part of the program actually beating your other channels, and a budget increase concentrated there is a defensible ask on the numbers you already have.
4. If the holdout confirms the cashback/coupon volume is largely incremental after all (possible — restore their rates and document it), fold them back into the doubling ask with real data instead of an assumed range.

Bring the board the corrected range and the fix in flight, not the $29.66 figure — it won't survive a CFO who asks "what's your incrementality-adjusted cost," and better that surface before the meeting than during it.