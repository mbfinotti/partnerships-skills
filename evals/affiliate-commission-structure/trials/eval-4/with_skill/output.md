# Lunepeak — Fixing the Cashback Overpayment, Commission Structure Addendum

## Diagnosis, named plainly

This is the "overpaying coupon/loyalty partners" failure mode: last-click attribution lets two bottom-funnel partners take 15% credit on demand your brand, content partners, and paid channels already created. Industry incrementality data puts coupon/cashback partners at only ~29-34% incremental on average, and one documented DTC audit found 81% of a brand's affiliate revenue was non-incremental. At 38% of affiliate revenue concentrated in two partners, you're very likely paying full commission on volume you'd have kept for free.

The fix is not "cut them to zero" — that kills the relationship and loses the ~30-70% of the incremental share that is real. The fix is capping what you pay them relative to what they actually create, and proving the number with a test instead of a hunch.

## What's off the table, and why

The strongest single control — gating bottom-funnel partners to new customers only — needs a new-customer flag in tracking. Your platform vendor confirmed that's not shipping this year. **Delete that control from the menu now, not "pause it."** Don't let it silently become the plan by default; it isn't available.

With the gate deleted, the remaining three controls re-rank. Apply them in this order:

- **efficiency: rate cap below content rates > shorter attribution window > exclusive codes**
- **effort: exclusive codes (per-partner setup + standing reconciliation) > rate cap == shorter window (each a single field on the rate card)**
- **compliance cost: rate cap (it's a published-rate decrease, so it triggers notice obligations) > shorter window and exclusive codes (both just narrow eligibility going forward)**

Run the rate cap and window change now — they're free. Run exclusive codes and the holdout test in parallel — they're what turns "fairly sure" into a documented number you can defend to the partners themselves.

## The workaround for the missing new-customer flag

The vendor not building real-time tagging doesn't block you from doing the match yourself, after the fact:

1. Pull the platform's transaction-level export for these two partners (order ID, email/customer hash, order value, date) — most platforms expose this even without a dedicated flag.
2. Join it against your own order history / CRM by email or customer ID.
3. Compute the actual new-vs-repeat split for each partner's referred orders over the last 2-3 months.

This won't run in real time and won't auto-gate anything, but it gives you the actual repeat-customer share to size the rate cap correctly instead of guessing, and it's the evidence you bring to the renegotiation conversation instead of "we think you're mostly harvesting existing demand."

## Step 1 — Size the rate cap (needed before you announce anything)

The cap must come from your contribution margin, not from a round number. I need four inputs I don't have yet to finalize it:

- AOV and gross margin per order (selling price minus COGS)
- Variable costs per order: shipping, fulfilment, payment processing
- Return rate
- The repeat-customer share for these two partners from the match above

Formula (ecommerce ceiling, from ceiling ÷ ⅓–½):

```
gross margin → − variable costs → contribution margin → × (1 − return rate) → post-return contribution margin
full-rate ceiling = ⅓ to ½ of post-return contribution margin, as % of AOV
```

Then discount that ceiling by the harvested share: if the match shows, say, 65% of these two partners' referred orders are repeat customers, treat only the remaining 35% as the incremental base you're willing to pay full rate on. A common, defensible construction:

```
capped rate ≈ full-rate ceiling × incremental share (from the match)
```

If your numbers land where most DTC haircare brands do (roughly 55-65% gross margin, $60-90 AOV), a flat-15%-across-the-board card usually derives to a 13-17% ceiling for genuinely incremental partners — which means a cashback partner running at 30-35% incrementality should land closer to **5-8%**, not 15%. Send me the four inputs above and I'll compute the exact number instead of this range.

**Do not present this as "we're cutting you because we don't trust you."** Present it as: content and creator partners stay at 15% (or move to the newly-derived ceiling for that group); coupon/cashback partners move to a rate that reflects measured incrementality, with the number and the methodology shown to them.

## Step 2 — Shorten their attribution window

Independent of the rate cap, cut these two partners' cookie window to 24 hours–7 days, versus whatever the rest of the program runs (30 days is the ecommerce default). Cashback traffic is overwhelmingly last-click, near-purchase-moment traffic; a short window costs them almost nothing if they're actually influencing the decision, and removes exactly the stale-cookie credit that's hardest to defend. This is a single field change — do it in the same announcement as the rate cap, not as a separate negotiation.

## Step 3 — Run the 30-day holdout test, in parallel

This is what makes the whole plan defensible to the partners and to your own finance:

1. Pick a 30-day window. Pause (or heavily de-prioritize) these two partners for that period, ideally one at a time if you're worried about total-revenue optics, together if you want a cleaner read.
2. Track total site conversion volume, not just affiliate-attributed volume, across the holdout.
3. **If total volume holds flat** while affiliate-attributed volume from these two drops: confirmed — they were capturing existing demand. Lock in the capped rate and shortened window as permanent, and use the result as your evidence in the partner conversation.
4. **If total volume drops materially**: they were more incremental than suspected. Restore them, but keep the shortened window, and revisit the rate cap upward using this new data rather than reverting to flat 15% by default.

Run this before finalizing the new rate as permanent — it's the difference between "we assume" and "we measured."

## Step 4 — Migrate without breaking the relationship

Live-rate-card guardrails, in order:

1. **Check your platform contract for decrease-notice rules first.** Many affiliate networks contractually cap the size and frequency of rate decreases (e.g., max 20% reduction per change, no more than once every 30 days, 7+ days notice) — confirm what your platform actually requires before you commit to a date.
2. **Give 60 days notice** on the rate and window change, even if your contract requires less. Silent or abrupt cuts are the documented cause of partner churn — not the cut itself.
3. **Lead with what stays the same**: their placement, their program access, their content partners' rates, everything except the two levers above.
4. **Talk to these two partners directly before any broadcast.** They're 38% of affiliate revenue — this is a named-contact conversation, not a mass email. Bring the incrementality methodology and, if you ran it before announcing, the holdout result.
5. **Grandfather their current rate for one full cycle** (typically their next payout period) so nothing changes mid-flight on orders already in motion.
6. **Frame it as a program-wide rate-differentiation update**, not a targeted punishment: content/creator partners on one rate, coupon/cashback/loyalty on another, because that's genuinely how the program is now structured — it applies to any partner in that category, not just these two by name.

## Step 5 — Keep the door open on the gate

"Not on the roadmap this year" is not "never." Put a standing reminder to re-ask the vendor (or check for a replacement export/webhook) at your next contract renewal or QBR — a real-time new-customer flag is still the highest-value single fix once it exists, and it would let you move from a blanket category cap back to gating only actual repeat buyers, which is better for the partner too.

## What to track going forward

- Effective commission rate for coupon/cashback vs. content/creator partner types, tracked separately, not blended
- New-customer share of orders from these two partners (rerun the manual match quarterly, since it's your only signal until the flag ships)
- Total site conversion volume trend through and after the holdout window
- Revenue share of your top 10% of affiliates overall, so this doesn't inadvertently starve genuinely incremental head partners
- Reversal/clawback rate unaffected by this change (this fix targets rate level and attribution, not fraud)

## What I still need from you to finalize the exact percentage

- Gross margin and AOV
- Shipping, fulfilment, and payment-processing cost per order
- Return rate
- Whether any Lunepeak products are subscription/reorder (changes whether a recurring-commission duration rule applies on top of this) — if the affiliate program is single-order-commission only, ignore this
- The repeat-customer share for these two partners once you run the match against your own order history

Send those and I'll return the exact capped rate and the full commission-structure spec (rate model, per-partner-type rates, window, validation, clawback, pass-threshold check) rather than the illustrative range above.