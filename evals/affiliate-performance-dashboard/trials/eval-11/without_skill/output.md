Affiliate Dashboard — Metric Definitions

Context locked in below: B2C apparel, 30-day cookie window, last-click attribution, orders DB includes returns, revenue column includes tax and shipping.

## 0. Shared primitives (define once, reuse everywhere)

- **Click**: a click on an affiliate tracking link that successfully sets/reads the tracking cookie.
- **Attribution window**: 30 days from click timestamp to order timestamp, last-click model — if a customer clicks Affiliate A then Affiliate B within 30 days and then orders, Affiliate B gets 100% of the credit. Direct/organic visits between click and order do not reset or break attribution.
- **Order revenue (raw)**: the value stored in the orders `revenue` column — includes tax and shipping. **Do not use this raw column in any metric below without adjustment.**
- **Net merchandise revenue**: `revenue − tax − shipping`, computed per order. Since tax and shipping aren't split out as separate columns today, this requires either (a) new columns populated at order time, or (b) a documented estimation rule (e.g., flat shipping fee lookup by order date + tax = revenue × known regional tax rate). **Flag to engineering**: until revenue is decomposed, every $ metric below is an approximation and should carry an asterisk on the dashboard.
- **Returned order**: an order with a return record against it, regardless of return reason or partial/full status.
- **Net order**: an order excluding fully-returned orders. A partially-returned order stays classified as a net order, but its revenue is reduced by the returned line items' net merchandise value.
- **Reporting period**: unless stated otherwise, all rate/ratio metrics are computed over a fixed calendar period (day/week/month) using **order date**, not click date. An order counts in the period it was placed, even if the click happened in a prior period (within the 30-day window).
- **Affiliate spend**: total commission paid/accrued to affiliates for orders attributed in the period, computed on net merchandise revenue (commission should never be paid on tax, shipping, or returned line items — flag if current commission calc doesn't already exclude these).

## 1. ROAS (Return on Ad Spend)

**Formula**: `Net merchandise revenue from attributed orders in period ÷ Affiliate spend in period`

- Numerator uses **net orders only** (returns excluded) and **net merchandise revenue** (tax/shipping excluded).
- Denominator = affiliate spend as defined above, same period, same attribution logic.
- Both numerator and denominator are bucketed by **order date**, not payout date.
- Expressed as a ratio (e.g., 4.2), not a percentage.

## 2. ROI (Return on Investment)

**Formula**: `(Net merchandise revenue from attributed orders − Affiliate spend) ÷ Affiliate spend × 100`

- Same numerator/denominator basis as ROAS (net revenue, net orders, same period).
- Expressed as a percentage. ROI = (ROAS − 1) × 100 — keep both metrics consistent by construction; don't let them drift from separately-tweaked queries.
- Does not deduct platform/tech fees or affiliate network fees — this is *program* ROI, not fully-loaded program P&L. Note this distinction if finance asks for the latter.

## 3. AOV (Average Order Value)

**Formula**: `Net merchandise revenue from attributed orders in period ÷ Number of attributed net orders in period`

- Use **net orders** (returns excluded) — a returned order shouldn't count toward volume or revenue.
- Use **net merchandise revenue** (tax/shipping excluded) — otherwise AOV inflates with tax-rate mix and shipping-fee changes rather than actual basket size.
- One order = one unit in the denominator, regardless of item count.

## 4. Conversion Rate

**Formula**: `Number of attributed orders in period ÷ Number of clicks in period × 100`

- Numerator counts **gross orders at time of order** (before returns) — conversion rate measures whether a click became an order, not whether it stayed one. Returns are a separate, downstream metric (return rate), not a conversion-rate adjustment.
- Denominator = clicks, not unique clickers — one person clicking twice within the window and ordering once still divides by 2 clicks, not 1.
- Both numerator and denominator bucketed by the date of the underlying event (click date for denominator, order date for numerator) — this metric is inherently a cohort approximation, not a same-period ratio, because of the 30-day window. Document this on the dashboard so viewers don't expect numerator and denominator to reconcile day-by-day.

## 5. EPC (Earnings Per Click)

**Formula**: `Affiliate spend on attributed orders ÷ Number of clicks × 100`

- Standard industry convention: EPC is expressed as earnings per **100 clicks**, in dollars (e.g., "$4.50 EPC" means $4.50 earned per 100 clicks). State this convention explicitly on the dashboard to avoid a 100x misread.
- Numerator = affiliate spend (commission owed to the affiliate), not merchant revenue — EPC answers "what does this affiliate earn per click," a different question from ROAS/AOV.
- Use **gross attributed orders** for the spend calc unless your commission terms already deduct returns (most programs pay commission net of returns with a clawback window) — pick one and document it; recommend: EPC uses spend *after* return clawbacks, consistent with what actually gets paid.
- Same cohort-approximation caveat as conversion rate: clicks and resulting orders may span periods.

## 6. Active Affiliate Rate

**Formula**: `Number of active affiliates in period ÷ Number of total enrolled affiliates in period × 100`

- **Active** = generated at least one click OR at least one attributed order in the period (define which — recommend: at least one click, since "active" should mean "did something," not "succeeded"; track order-producing affiliates separately as a funnel stage).
- **Enrolled** = affiliates with an approved/active program status as of the last day of the period (excludes pending applications and terminated/banned affiliates).
- Period should match the reporting cadence used elsewhere on the dashboard (e.g., monthly) — an affiliate active on day 1 and inactive the rest of the month still counts as active for that month.

## 7. New-to-File (NTF) Rate

**Formula**: `Number of attributed orders from first-time customers in period ÷ Total attributed orders in period × 100`

- **First-time customer** = the customer has no prior order (any channel, not just affiliate) in the orders database before this order's timestamp. Uses lifetime order history, not a rolling window.
- Determined **per order**, not per customer-affiliate pair — if a customer's only prior order was through a different channel, this order is still NTF.
- Identity match is by customer account/email (or your canonical customer ID), not by device or cookie — guest checkouts with a matching email/phone to a prior order count as returning, not NTF.
- Gross orders (pre-return) in both numerator and denominator — NTF is a customer-acquisition signal at time of purchase, not a revenue-quality signal; a returned NTF order still proves the affiliate acquired a new customer.

---

## Open items to resolve before these are final

1. **Tax/shipping split**: nothing here is exact until revenue is decomposed. Recommend adding `tax_amount` and `shipping_amount` columns populated at order creation, backfilled via a documented estimation rule for historical orders.
2. **Commission basis**: confirm with finance/ops whether current commission calculations already exclude tax/shipping/returns — if not, ROAS/ROI/EPC denominators need a correction factor until the calc is fixed at the source.
3. **"Attributed order" edge case**: an order with items from multiple categories but one attribution — fine, last-click is order-level, not line-item-level. State this explicitly since apparel returns are often partial and per-SKU.
4. **Time zone**: pick one (store timezone vs. UTC) for date-bucketing every metric above and apply it uniformly — mismatches here are a classic source of "why don't our numbers match" disputes.