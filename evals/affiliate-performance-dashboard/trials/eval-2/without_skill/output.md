This is an affiliate attribution problem, not a performance problem. Last-click on a 30-day cookie systematically overpays whoever touches the customer last, and coupon/cashback sites are structurally built to be that last touch. Here's what to measure before you cut anything.

## The core question

Did the coupon site _cause_ the sale, or did it just intercept a sale that content already created? Last-click can't tell the difference. You need to test for incrementality, not just look at the leaderboard.

## 1. Run a coupon-site holdout / suppression test

The single most decisive thing you can do.

- Pick a sample of traffic (or a set of geos/segments if you can't split traffic cleanly) and **block your top coupon/cashback affiliates' links from firing for ~2-4 weeks** — redirect them to a plain landing page or temporarily deactivate the offer for that subset.
- Compare total site conversions and revenue in that window vs. a matched control period/segment, not just "coupon line went to zero."
- If overall sales barely move, those affiliates were harvesting demand that would have converted anyway. If sales drop close to 1:1 with the lost coupon-attributed revenue, they were genuinely incremental.
- This single test settles more than any amount of dashboard analysis. Coupon-industry studies (and most retailers who've run this) typically find 70-90% of coupon-site "sales" would have happened anyway — but you need _your_ number, not the industry number.

## 2. Path analysis: what happened before the last click

Pull multi-touch path data (most affiliate platforms — Impact, Awin, CJ — expose click/impression logs even under last-click payout).

- For orders credited to coupon sites, look at the **full click path in the 30-day window**: did a content affiliate, paid search, email, or organic touch the same customer earlier?
- Metric to build: **% of coupon-site-credited orders where a content affiliate touched the same session/customer first.** If it's high, content is doing discovery/persuasion work and coupon sites are just closing at checkout — the CPA is being misallocated, not earned twice.
- Separately measure **content-first-then-coupon-last** paths as a % of content affiliates' total influenced (non-credited) traffic. This is the revenue content is currently generating for free.

## 3. Coupon-search behavior signal

- Segment coupon-site clicks by **time-to-purchase and cart state**. A huge share of coupon-site clicks happen in the last few minutes before checkout, often from users who already had items in cart, searching "Petalgrove promo code." That's demand capture, not demand generation.
- If you have session recordings or funnel data, check what % of coupon-site referrals arrive directly at checkout/cart vs. a landing/category page. High checkout-entry share = strong incrementality red flag.

## 4. Brand vs. non-brand keyword overlap

- Check whether coupon/cashback sites rank on **branded search terms** ("Petalgrove coupon", "Petalgrove promo code") — i.e., are they capturing your own branded demand that would've come to you directly, cookie or no cookie?
- If yes, you're paying 10% CPA to intermediate a sale a customer was already going to make by typing your name into Google.

## 5. New-customer vs. repeat-customer mix

- Break down each channel's orders by new vs. returning customer.
- Content affiliates typically skew toward new-customer acquisition (discovery, "best plants for X" content ranks for non-brand, top-of-funnel queries). Coupon sites typically skew toward existing/repeat customers who already decided to buy and are just looking for a discount.
- If coupon sites are mostly monetizing repeat buyers, that 10% CPA is a margin leak on demand you already owned, not customer acquisition cost.

## 6. Discount cannibalization / AOV impact

- Compare **AOV and margin per order** for coupon-attributed orders vs. content-attributed orders. Coupon codes often train customers to expect discounts and can suppress AOV or push customers who'd have paid full price to use a code they found via the coupon site (again, capturing not creating).

## 7. Assisted-conversion / view-through reporting

- If your affiliate platform supports it, pull **assisted conversions** (multi-touch, not just last-click) for each affiliate type. Compare each content affiliate's "assisted" credit to their "last-click" credit — this is often where you'll see content affiliates are 5-10x more valuable than the leaderboard shows.

## What to bring to leadership

Build one table: **Channel | Last-click revenue | Incremental revenue (from holdout) | Assisted-conversion revenue | New-customer % | Effective CPA on incremental sales.**

That last column reframes everything — a coupon site's _nominal_ CPA might be 10%, but if only 20% of its credited sales are incremental, its _real_ CPA on sales it actually caused is 50%. Content affiliates likely show the inverse pattern.

**Bottom line:** don't defend content's spot on the leaderboard — replace the leaderboard's metric. Last-click is measuring who touched the sale last, not who created it. The holdout test (#1) is the one piece of evidence that will actually settle the argument with leadership, because it's a real revenue number, not a modeled one — budget the 2-4 week test before making the cut.
