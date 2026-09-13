No internal data on Ravencourt Outdoors exists in this repo outside `skill-wip/` (I didn't touch that path). This answer is general affiliate-program expertise applied to the numbers you gave me.

## 1. Capping the top affiliate (38% of validated revenue)

**First, classify the partner before picking a lever.** The right cap mechanism depends entirely on what type of affiliate this is:

- Coupon/deal site → usually last-click-steals-credit on sales that would've happened anyway. Cap hard.
- Cashback/loyalty/browser-extension → often intercepts _returning_ customers at checkout. Cap hard, or move to new-customer-only commission.
- Content/review/comparison publisher → often genuinely incremental (drives net-new demand). Cap gently, don't kill the relationship.
- One of your three sub-networks → different problem entirely (see §3). Don't cap the network row — you'd be capping hundreds of unrelated publishers via one blunt instrument.

**Before touching the rate, run an incrementality check.** Turn off tracking for a small traffic sample for 2-4 weeks and measure conversion without attribution. If most of that 38% converts anyway, the "cap" isn't really redistributing revenue to the rest of the base — it's recovering margin. Set expectations accordingly; don't promise the tail will magically absorb the freed volume.

**Mechanisms, not mutually exclusive:**

1. **Declining marginal rate** — full rate up to a revenue threshold, stepped-down rate above it. Caps blended payout without a cliff-edge cut.
2. **New-customer-only commission** — near-zero on returning customers. This is usually the single biggest lever for a concentrated top affiliate, since dominant partners over-index on customers who'd have bought anyway.
3. **Per-order commission cap** — flat $ ceiling per transaction, neutralizes basket-size inflation.
4. **Flat CPA instead of % of sale** — decouples payout from their growth, so scaling further doesn't scale your cost.
5. **Monthly payout ceiling** — most aggressive, most likely to trigger a walkaway; last resort.

**Sequencing:**

1. Check the affiliate agreement's rate-change clause and notice period — don't flip this unilaterally on a partner this size.
2. Model revenue-at-risk net of incrementality, not gross 38%.
3. Phase the cut over 1-2 cycles instead of overnight.
4. Have the retention conversation (segmented deal) before the blunt cap — you'd rather negotiate new-customer-only terms than lose the relationship.
5. Redeploy the freed margin deliberately: incentive tiers for rank 6-30, recruitment push into underrepresented affiliate types. A cap alone doesn't grow the tail — reallocation does.
6. Set an explicit concentration target (e.g., "no single affiliate >20% of validated revenue within 2 quarters") so this isn't a one-off fix.

## 2. Concentration tiles to build

- **Top-N share tiles** — Top-1, Top-5, Top-10, Top-20 share of validated revenue, each with trend vs. prior period. Your 38% / 61% are the seed values for the first two.
- **Pareto/cumulative-share curve** — affiliates ranked descending, cumulative % of revenue, with an 80/20 reference line. Shows the concentration shape at a glance, not just two numbers.
- **HHI tile** — single Herfindahl-Hirschman score (sum of squared shares) across all affiliates, tracked over time. One number that moves as concentration improves or worsens; gives you a threshold-based risk band instead of eyeballing percentages.
- **Revenue-at-risk tile** — $ of validated revenue sitting above your risk threshold (e.g., any affiliate >15%), not just %. Reads as business exposure, not a stat.
- **New-vs-returning mix per affiliate** — cross-cut concentration with customer quality. A top affiliate built on new-customer acquisition is a different risk than one built on returning-customer capture.
- **Effective payout rate by affiliate, ranked** — blended commission ÷ revenue per affiliate. Flags whether your top partner is also disproportionately expensive relative to peers, separate from the cap decision.
- **Concentration trend over time** — Top-1 / Top-5 / rest share, monthly, stacked or as a bump chart — proves whether the cap is actually working after you ship it.
- **Long-tail health tile** — count and revenue share of affiliates outside Top-20, tracked over time. The counter-metric: if you're redeploying budget to grow the tail, this is the tile that proves it happened.
- **Disaggregated vs. network-level concentration, side by side** — see §3. Build both; they answer different questions.

## 3. Splitting the three sub-networks — do it, but not for the reason you framed

"So the numbers look less scary" is the wrong test, and if that's the only reason, don't do it — it's a cosmetic edit to a risk report. The right test is: **does the network row conflate two different kinds of risk that need different responses?** It does, so split — for analysis, not for the dashboard cop-out.

- A single affiliate at 20% share and a sub-network at 20% share are not the same risk even though the row looks identical. One publisher can walk overnight and take 20% with them. A network's 20% is spread over hundreds of independent publishers — any one of them leaving barely moves the number. Averaging them into one concentration metric is an apples-to-oranges error, not just an optics problem.
- Disaggregating will very likely _shrink_ your apparent concentration, because network rows currently overstate single-point-of-failure risk. That's a legitimate, non-cosmetic reason to split.
- But disaggregating can also _reveal_ a risk you're currently blind to: if one publisher inside a sub-network drives most of that network's volume, your true #1 by traffic dependency might not be the affiliate you think it is today. You can't know until you look.
- **Action:** pull sub-ID/sub-publisher-level reporting from each network (Impact, CJ, Awin, Rakuten, ShareASale, Partnerize all support this — ask your account manager if it's not already surfaced). If a network can't or won't give you that breakdown, treat that opacity itself as a risk finding — you don't actually control or understand a third of your program.
- **Keep two views, don't merge them:**
  - _Commercial/contract view_ — network as one row. This is who you negotiate rates and payment terms with.
  - _Concentration/risk view_ — always disaggregated to true publisher level. This is the one that should feed every tile in §2, including the cap decision in §1. Don't build your concentration tiles on the commercial view — it will consistently understate real dependency risk on any single blockbuster publisher hiding inside a network.
