# What to measure to settle the coupon-vs-content question

No standardized affiliate-dashboard framework exists for this — no standards body enforces these definitions, only vendor/trade-body guidance. What follows is the operative method, not a branded framework.

## The diagnosis, stated plainly

Last-click, 30-day-cookie attribution has one well-documented failure mode: **checkout-adjacent partners (coupon, cashback, browser extensions) sit at the last click and collect credit for demand another channel already created.** Content partners introduce a buyer weeks before purchase; a coupon site catches the same buyer at checkout and takes 100% of the credit under last-click rules. Your leaderboard isn't wrong — it's answering "who touched the sale last," not "who caused the sale." Those are different questions, and leadership is currently deciding budget on the first one.

Reference case worth citing internally: the Honey browser extension injected its own affiliate cookie at checkout, overriding creators' earlier attribution — PayPal defended it as "industry-standard last-click." Chrome's Web Store policy now bars that specific pattern (March 2025). It's the canonical illustration of exactly your setup: last-click without an incrementality check systematically over-rewards checkout-adjacent partners.

One more thing worth saying to leadership directly: **lift-test evidence suggests that when a checkout-adjacent partner is cut, the revenue usually redistributes to top-of-funnel content partners rather than disappearing.** Cutting a low-incrementality coupon partner rarely destroys the demand — it just gets credited correctly next time.

## What actually settles it: metrics, then a test

Metrics alone won't settle this — they build the case. Only a test gives you a number finance will accept. Do both, cheapest first.

### Step 1 — reframe the leaderboard (near-zero cost, spine-based, ship this month)

| Metric                                        | Formula                                                                                                                     | Decides                                                                            | Source                                   | Alert/Target                                                               |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------- | -------------------------------------------------------------------------- |
| **Checkout-adjacent revenue share**           | validated commission from coupon+cashback+extension partners / total validated program commission, monthly                  | Whether the repricing conversation is even warranted                               | Platform export (partner-type field)     | +10pt in a quarter → triggers incrementality review [DERIVE]               |
| **New-to-file rate, by partner type**         | orders from customers with no prior order in the customer file / orders credited to that partner type, order-level, monthly | 🎯 The single number leadership is missing                                         | Order DB, partner ID stamped at checkout | Own baseline [DERIVE] — no vendor target exists                            |
| **AOV, by partner type**                      | net order revenue (net of returns, excl. tax/shipping) / orders, monthly, sliced by type                                    | Which types are discount-driven low-margin vs premium buyers                       | Order DB                                 | Own baseline                                                               |
| **Net program contribution, by partner type** | attributed net revenue − (validated commission + network/agency/placement fees), by type, monthly                           | The actual profitability comparison leadership is trying to make                   | Order DB + billing                       | Positive and growing per type                                              |
| **Top-5-partner concentration**               | top-5 validated revenue / total program revenue, quarterly                                                                  | Whether "top six lines" is a concentration risk independent of the coupon question | Order DB                                 | >50% is the working risk threshold [VENDOR, re-band from your own history] |

New-to-file is the load-bearing row: **high new-to-file with a weak repeat rate signals discount-driven one-off buyers, not durable acquisition.** It's also only a proxy — it proves the customer wasn't already yours, never that the partner _caused_ the purchase. A coupon site intercepting someone already heading to checkout still scores as new-to-file. That's why Step 2 exists.

Before you trust the leaderboard's partner count at all: **confirm those "top six lines" are six distinct credited entities, not sub-network fragments of one or two networks.** Counting a sub-network's sites as separate partners distorts concentration and makes the coupon/cashback bloc look bigger and more diverse than it is.

### Step 2 — the test that actually settles it

Ranked by value-for-effort, four instruments exist (new-to-file screen → commission-reduction test → geo-lift → holdout). You've already got the screen from Step 1. The next cheapest instrument that still answers _your_ live question — reprice or not — is:

**Commission-reduction test.** Step the rate down 20–30% for your top 2–3 coupon/cashback partners for one full attribution cycle (at least 30 days, matching your cookie window, so the test doesn't get contaminated by pending conversions from the old rate). Hold content-partner rates flat as the comparison.

- Volume/revenue holds flat despite the cut → largely non-incremental, capturing demand that would have converted anyway. Reprice down with data behind it.
- Volume drops materially → they're driving real marginal behavior. The leaderboard rank is at least partly earned.

This is the **highest-compliance-cost** instrument on the list, because it unilaterally changes a partner's economics — check the notice and rate-change clauses in your affiliate terms before running it, and expect relationship friction with the partners you test on regardless of the result. Disclose the design internally as a real test, not a quiet rate change. If the result comes back ambiguous, or the budget at stake is large enough to justify it, climb to a geo-lift (pause the program in matched markets for a quarter) or a holdout (randomize 5–10% of traffic out of exposure) — both cost more but produce a defensible causal number.

Do **not** adopt a published affiliate ROI/ROAS benchmark (12:1 network average, CJ Affiliate's 46%/29%/88% lift figures) as your own bar — those come from vendors and networks with an incentive to inflate the channel, and the CJ figures are an observational test/control split, not a randomized holdout. They justify running your own test; they are never your program's number.

## How to route the result

The metrics and the test decide two different things — keep them separate when you report back:

- **Low incrementality on coupon/cashback → a repricing decision.** Cut their rate, don't necessarily cut the relationship.
- **Content partners' true contribution, once seen through new-to-file and AOV → a recruiting/budget decision**, made on their actual numbers instead of last-click rank.
- If you find evidence of cookie-stuffing or checkout-injection (not just legitimate last-click capture) — that's a separate fraud-rule conversation, not this one.

## Cadence

Add checkout-adjacent share and new-to-file-by-type to whatever monthly review already looks at the leaderboard — same meeting, reframed view. Run the commission-reduction test readout as a quarterly item; it needs a full cycle to read cleanly, and re-running it monthly would just add noise.

## Open items — confirm these before the numbers above are trustworthy

- ⚠️ **Partner-type tagging per partner** — needed for every row above. If the platform doesn't already classify partners as content/coupon/cashback/email/PPC/sub-network, that's the first fix, and it's normally cheap.
- ⚠️ **Partner ID stamped on the order at checkout**, not only inside the affiliate platform — required for new-to-file. If it's platform-only today, this is roughly a week of engineering, not a quarter, in a B2C order-database setup.
- **Validation/lock window and clawback policy** — not stated. Any period comparison is unreliable until you know how long reversals take to settle; don't compare a fresh month against a fully-validated one.
- **Program terms' rate-change and notice clauses** — check before running the commission-reduction test; this is a partnerships/legal read, not an analytics one.
- **Monthly commission spend and program age** — not given. If the effort budget is thin, do Step 1 only for now and park the test in the next cycle; if a lot of monthly spend rides on this decision, the test pays for itself immediately.
