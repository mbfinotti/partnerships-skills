# Partner Onboarding Sequence — Sanity Check + Completed Plan

## Verdict on what you've got

**⚠️ Activation definition is under-specified — this is the biggest gap.**
"First referral within 30 days" doesn't say what counts as a referral (a name mentioned in an email? a deal registered in a CRM with a prospect + size?). With a $60k ACV and a 5-month cycle, a loose definition invites partners to pad activation with junk leads that never convert. Fix: define "referral" as a **deal registered in your portal/CRM with prospect name + estimated deal size**. Keep your 30-day window for that (it's a fast, low-friction ask, so 30 days is fine) — but add a second metric so you're not flying blind on revenue for 5 months (see KPIs below).

**❌ No never-activated branch.** You didn't mention one. Without it, the ~80%+ of partners who don't refer anyone in 30 days just go silent with no diagnosis, re-engagement, or cleanup.

**❌ No activation nudge.** A deadline-bound incentive inside the window is one of the highest-leverage pieces of a B2B sequence and it's missing.

**⚠️ 14 days is a skeleton, not the whole sequence.** Documented practitioner consensus is 4-6 touches over 10-14 days — that's your drip's shape, correctly. But your activation window is 30 days and your sales cycle is 5 months. A drip that stops at day 14 leaves days 15-30 uncovered (exactly where the nudge and never-activated entry belong) and leaves partners with zero contact for the ~4 months between "referral submitted" and "deal closed." That silence is where partners quietly disengage.

**⚠️ One archetype table, two very different partners.** Boutique consultancies and systems integrators shouldn't get the same tier. SIs typically carry outsized deal potential per partner; with only 2 of them and one AM who can do calls, high-touch for the SIs is cheap to staff and probably worth more than what it costs. Blanketing all 18 with the same treatment either overspends on the consultancies or underspends on the SIs.

**✅ What's right:** one AM with call capacity, 18/month, a written drip already in hand — none of this is being started from zero, and 18/month is comfortably within staffable range for a hybrid+high-touch split.

## Gaps I can't fill for you — answer these before finalizing

1. **Commission model, cookie/attribution window, payout threshold, hold period.** Not stated. These drive touch-1 money-mechanics copy and the nudge's bonus economics — that's the commission-structure skill's job, but I can't finish touch 1 without at least placeholders.
2. **Did the already-approved 18 receive the drip, or is it unsent?** If unsent, their intent is decaying right now — this is the single most time-sensitive item in this whole review.
3. **Tracking readiness**: is a referral submission actually recorded against the partner (CRM field, deal-reg tool with dedup), or is this still "email us a name"? If it's the latter, your 30-day activation number will be unreliable before it's even measured.
4. **Day-0 provisioning**: sandbox/demo access, comparison/buyer-FAQ material, terms + disclosure attestation, tax/payout collection — none of these were mentioned. Verify each has an owner and fires at approval, not on request.
5. **Target date for a first activation read.** Not given — I've assumed you want a read at the next cohort's 30-day mark.

## The Sequence Plan

