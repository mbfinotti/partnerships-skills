## Reframe before the build

The plan you described — copy the marketing drip, build the portal, build the self-serve asset library — is the standard shape for a _high-volume, low-value_ intake (hundreds of signups a month, most worth little individually). Your program is the opposite profile: **14 partners today, ~1-2 landing per quarter, each worth $200k+ in year-one value, and a partner manager sitting on open calendar time.**

That combination inverts the usual ranking. Normally self-serve automation wins because its build cost amortizes across volume. At your volume, a week spent building a drip/portal/asset library never pays back — you'd be routing a $200k relationship through the same templated emails as a $40 affiliate, while the person who could actually work the relationship sits idle. High-touch wins here on _both_ activation rate _and_ efficiency, not just activation rate.

**Recommendation: make the partner manager the engine, not the email sequence.** Every one of the 14 (and the ~6/year after) gets a personal onboarding track run by the AM. Build only the thin support layer underneath it — no bespoke portal, no marketing-grade asset library.

## Confirm before launch (open items)

I've drafted the plan below on these assumptions — flag any that are wrong:

1. **Activation event**: I used _first qualified opportunity registered_ (a named prospect + estimated value) as the tracked activation, with _first closed-won deal_ tracked separately as the real revenue KPI. Enterprise clinical-trial procurement cycles run long, so gating "activation" on closed revenue would leave the sequence unable to report anything for most of a year.
2. **Window**: 120 days (vs. the 90-day B2B default) — a guess to account for CRO/consultancy sales cycles. Tell me the real median if you have one.
3. **Commission/referral model**: unspecified (referral fee, reseller margin, co-sell). This determines whether touch 1 needs tax/payout collection at all, or just a signed partner agreement. I've placeholder-flagged this — routing it to a commission-structure design is out of this skill's scope.
4. **Partner relationship type**: I assumed a mix of pure referral (CRO recommends Reyvant) and implementation/co-sell (consultancy delivers it) — both route to high-touch, but the kickoff content differs slightly. Confirm the actual split across your 14.
5. **The 3 added this quarter**: presumably onboarded informally already. I'd run the kickoff-call track retroactively for them rather than exempting them — treat "already a partner" as day-0, not as already activated.

## SEQUENCE PLAN — Reyvant Partner Program, 2026-09

