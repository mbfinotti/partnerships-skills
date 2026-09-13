# Affiliate Dashboard — Metric Definitions (B2C Apparel)

No canonical metric-definition standard exists for affiliate dashboards — these are written to be internally consistent and reproducible for _your_ program, not to match a vendor's glossary.

## Comparability contract (governs every metric below)

- **Source of truth:** orders database, reconciled to the affiliate platform for clicks/traffic.
- **Attribution:** last click, 30-day cookie.
- **Order state counted:** _validated_ = not returned/cancelled as of the report run date. A period is only comparable once its return window has fully elapsed for every order in it — don't compare a fresh period against a mature one.
- **Revenue field:** gross order value as stored, **minus returned line items**, and it **includes tax and shipping** because your schema can't separate them out. Every revenue-based metric below inherits this — treat all of them as tax-and-shipping-inclusive, and never compare them to an external benchmark (or a competitor's dashboard) that reports ex-tax/ex-shipping, without saying so.
- **Date basis:** order date for volume/revenue metrics; return-processing date for reversal-driven adjustments.
- **Timezone / currency:** not specified in the brief — pick one (store checkout timezone, settlement currency) and put it in the dashboard header. Every metric below is undefined until that's fixed.

## The 7 metrics

**ROAS** — Attributed order revenue for the period (last-click, 30-day cookie, validated orders, net of returns, inclusive of tax/shipping per the contract) ÷ affiliate cost of sale for the same order-date period (validated commission + network fees + agency fees + placement fees), shown as a ratio (e.g. "9.2:1"). There's no separate media-spend line in an affiliate program, so "cost" here _is_ cost of sale — state that substitution on the tile so nobody reads it as ad spend.

**ROI** — Two ROI formulas exist in circulation and disagree (revenue ÷ (cost+COGS), vs (revenue−cost) ÷ cost × 100). Reconciled definition to use here: **ROI = (Attributed order revenue − Total cost) ÷ Total cost × 100**, where Total cost = affiliate cost of sale (same as ROAS) + COGS of the goods in those orders (landed unit cost, not a revenue-derived estimate). Same period, order-date, validated-only rules as ROAS. This needs a per-order/per-SKU COGS feed — if merchandise cost isn't joinable to orders today, ROI can't be computed as specified; say so in Open items rather than faking it with a margin assumption.

**AOV** — Total validated order revenue (net of returns, inclusive of tax/shipping) ÷ count of validated orders, for the period, order-date basis. State "includes tax and shipping" directly on the tile — this is the one disagreement every published AOV source leaves unstated, and yours resolves toward the higher number. Unsliced, this metric decides nothing; slice by partner type before anyone acts on it.

**Conversion rate** (click-to-conversion) — Validated conversions (last-click, 30-day cookie) ÷ **unique** clicks in the same period × 100. Naming "unique" is the whole definition — raw vs. unique vs. bot-filtered clicks alone can move this number 2-6x between two people looking at "the same" export.

**EPC** — Validated commission paid on those conversions ÷ unique clicks in the same period, expressed in currency **per single click** (not per-100-clicks, not per-visitor — all three are used in the wild). State the click definition (unique, bot-filtered) next to the number every time it's shown, especially anywhere a partner sees it — they negotiate rates off this figure directly.

**Active-affiliate rate** — Affiliates with ≥1 validated conversion in the trailing 30 days ÷ total enrolled affiliates as of the same date × 100. The 30-day window is chosen to match your cookie window, not because it's the "correct" one — 30/60/90 all appear in published definitions with no consensus. Lock this window in writing before anyone is managed against the number.

**New-to-file rate** — Affiliate-attributed validated conversions where the customer (matched by email or customer ID) has **no prior order anywhere in full order history** ÷ total affiliate-attributed validated conversions in the period × 100. Two hard requirements: the affiliate/partner ID must already be stamped on the order at creation, and the match must check _all_ history, not just the reporting period. Known failure mode: a returning customer on a new device/email reads as new-to-file — that's an identity-resolution limit, not a formula error, and it's why this metric only ever _screens_ for incrementality, it never proves it (a coupon or cashback partner intercepting a shopper already headed to checkout scores as new-to-file too).

## Open items (things the brief didn't settle — don't let anyone assume these silently)

- **Timezone and currency** for the reporting day boundary: undecided. Fix before the first number is published; changing it later invalidates every historical comparison.
- **Validation/lock window length**: undecided. Tie it to your actual return-window policy (e.g., "no order counts as validated before day N") and put that number in the dashboard header, since AOV/ROAS/ROI/conversion rate all key off "validated."
- **Tax and shipping in the revenue column**: standing limitation, not a one-time caveat. Every dollar-based metric above is inflated relative to a merchandise-only figure. If the program will ever be benchmarked externally, this is worth a `tax_amount`/`shipping_amount` column split rather than a permanent asterisk.
- **COGS join for ROI**: assumed to exist at order or SKU level. If it doesn't, ROI as defined above can't be computed — don't substitute a blended margin guess; park it here until the feed exists.
- **Active-affiliate window (30 days) and EPC click convention (unique, per-click)**: both are conventions picked here to kill ambiguity, not derived from your data. Confirm both with whoever owns partner-facing reporting before they go live, since they directly change who counts as "active" and what a partner sees as their own EPC.
- **Last-click bias**: not asked about, but relevant given the attribution model — last-click ROAS/ROI systematically favor checkout-adjacent partners (coupon, cashback) over the partners who actually created the demand. New-to-file share by partner is the cheapest check against this; nothing above corrects for it on its own.
