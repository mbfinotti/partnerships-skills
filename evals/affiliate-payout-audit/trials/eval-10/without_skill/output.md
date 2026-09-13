## Affiliate Reconciliation — Decision on the $31,400 Hollowbrook Goods Run

**Recommendation: do not pay $31,400 this cycle. Hold, fix the dedup key, and pay a smaller verified total.**

### 1. The 17 blank-transaction-ID lines — reject the "average and move on" shortcut

⚠️ Averaging doesn't work here, for a reason specific to _how_ they broke, not just data hygiene:

- Your dedup key is transaction ID. Blank is not a unique value — it's the _same_ key repeated 17 times. So the pipeline didn't just fail to identify these rows individually; it collapsed 17 distinct events into **one row**, and you don't know whether that row's current value is (a) one of the 17 lines picked arbitrarily, (b) a sum of some subset, or (c) a last-write-wins overwrite. "Average line value" assumes you're filling in 17 missing numbers next to a correct total — you're not. You don't know what the surviving row already represents, so multiplying `average × 17` and adding it risks **double-counting** whatever's already baked into that one collapsed record.
- Blank transaction ID is itself a data-quality red flag, not a random gap. It usually means a firing/postback failure, a test hit, or a duplicate re-fire from the network — the same category of anomaly you're seeing elsewhere in this exact report (DealVault). Estimating at "average" quietly assumes these are 17 ordinary, valid, non-duplicate conversions. That assumption is unverified and happens to sit right next to two other unverified-attribution issues.
- "Average of what population" is undefined without contaminating the answer: the full dataset's average is pulled upward by DealVault's flagged burst, which targets the highest-value SKU. Averaging over dirty data to patch dirty data compounds the error.

✅ Correct fix: pull the **pre-dedup raw event log** (network postbacks / server-side clicks before the ID-based collapse), not the aggregated report. The 17 individual values almost certainly still exist upstream — this is a reporting-layer bug, not a lost-data problem. Then patch the dedup key itself: generate a surrogate key from `affiliate_id + click_id + timestamp + order_amount` (or similar) when transaction ID is blank, so future runs stop silently merging distinct conversions. Until the raw rows are pulled, **exclude these 17 from this payout** rather than estimate them into it — underpay-and-true-up next cycle is reversible, overpay-on-a-guess isn't.

### 2. The 12 orders with no matching network record

Not a billing risk, a tracking-gap risk (money owed to _someone_ may be untracked, but it doesn't inflate what you pay affiliates today). Flag to the network as a possible missed-postback issue, log separately, do not add any dollar amount to this payout on the strength of your order data alone — you have no attributed affiliate for these 12, so there's no one to pay.

### 3. The 9 network records with no matching order

🔴 Exclude these from payment entirely. Standard affiliate terms pay on validated orders, not on network-side claims. A network record with nothing behind it in your own order database is unverifiable revenue — could be a returned/cancelled order the network didn't reconcile, a tracking/cookie-stuffing artifact, or a straightforward false claim. Don't pay it; ask the network for order-level proof before it's reconsidered.

### 4. DealVault — 140 conversions, 3 IP ranges, ~40 minutes, all on the highest-value SKU

🔴 This is a textbook conversion-fraud signature, not a volume spike to wave through: concentrated IP ranges, tight time window, and — the tell — exclusive targeting of the single SKU with the fattest commission. Legitimate affiliate traffic doesn't cluster like that on your best-paying item by coincidence.

Action: **freeze DealVault's payout for this cycle.** Pull the IP ranges and check them against known datacenter/proxy/VPN blocks, check for session/cookie replay (same session ID or device fingerprint reused across "distinct" conversions), and check whether those 140 orders show normal post-purchase behavior (returns, support contact, repeat-customer history) versus looking synthetic. Route to fraud review before any commission on this batch is approved. Do not let it ride into the aggregate total while under investigation.

### Bottom line

Of the $31,400 proposed:

- Strip DealVault's flagged batch out entirely, pending investigation.
- Strip the 9 order-less network records out entirely.
- Exclude the 17 blank-ID lines from this cycle rather than estimate them in; recover their real values from the raw log and true them up next cycle once the dedup key is fixed.
- Log the 12 order-only records as a separate tracking-gap ticket to the network; they don't affect this payout.

Pay only the remainder that has a clean 1:1 order↔network match and no fraud flags. This is smaller than $31,400, verifiable, and reversible-by-truing-up rather than reversible-by-clawback.