```
Activation       : first qualified opportunity registered within 120 days of signed
                   partner agreement; first closed-won deal tracked separately,
                   uncapped window, as the real revenue KPI
Routing          : all 14 current + ~6/yr expected -> high-touch (100%).
                   Volume (~1-2 landed/quarter) makes the self-serve build cost
                   never pay back; AM has open capacity to cover 100% personally.
                   No hybrid/self-serve tier - a tier nobody needs to be routed
                   away from personal attention isn't a tier, it's a downgrade.
Touches          :
  T1 Trigger : partner agreement signed (within 1 business day)
     Channel : email + calendar invite   Sender : named partner manager
     Action  : book the 45-min kickoff call
     Content : agreement recap, deal-registration process and protection window,
               [commission/margin terms - pending model confirmation], what
               happens between now and the call
     Asset   : resource-hub link, signed agreement copy, deal-reg link
     Why     : a signed agreement with no concrete next step is the "approval
               as finish line" failure - the call booking is the one action

  T2 Trigger : kickoff call held (target day 3-7; AM chases if unbooked by day 5)
     Channel : call   Sender : partner manager
     Action  : agree the activation plan - name the first 1-3 target accounts,
               who owns outreach, target dates
     Content : product/sandbox walkthrough, use-case and buyer-question
               material for clinical-ops stakeholders (CRA, clinical ops
               director, sponsor procurement), competitive positioning
     Asset   : sandbox/demo environment, sales deck, comparison one-sheet
     Why     : "don't sign and let it sit" - the concrete plan with named
               owners is what practitioner-cited programs credit for activation

  T3 Trigger : day 10, if no opportunity registered yet (calendar)
     Channel : email   Sender : partner manager
     Action  : register your first opportunity, even early-stage
     Content : deal-reg link + protection window restated; low-friction framing
     Asset   : deal-registration portal link

  T4 Trigger : first opportunity registered (behavior - overrides T3/T5)
     Channel : email   Sender : partner manager
     Action  : none - celebrate
     Content : confirm the registration and protection window, what Reyvant's
               sales-engineering side does next, realistic timeline for
               enterprise clinical-trial procurement

  T5 Trigger : no opportunity registered by day 60 (behavior; half the window)
     Channel : call   Sender : partner manager
     Action  : which account would you pitch first, what's blocking you
     Content : personal check-in, offer a joint call with the partner's
               prospect, refresh use-case angles
     Why     : email-only at this stage under-serves a $200k relationship -
               calendar time exists, so spend it here rather than on a template

  T6 Trigger : day 100, only if still not registered
     Channel : call + email   Sender : partner manager
     Action  : register a qualified opportunity by day 120
     Content : time-boxed ramp incentive, framed as a finish line, never as a
               condition of staying in the program [incentive economics -
               pending commission-model confirmation]

  T7 Trigger : first closed-won deal (behavior; may land well past day 120)
     Channel : call + email   Sender : partner manager (+ a founder/exec note,
               given deal size)
     Action  : none - celebrate; confirm commission/margin payment mechanics
     Content : ask for a reference/case-study conversation; discuss the next
               target account together
     Why     : this is the real revenue event - it gets more ceremony than a
               $50 affiliate bonus would, deliberately

Activation nudge : ramp incentive at T6, expires day 120 [rate pending
                   commission-skill design]
Never-activated  : entry = no opportunity registered by day 120. Given ~1-2
                   partners a quarter, every never-activated partner is a named
                   case, not a cohort - handled personally throughout:
                     - Day 150: one re-engagement call - new use-case angle,
                       ask what changed since signing
                     - Month 9-12: one final-notice email/call framed as a
                       relationship check-in, never a threat
                     - Then: mark dormant in CRM, keep the relationship warm -
                       CRO/consultancy circles are small; a dormant partner can
                       still refer or re-activate later
Exits            : on activation -> hand off to standing account-management
                   cadence, not back into this sequence
                   on never-activated entry -> branch rules above take over
                   suppression -> pause calendar touches while an active call/
                   email thread with the AM is open
KPIs             : per-partner: opportunity registered? (Y/N + date), time-to-
                   first-opportunity, time-to-first-close, deal value
                   reviewed monthly by the AM as a named list, not a dashboard
                   percentage (see caveat below)
```

## What to build (day-0, minimal)

- **Signed partner agreement + deal-registration mechanism** in your CRM — this blocks T1 and can't be deferred.
- **A lightweight resource page** (a shared drive folder or one Notion/portal page is enough — a day of work, not a project): sandbox access instructions, sales deck, comparison one-sheet, deal-reg link, FAQ. This is reference material the AM points to on calls, not a self-serve activation engine.
- **Sandbox/demo environment access**, provisioned per partner, not built as a generic self-serve signup flow.
- **Tax/payout collection** — only if the model is referral-fee-based. If it's a reseller-margin model, this step doesn't apply; confirm which.

Skip: a custom partner portal, a multi-touch marketing-automation drip, banner/creative libraries, and anything else built for placement volume you don't have. If you later scale past ~30-40 active partners and the AM's calendar stops covering everyone, that's the trigger to revisit self-serve — not before.

## KPI caveat — read before reporting a number

The usual pass gates (≥20% B2B activation at 90 days, per TrackRev/U4IA vendor data) are built for cohorts of dozens or hundreds. At n=14 growing to ~20, one partner is 5-7 percentage points — "activation rate" will swing from 0% to 33% based on a single deal landing. Report **absolute counts and named status** (which partners have a registered opportunity, which don't, and why) in the AM's monthly review instead of a percentage; treat the vendor gate as background context, not a bar to hit.
