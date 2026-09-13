## Affiliate fraud detection rules — pre-Thursday payout + ongoing

First, some context on that stat: the 17%/$3.4B figures come from cross-industry reports that are heavily weighted by mobile in-app and incentivized-install traffic. For a DTC brand on last-click/30-day-cookie, your actual exposure concentrates in a narrower set of vectors — mainly **cookie/coupon fraud**, not bot armies. Last-click + long cookie window is specifically the attribution model that fraud is easiest to exploit, so that's where to point detection first.

### Run these now, against Thursday's batch (orders that hit day-14 and are queued for payout)

1. **Time-to-conversion outliers**
   - Flag: conversion within <5 seconds of click, or click-to-order gap of exactly 0–2 minutes at unusual volume for that affiliate.
   - Why: signature of cookie-stuffing (cookie dropped via hidden pixel/iframe, no real visit occurred).

2. **Last-click override / coupon-code injection**
   - Flag: sessions where a coupon-site or browser-extension affiliate's click lands in the _final seconds_ before checkout, especially after an earlier click from a different (often content/organic) affiliate or no-affiliate session existed in the same 30-day window.
   - Why: this is the #1 real-money leak in last-click programs — extensions (Honey-style) and coupon aggregators hijack the sale at checkout, stealing credit from whoever actually drove the customer.
   - Rule: `last_click_affiliate != first_meaningful_touch AND last_click_type IN ('coupon_site','extension') AND time_to_checkout < 60s` → hold for manual review, don't auto-pay.

3. **Click-to-conversion ratio outliers**
   - Baseline your network's median CTR→CVR. Flag any affiliate converting >3x the network median for two consecutive weeks.
   - Especially suspicious combined with #1.

4. **Self-referral / friends-and-family**
   - Flag: order billing/shipping name, email domain, or payment method matches the affiliate's own registered account details (name, email, IBAN/PayPal on file).
   - Flag: same customer email appearing as a "new customer" conversion for the same affiliate more than once in 90 days (classic buy-to-earn-commission loop).

5. **Refund/chargeback reconciliation before payout**
   - You approve+pay at day 14 — pull refund/chargeback status _at time of batch run_, not at order date. Any order refunded or charged back between order date and day 14 gets pulled from the batch, not clawed back later.
   - Track a rolling refund-rate-per-affiliate metric; refund rate >2x network average is a fraud/quality signal even for orders that haven't been refunded yet.

6. **Geo mismatch**
   - Flag: click IP geolocation materially different from order shipping/billing country/region, especially recurring for one affiliate.

7. **New-affiliate volume spike**
   - Flag: any affiliate <30 days old suddenly producing >2 std dev above the median new-affiliate volume. Legit affiliates ramp; fraud rings front-load.

8. **IP/device/account clustering**
   - Flag: multiple "distinct" affiliates sharing IP ranges, device fingerprints, payout destinations (same PayPal/bank), or registration patterns (email pattern, signup time clustering). Sub-account fraud rings are common at 340-affiliate scale.

### Structural fix (bigger than Thursday, but cheap and high-leverage)

Your last-click model is the actual root cause of most of #2 and #5. Two options, ranked by effort:

- **Cheap now**: exclude coupon-site/extension affiliate types from last-click override — give credit to the touch that occurred _before_ the coupon click if one exists within the session/cookie window. Most affiliate platforms (Impact, Everflow, Tapfiliate, PartnerStack) support this as a rule-based override without a full attribution rebuild.
- **Bigger**: move to a hybrid model (first-click for discovery-type affiliates, last-click for closers) once you have volume to justify it.

### Ongoing detection cadence (not just payout day)

- Run rules 1–3 and 6–8 **daily**, not at payout time — catching fraud at click/conversion time lets you void before the 14-day hold even completes, rather than after you've already promised payment.
- Run rules 4–5 **at every payout batch**, since refund/chargeback and self-referral patterns only fully resolve near the day-14 mark.
- Weekly: review affiliate-level CVR and refund-rate dashboards for drift, not just absolute thresholds — fraud rings adapt to fixed thresholds fast.

### For Thursday specifically

Given you likely don't have all of this instrumented yet, minimum viable triage before you approve the batch:

1. Pull refund/chargeback status fresh (rule 5) — non-negotiable, protects real cash.
2. Run the time-to-conversion query (rule 1) — cheapest, highest signal-to-noise, catches the most damaging fraud type.
3. Spot-check top 10 affiliates by commission $ in this batch for self-referral (rule 4) and CVR outliers (rule 3) — at $58K/month, your top decile of affiliates likely represents the majority of dollars at risk.
4. Anything flagged: hold from this run, don't claw back later — pay next cycle once cleared.