```
SEQUENCE PLAN - [Data Catalog Partner Program], 2026-09
Activation       : primary = first referral (deal registered with prospect name +
                   est. deal size) within 30 days of approval
                   secondary (not pass/fail, but tracked) = referral progresses to
                   qualified opportunity within 90 days; closed-won tracked at
                   cohort level given ~5-month cycle
Routing          : boutique consultancies (~16) -> hybrid
                   systems integrators (2) -> high-touch
                   18/mo, 1 AM with call capacity => both tiers staffable;
                   revisit if approvals exceed ~100/mo (deletes high-touch)
Touches          :
  T1 Trigger : approval (within minutes)
     Channel : email  Sender : named AM (SIs) | automated, AM cc'd (consultancies)
     Action  : register your first deal (deal-reg link) / book your kickoff
               call (SIs)
     Content : approval confirmed; referral fee %, cookie/attribution window,
               payout threshold + hold period [pending commission-skill input];
               terms + disclosure attestation; under ~300 words
     Asset   : portal credentials, deal-registration link, sandbox/demo access
  T2 Trigger : day 2-3
     Channel : email  Sender : automated
     Action  : review the one-sheet and comparison/buyer-FAQ material
     Content : positioning, top objections, where the platform wins vs.
               incumbents
     Asset   : one-sheet, comparison sheet, sandbox walkthrough
  T3 Trigger : kickoff call booked (SIs, behavior) - else day 7 reminder |
               day 5-7 (consultancies)
     Channel : call (SIs) / email (consultancies)  Sender : named AM
     Action  : name the one account you'd refer first
     Content : SIs: targets, activation plan, promo-calendar slot, next-step
               owners. Consultancies: personal check-in, offer of co-pitch help
     Asset   : sales deck (SIs)
  T4 Trigger : day 14
     Channel : email  Sender : automated
     Action  : send the one-pager to that account (low-effort, ready-cut)
     Content : lowest-friction promo, pre-written intro email
     Asset   : swipe copy / intro-email template
  T5 Trigger : first referral submitted (behavior) - overrides calendar
     Channel : email  Sender : named AM
     Action  : none - celebrate; set expectations for the ~5-month cycle ahead
     Content : states what happens next (qualification, demo, close) and when
               the AM will check back in, so 4 months of silence isn't a surprise
  T6 Trigger : no referral by day 21 (behavior, half the window)
     Channel : email  Sender : named AM
     Action  : hit the bonus by day 30
     Content : deadline-bound activation bonus [economics pending commission
               skill]; reminder of deal-reg link
  T7 Trigger : day 30, only if not activated
     Channel : (none - enters never-activated branch)
Post-activation  : quarterly AM check-in per referred deal while it sits in the
nurture            5-month pipeline - not a classic onboarding touch, but without
                   it partners assume a submitted referral vanished
Activation nudge : deadline-bound bonus, expires day 30, carried by T6
Never-activated  : entry = no referral by day 30; diagnose never-activated vs.
                   dormant (was a referral submitted then went quiet - different
                   message); re-engagement at day 45 (new use-case angle + one
                   incentive); final notice at month 6 ("archived unless you
                   reply" - no threat framing); archive, don't delete
Exits            : exit calendar track on first referral (fire T5, hand to
                   nurture cadence); suppress calendar touches while an AM reply
                   thread is open; re-activated partners re-enter at T2, not T1
KPIs             : 30-day referral-activation rate (primary, per monthly cohort)
                   referral -> qualified-opportunity rate (leading revenue signal)
                   referral -> closed-won rate + time-to-close (cohort-level,
                   ~5-month lag - track, don't gate on it monthly)
                   never-activated share at day 30
                   per-touch open/click and call-booked rate (SIs)
```

## Measurement notes

- **Cohort, not blended.** Judge August's 18 only once their 30-day window closes; don't average across months yet.
- **Sample-size caution.** 18 partners means 3-4 activations either way swings the rate ~15-20 points. Don't read a trend off one cohort — wait for 2-3 months.
- **Benchmark context**, flagged as vendor/practitioner data, not audited: B2B programs are commonly cited at ~20% activation by 90 days; below that is treated as an onboarding-diagnostic trigger, not a hard failure. Your metric and window differ from that benchmark's shape (30-day referral vs. 90-day qualified opportunity), so use it as a rough sanity anchor, not a pass/fail line.
- **Don't optimize referral count in isolation.** Track the referral→qualified-opportunity rate alongside it, or the 30-day number can look healthy while the pipeline behind it is empty.

## Do these first, in order

1. **Confirm the 18 already-approved partners received (or haven't yet received) the drip.** If unsent, send now — intent decays fast and a month has already passed.
2. **Verify referral tracking is actually wired** (CRM field or deal-reg tool, tied to the partner). If it isn't, fix this before trusting any activation number.
3. **Split the routing**: pull the 2 SIs into high-touch with the AM now; leave the 16 consultancies on hybrid.
4. **Add the day-30 nudge and the never-activated branch** — both are currently absent and the first cohort's window is closing soon.
5. **Get commission/cookie/payout terms finalized** so T1 and the nudge can state real numbers instead of placeholders.
6. **Run every touch through a humanizer pass** before sending — template-scented copy is the fastest way to train professional partners to skim.
