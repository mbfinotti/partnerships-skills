## Arithmetic checks out — the framing doesn't

**The numbers themselves are right:**
- $86,000 / 2,900 orders = $29.66/order ✅
- ($41 − $29.66) / $41 = 27.7% ≈ "28% cheaper" ✅

The division is correct. The comparison it's being used to justify is not sound enough to take to a board yet. Four problems, roughly in order of how much they'd move the number:

### 1. Cashback + coupon aren't acquisition — they're a discount tax on demand you already had

46% of your orders (≈1,334) come from two cashback partners and a coupon aggregator. That category has the weakest incrementality of any affiliate sub-channel, for a structural reason, not a quality-of-partner reason: a customer who has already decided to buy and is mid-checkout will frequently search "[brand] coupon code" or "[brand] cashback" before hitting purchase. They click through, the cookie overwrites whatever channel actually drove the decision (paid search, email, direct, organic), and the sale gets attributed — and paid a commission — as if the affiliate created the purchase. This is well-documented industry-wide (it's the reason Honey/PayPal Honey drew antitrust and creator-lawsuit scrutiny, and why most sophisticated affiliate programs run incrementality holdouts specifically on coupon/cashback).

Consequence: your $29.66 blended CPO is a mix of two very different things —
- Content/creator orders (54%, ~1,566): plausibly incremental, closer to genuine discovery/acquisition.
- Cashback/coupon orders (46%, ~1,334): a meaningful share of these would have converted anyway through another channel that you already paid for once. You may be double-paying for the same order.

You cannot know the true CPO of "affiliate as a channel" without an incrementality estimate (holdout test, geo test, or at minimum a post-purchase survey / new-vs-repeat and AOV split by partner type) on the cashback/coupon segment specifically.

### 2. You're blending order-share with spend, and you haven't shown spend-share

You know 46% of *orders* come from three partners. You have not stated what share of the *$86,000* went to them. Cashback/coupon commissions are typically flat-rate or low-percentage; content/creator deals often carry higher commissions, flat retainers, or bonuses. If cashback/coupon consumed less than 46% of spend, the *content/creator* CPO is actually higher than $29.66 (worse than it looks), and if it consumed more, content/creator CPO is lower (better than it looks) — the blended average tells you nothing about either segment on its own. Pull spend-by-partner-type before the board meeting; this is a five-minute query and changes the story either way.

### 3. Comparing a blended affiliate CPO to a blended "other channels" CAC is apples-to-oranges twice over

- Your affiliate figure explicitly includes network fees. Confirm the $41 "other channels" CAC is calculated on the same fully-loaded basis (platform fees, agency fees, tooling, creative production) — if it's media spend only, the comparison flatters affiliate.
- "Other channels" is itself a blend (presumably paid search, paid social, etc.), each with its own incrementality profile. You're comparing one blended number that's partly non-incremental against another blended number without knowing its own incrementality either. The 28%-cheaper headline compares two numbers that aren't measuring the same thing.

### 4. "Double the budget" assumes constant returns to scale that affiliate inventory won't support

Cashback/coupon/aggregator placements are the easiest inventory to buy more of — but that's exactly the inventory with the incrementality problem in #1, so scaling there just buys more of the same margin leakage. Genuinely incremental growth would need more content sites and creators, which is a sourcing/negotiation/ramp-time problem, not a checkbook problem — you can't assume the next dollar buys orders at $29.66. Realistically, doubling the budget skews the mix *further* toward cashback/coupon (because that's the low-effort dollar to deploy fast), which would raise the true, incrementality-adjusted CPO, not hold it flat.

### What I'd do before presenting

1. Get spend-by-partner-type (at minimum: the three high-volume partners vs. everyone else).
2. Compute CPO separately for cashback/coupon vs. content/creator using that split.
3. Run even a rough incrementality check on the top 2-3 cashback/coupon partners (a 2-4 week holdout in a subset of geos/segments is the standard approach) — or at minimum compare new-customer rate and AOV for that segment against content/creator and against your other channels.
4. Reframe the board ask as "double the budget for content/creator, which is showing $X CPO and Y% new-customer rate" rather than "double affiliate" — that's a defensible, scalable ask. Asking to double a budget that's 46% concentrated in a channel with a known attribution-inflation problem is the version most likely to get picked apart in the room, or worse, approved and then embarrass you at the 12-month readout when someone runs the incrementality test you didn't.

The 28%-cheaper number may still turn out to be directionally true for the content/creator half of the program — but as stated, it's presenting a blended average that's most likely being pulled favorable by the least defensible part of the spend.