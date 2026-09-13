# Cutting cashback-site overpayment without a customer-tagging feature

## The core problem

Flat 15% commission pays cashback sites the same rate whether they originated a customer or just intercepted one already mid-checkout. Since the platform vendor won't build new-vs-repeat tagging this year, the fix has to work with data and levers you already control: cookie windows, commission tiers, and your own attribution — not theirs.

## 1. Get your own evidence first (before touching payouts)

Don't renegotiate on a hunch — build the case:

- **Pull last-click vs. assisted-conversion data from your own analytics** (GA4/PostHog, whichever you run) for the two cashback domains. Compare session paths: did the user land via a paid/organic/direct channel first, then a cashback link appeared only at checkout? A short time-gap between "cashback click" and "order" (minutes) with prior on-site history is the signature of coupon/cashback extension interception, not genuine acquisition.
- **Check coupon-extension interception specifically.** Cashback sites are frequently triggered by browser extensions (Honey-style) that fire at checkout regardless of whether the shopper ever visited the cashback site intentionally. Look at whether the affiliate click timestamp is seconds before order completion — that's extension interception, not discovery.
- **Cohort overlap**: cross-reference cashback-attributed order emails against your existing customer list (newsletter subscribers, past orders, logged-in accounts). If a large share were already known to you, that's your smoking gun for the vendor conversation and any public justification.
- Quantify: what % of the 38% would you estimate is "would have bought anyway"? Even a rough range (e.g., "60-80% based on repeat-customer overlap") is enough to size the fix.

## 2. Structural fix: split new-customer vs. existing-customer commission — enforced on your side, not theirs

Since the platform can't tag this, do it in your own checkout/order system instead of relying on the affiliate network:

- At order time, your backend already knows if the email/account is new or existing (first order vs. repeat). Compute this yourself, independent of the affiliate platform.
- **Change commission structure to two tiers**: e.g., 15% on new-customer orders, a much lower flat rate (e.g., 3-5%, or a small flat fee) on repeat-customer orders. This is a program-wide rule change, not something you can apply only to two partners — same rule applies to all affiliates, which keeps it defensible and non-discriminatory.
- Push the corrected commission amount via **manual adjustment / commission override** in the platform (most affiliate platforms, even basic ones, allow post-hoc commission editing or a manual payout adjustment queue) rather than waiting for a tagging feature. This is more manual work per payout cycle, but it's available today regardless of the vendor's roadmap.
- Alternative if manual override is too heavy: **lower everyone's base rate** (e.g., 15% → 8%) and add a **new-customer bonus** (e.g., +10% only on first-time orders) on top. Net effect for genuine new-customer acquisition stays rewarding; cashback sites skimming repeat buyers get paid the lower base rate. This reshapes the incentive without singling anyone out and doesn't require identifying "new vs repeat" per click — only per order, which you control.

## 3. Cookie window and last-click tightening

- **Shorten the attribution/cookie window** (e.g., from 30 days to 3-7 days). This reduces the ability of a cashback site to claim credit for a sale that started elsewhere weeks earlier.
- Consider **first-click or position-based attribution** instead of last-click, if your platform supports it — this alone can gut cashback-site "credit theft," since cashback links are almost always the last click, not the first.
- **Exclude coupon/cashback code injection at final checkout step** if technically feasible (i.e., don't allow an affiliate cookie set in the final 60 seconds before order confirmation to override an earlier-session affiliate cookie). This is the single highest-leverage technical fix against browser-extension-triggered cashback attribution, and doesn't require the vendor's roadmap item at all — it's an attribution-logic setting, not a customer-identity feature.

## 4. Negotiate directly with the two cashback sites — reframe, don't just cut

Cutting them cold risks losing whatever genuine incremental volume they do bring, and they're large enough that an abrupt cut looks adversarial. Instead:

- Bring them your own new-vs-repeat overlap data (from step 1) and propose a **restructured deal**: lower base rate + new-customer bonus, same as the program-wide change in step 2 — so it isn't "we're singling you out," it's "the whole program moved to this model."
- Offer a **minimum-spend floor or flat monthly retainer** in exchange for accepting the lower rate, if they're valuable enough to want to keep predictable. This preserves the relationship while decoupling your cost from repeat-buyer leakage.
- Ask them directly whether they can restrict placement to **new-visitor targeting only** (many cashback platforms can suppress showing your offer to users with existing account cookies/session history on your domain, if you share a suppression pixel/list). This costs them little and directly fixes the leakage without lowering their headline rate.

## 5. Sequencing and safeguards

1. **Week 1-2**: Pull attribution/overlap data (step 1). Get a real number, not a guess.
2. **Week 2-3**: Implement cookie-window shortening and last-click/final-step attribution guard (step 3) — pure config change, no negotiation needed, do this regardless of what else happens.
3. **Week 3-4**: Roll out the new/repeat commission tiering as a program-wide policy change (step 2), announced to all affiliates with reasonable notice (e.g., 30 days), not just the two cashback sites.
4. **Week 4+**: Have the direct conversation with the two cashback sites, backed by data, offering the restructured/negotiated deal (step 4) before the new terms take effect for them.
5. **Monitor**: Track total affiliate revenue and cashback-site share monthly after the change. If their share of revenue drops roughly proportional to the new/repeat mix you estimated, the fix is working; if it collapses far more (they stop sending any traffic at all), that tells you they were more incremental than your data suggested — revisit the new-customer bonus rate upward if needed.

## What NOT to do

- Don't quietly cap or blocklist just the two sites without changing program terms — this breaches the spirit of a flat-rate program and, if discovered, damages trust with your entire affiliate base, not just these two.
- Don't wait on the vendor's roadmap — every lever above (cookie window, attribution model, order-level new/repeat tiering, direct negotiation) is available today without their tagging feature.
