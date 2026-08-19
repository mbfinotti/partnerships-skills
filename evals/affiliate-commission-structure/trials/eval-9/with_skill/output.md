## Verdict on 35%: it fails the pass threshold — don't ship it

Derived from Sablefin's own numbers, not from what competitors advertise:

```
Revenue LTV       = $199 × 20 months                    = $3,980
Gross-profit LTV  = $3,980 × 79%                         = $3,144.20
SaaS ceiling      = 5-15% of revenue LTV, never >30-40% of gross-profit LTV
                  = $199-$597 (LTV leg) / up to $943-$1,258 (margin leg)
Blended CAC       = $740
```

| Structure | Total paid/customer (12-mo cap) | % of revenue LTV | % of gross-profit LTV | vs $740 CAC |
|---|---|---|---|---|
| **Current: 20% × 12mo** | $477.60 | 12.0% | 15.2% | 64.5% |
| **Proposed: 35% × 12mo** | $835.80 | **21.0% — fails 15% ceiling** | 26.6% (passes alone) | **113% — exceeds CAC before any incrementality discount** |

35% fails on two legs at once: it blows the LTV ceiling by 40%, and it costs more than the full blended CAC per customer *before* discounting for non-incremental affiliates (coupon/cashback-style partners capture credit on demand others already created — the real cost per *incremental* customer only goes up from $835.80, never down). The fact that it clears the gross-margin leg alone doesn't save it; the gate needs both legs to hold, and it doesn't. This is the exact "match the market" trap — a rate copied from a competitor's headline instead of derived from your own contribution economics, and the kind of move that reads fine on launch day and shows up as a loss only once it's been running a quarter.

## The real problem isn't the rate

412 approved affiliates, 11 converted last quarter, revenue flat for three straight quarters. That's a 2.7% activation rate. Raising the headline rate makes the 11 producers marginally happier — it does nothing for the other 401, who aren't inactive because the commission is too low, they're inactive because they were never activated. A rate change layered on top of an activation problem will not move the flat-revenue line; it will just make the flat revenue you do get more expensive. Fix activation (onboarding, content/co-marketing support, direct outreach) as a separate track — this is outside a commission-structure fix and shouldn't be sold internally as if a rate bump solves it.

## Recommended structure

```
COMMISSION STRUCTURE - Sablefin, 2026-09-12
Rate model        : recurring revenue share - retention-aligned, matches current model
Headline rates    : 30% months 1-6, 18% months 7-12, capped at 12 months
                    - front-loaded taper lets the public headline say "30%,"
                      matching competitors' advertised number, while the back-half
                      step funds it inside the ceiling (same lever as the standard
                      SaaS worked case: same headline, taper beats a flat cut)
Tiers             : flat - only 11 affiliates have any conversion history; not enough
                      data to place a breakpoint. Revisit once a full quarter of
                      post-relaunch data exists.
                    Immediate exception: private milestone bonus for the current 11
                      active producers (5-10% of new-customer revenue on top of base,
                      paid only on that outcome) - rewards the concentration you
                      already have without moving the public headline for 401
                      affiliates who haven't earned a cent yet
Recurring duration: 12-month cap, unchanged from today - margin (79%) and tenure (20mo)
                      would tolerate longer, but 3 flat quarters is too little signal
                      to extend liability before proving the new rate moves volume
Attribution       : proposed 90-day cookie (B2B SaaS default for a monthly-price point
                      this size) - CONFIRM against current tracking config, not
                      provided in the brief
Validation        : 30-45 day lock = trial-to-paid + refund window - CONFIRM trial
                      length and refund policy, not provided in the brief
Payment           : net-30, $50 minimum threshold, clawback on refund/chargeback/
                      cancellation-in-window, negative balance carried forward
                      (unchanged - no reason given to touch payment terms)
Economics         : total commission/customer = (30%×$199×6) + (18%×$199×6) = $573.12
                    = 14.4% of revenue LTV (inside 5-15% band, with headroom)
                    = 18.2% of gross-profit LTV (inside 30-40% band)
                    = 77.5% of blended CAC, before incrementality discount -> PASS
                    effective blended rate over 12 months: 24.0%
                    headroom to the hard LTV ceiling: ~$24/customer (the absolute max
                      a flat 12-month-cap rate can sustain here is 25.0%, i.e. $597)
Validation plan   : 30-day holdout on your top 3 of the 11 active producers post-launch
                      - if their volume holds and nobody else picks up the slack, the
                      program's problem is activation, confirmed, not rate
KPIs              : cost per incremental affiliate customer vs $740 CAC; effective
                      commission rate; share of the 412 who convert at least once
                      (the number that actually needs to move); revenue share of the
                      current top 10 producers
```

**If your affiliate platform can't express a two-step taper**, use the flat equivalent instead: **24% recurring, capped at 12 months** — identical $573.12 cost, same 14.4%/18.2% ratios, just without the "30%" headline number to put in marketing copy. Everything else in the spec is unchanged.

**What this doesn't do:** it doesn't hit 35%, and it doesn't let you claim a number higher than competitors'. It ties their advertised 30% on the number affiliates actually see up front, at a cost Sablefin can sustain per customer. Going to 35% to "leapfrog" is a headline move with no economic floor under it — recommend against it regardless of what competitors publish.

## Migration plan

1. **60 days' notice** before the new rate takes effect — do not change it silently.
2. **Lead with what stays the same**: still a recurring revenue-share model, still a 12-month cap, still net-30/$50 threshold/clawback terms unchanged.
3. **Phase communication top-producers-first**: reach out directly to the 11 affiliates who converted last quarter before the broadcast email — for every one of them, the new structure pays strictly more than today's flat 20% ($573.12 vs $477.60 over 12 months), so this is an easy conversation, not a defensive one.
4. **No grandfathering needed on economics** — the new rate beats the old rate for every existing affiliate. Grandfather only if any partner has a *custom* rate above 30% already negotiated; none indicated in the brief.
5. **Broadcast to the full 412** after the top-producer calls, paired with the activation push — this is also the moment to re-engage the 401 who've never converted, since a rate announcement is a legitimate reason to re-open contact with a dormant partner base.

## Announcement (affiliate-facing)

---

**Subject: Your Sablefin commission is going up — here's what's changing**

Hi [Partner Name],

Starting [date, 60 days out], we're increasing the Sablefin affiliate commission:

- **30% recurring commission for the first 6 months** of every customer you refer
- **18% recurring for months 7-12**
- Still capped at 12 months, still paid monthly, still net-30 with a $50 minimum payout

Everything else about the program stays the same: same 12-month structure, same payment terms, same tracking link and dashboard.

For a typical Sablefin customer, this pays out more in total than today's flat 20% rate — the new structure front-loads the payout so you see more, sooner, on every new customer.

If you're one of our active partners, someone from our team will reach out directly this week to walk through what this means for your account. If you haven't sent a referral our way yet, now's a good time to start — [refreshed partner resources / onboarding link].

Questions, reply directly to this email.

[Signature]

---

**One open item before this goes final**: cookie window and validation-lock length weren't in the brief and are marked "proposed" above — confirm those against what Sablefin's tracking actually supports before publishing terms, since a published window becomes a contractual commitment the moment affiliates start relying on it.