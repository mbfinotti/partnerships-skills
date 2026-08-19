## Before the build: two flags on the brief

**⚠️ The "60/40 Principle" — not using it.** I checked the sourced framework list for affiliate onboarding: it "appears in one vendor guide with no named originator or citation. Unverified; do not use." No practitioner, platform, or study backs it — it's un-traceable marketing-guide filler, not a method. I'm not building any part of this sequence around it. If your boss wants a similar three/four-part mnemonic for structuring the copy, two *are* real and sourced: Prussakov's **3 Es** (Excite, Encourage, Equip) or **RITS** (Resources, Incentives, Tools, Support) — both single-author practitioner coinages, not industry standards, but at least attributable. Happy to swap one in if useful.

**⚠️ AIDA — real framework, wrong layer if forced onto the whole sequence.** AIDA/RACE/AARRR are general marketing funnels never built for affiliate activation, and force-fitting one as the sequence's *architecture* (i.e., "Touch 1 = Attention, Touch 2 = Interest...") would throw away the one thing that actually drives activation in this channel: behavior triggers (first click, first sale, no-click-by-day-N) overriding a fixed calendar. A rigid 4-stage funnel can't react to "they clicked but didn't buy."

What I did instead, to still give you AIDA consistency with the rest of your marketing: **I used AIDA as the copy structure inside every individual email** (each touch opens with Attention, builds Interest specific to the affiliate's content/coupon channel, states Desire via the money mechanics or bonus, closes with one Action). The *sequence timing and branching* stays on the evidence-based trigger model — that's the part actually responsible for activation rate. I've labeled the AIDA beats inline in each draft below so it's auditable against your boss's brief.

---

## Assumptions (confirm before send — I didn't have these)

| Item | Assumed | Why |
|---|---|---|
| Activation event | First tracked sale, within 30 days of approval | Given |
| Cookie window | 60 days | Given — **note this is separate from the 30-day activation window**: cookie window governs how long a click stays credited to the affiliate; activation window governs how long the onboarding sequence runs before branching to never-activated. Don't merge these two numbers in copy. |
| Commission | 8% one-time, per sale | Typical for outdoor hardgoods (lower margin than DTC skincare/apparel) — **replace with your real rate** |
| Payout threshold / hold | $50 / net-30 | Standard default; confirm your actual terms |
| Archetypes in intake | Coupon-deal, content/review site only | Per your brief |
| AM capacity | None mentioned → **self-serve tier for both archetypes** | If you do have manager hours, content sites are the archetype worth promoting to hybrid (add one personal check-in at the T3 slot) — coupon sites rarely repay the check-in |
| Volume | Unstated | Doesn't change routing here since there's no AM tier in play |
| Tracking | Assumed server-side/postback is live | **Verify this before launch** — if it isn't, activation numbers will understate reality and you'll misdiagnose a working sequence as broken |

---

## Day-0 provisioning (must be true before Touch 1 sends — this is a pre-condition, not a sequence step)

- [ ] Portal credentials issued at approval
- [ ] Tracking link auto-generated
- [ ] Unique coupon code issued (coupon-deal archetype)
- [ ] Asset hub access granted
- [ ] Terms + FTC disclosure attestation captured at approval
- [ ] Tax form + payout method collection triggered — **gates payout, not onboarding**: don't let anyone earn a commission before this is done
- [ ] Archetype tag applied (coupon-deal / content-review) so routing fires correctly

If any of these are manual today, fix them first — manual provisioning runs 1-3 business days, which burns the highest-intent window before the affiliate gets a single email.

---

## Routing

| Archetype | Tier | First action asked | Leading asset |
|---|---|---|---|
| Coupon-deal | Self-serve | Publish the exclusive code | Unique per-affiliate code, code-page template |
| Content/review site | Self-serve | Place link in an existing high-traffic post | Best-converting pages, product one-sheet, seasonal angles |

Both routed self-serve by default — no AM was named. If that changes, content sites are the one worth a manual check-in (they take longer to activate and a nudge from a real person moves the needle more than it does for coupon sites, which convert on code visibility alone).

---

## SEQUENCE PLAN — Hoymar Affiliates, 2026-09

```
Activation       : first tracked sale within 30 days of approval
                   (cookie window is 60 days — separate axis, stated in copy, not
                   used as the activation cutoff)
Routing          : coupon-deal -> self-serve | content/review -> self-serve
                   (no AM named -> no hybrid/high-touch tier; revisit if that changes)
Touches          :
  T1 Trigger : approval (within minutes)
     Channel : email   Sender : automated program address
     Action  : copy your link/code (in the first two lines)
     Content : approval confirmed; commission/cookie/payout terms; disclosure
               attestation; under 300 words
     Asset   : pre-coded link (+ coupon code for coupon-deal)
  T2 Trigger : day 2-3
     Channel : email   Sender : automated
     Action  : grab your one asset and use it
     Content : coupon sites -> code-page template; content sites -> product
               one-sheet + best-converting pages
     Asset   : asset hub, deep-linked per archetype
  T3 Trigger : first click (behavior; overrides calendar)
     Channel : email   Sender : automated
     Action  : place the link/code on the page that traffic came from
     Content : celebration + which page converts best for that traffic
     Asset   : best-converting-pages one-sheet
  T4 Trigger : no click by day 15 (behavior — half the 30-day window)
     Channel : email   Sender : automated
     Action  : one 30-minute promo (send a ready-cut post / publish the code)
     Content : lowest-effort version of the ask, fully pre-written
     Asset   : swipe copy / social caption
  T5 Trigger : day 21, only if not yet activated
     Channel : email   Sender : automated
     Action  : make one sale by day 30
     Content : deadline-bound activation bonus, framed as opportunity not condition
     Asset   : link/code reminder
  T6 Trigger : first sale (behavior)
     Channel : email   Sender : automated
     Action  : none — celebrate; state commission approval timing (after return
               window) and payout date (net-30)
Activation nudge : first-sale bonus, expires day 30, carried by T5
Never-activated  : entry = no click and no sale by day 30; re-engagement at day 45
                   (Excite + one incentive + one asset); final notice at month 6
                   ("account archived unless you reply" — no threat framing);
                   archive, don't delete
Exits            : on activation -> celebration touch (T6), then off the calendar
                   track entirely; on branch entry -> main sequence stops, branch
                   rules take over; unsubscribes honored immediately
KPIs             : 30-day activation rate | median time-to-first-sale |
                   never-activated share at day 30 | per-touch open/click
```

---

## The emails

**⚠️ Note on the humanizer pass:** the skill's own workflow requires running every draft through a humanizer skill before it's final — reject raw first-draft copy. This session doesn't have a general-purpose English humanizer skill loaded (only a French one and a technical-documentation one, neither fits marketing email). I've written these in a direct, human register already, but **run them through whatever tone/humanizer pass you use before sending** — treat what's below as content-final, not tone-final.

Each subject line and body is tagged with its AIDA beat inline, per your boss's ask — that's the copy-level mapping; the send logic above it is the trigger-based architecture.

---

### T1 — Welcome (fires at approval)

**Subject:** Your Hoymar link + code are live

> **[Attention]** You're approved — welcome to the Hoymar affiliate program.
>
> **[Interest]** Here's your tracking link: `{{tracking_link}}`
> {{#if coupon-deal}}And your code: **`{{unique_code}}`** — publish it wherever you'd usually run a deal.{{/if}}
> {{#if content-review}}Drop that link into whichever post already gets your best outdoor-gear traffic — it's tracked the moment someone clicks.{{/if}}
>
> **[Desire]** You earn 8% on every sale it drives, tracked for 60 days after the click. Payouts go out net-30 once you clear $50, after our 30-day return window closes on each sale. One thing before your first payout: we'll need your tax form and payout details — get that done now and it's one less thing later.
>
> By clicking through, you're confirming you'll disclose the affiliate relationship on anything you publish (quick, standard FTC requirement) — full terms are in your portal.
>
> **[Action]** Copy your link above and place it somewhere it'll actually get seen this week.
>
> Questions — just reply.

---

### T2 — Tools (day 2-3)

**Subject — coupon-deal:** Your code page template
**Subject — content-review:** Your best-converting Hoymar pages

> **[Attention]** Quick one — here's the asset that gets our affiliates their first sale fastest.
>
> **[Interest]** {{#if coupon-deal}}This code page template is what our top coupon partners use — code, terms, and a photo, ready to paste.{{/if}}{{#if content-review}}These three product pages convert best from review/comparison traffic: [Trail packs], [Hardshell jackets], [Camp cookware]. Link into whichever matches what you already write about.{{/if}}
>
> **[Desire]** Everything's in your asset hub — logos, product shots, and this week's seasonal angle (early-fall trail gear), so you're not starting from a blank page.
>
> **[Action]** Grab one asset from the hub and use it today: {{asset_hub_link}}

---

### T3 — First click (fires on behavior, not calendar)

**Subject:** Nice — your first click just tracked

> **[Attention]** Someone just clicked your Hoymar link.
>
> **[Interest]** Since that traffic already found your {{content/code}}, here's the page it's most likely to convert on: [{{best_converting_page}}].
>
> **[Desire]** You're now one sale away from your first commission — no extra step needed.
>
> **[Action]** If you haven't already, place that same link/code near where this traffic came from — it's the fastest way to turn a click into a sale.

---

### T4 — No click by day 15 (behavior override)

**Subject:** One 30-minute thing this week

> **[Attention]** No rush, but we haven't seen your link get placed yet.
>
> **[Interest]** Here's the lowest-effort version: a ready-written {{post/email}} with your code already dropped in — copy, paste, publish.
>
> **[Desire]** It's the same 8% commission, just a smaller lift to get started.
>
> **[Action]** Copy this and publish it today: {{swipe_copy_link}}

---

### T5 — Activation nudge (day 21, if not yet activated)

**Subject:** Bonus for your first sale — through day 30

> **[Attention]** Your first 30 days close on {{date}} — here's a reason to make it count.
>
> **[Interest]** Land your first tracked sale before then and we'll add a **{{bonus_amount}} bonus** on top of your standard 8%.
>
> **[Desire]** No catch, no minimum spend on the shopper's side — just get one order through your link or code by {{date}}.
>
> **[Action]** Your link: `{{tracking_link}}` {{code_if_applicable}} — one placement is all it takes.

*(Framed as a finish line to hit, never a condition for staying in the program — no "or your account may be reviewed" language anywhere near this.)*

---

### T6 — First sale (fires on behavior)

**Subject:** Your first sale just tracked 🎉

> **[Attention]** You just earned your first Hoymar commission.
>
> **[Interest]** It's sitting as pending while the order clears our 30-day return window.
>
> **[Desire]** Once that closes, it moves to approved and pays out on our next net-30 cycle — assuming you're past the $50 threshold.
>
> **[Action]** Nothing to do here — just wanted you to see it land. Keep going: {{best_converting_page}} is still your top spot.

---

## Never-activated branch (entry: no click, no sale by day 30)

**Day 45 — re-engagement** (Excite + Equip, one email, no fake urgency):

**Subject:** Trail season's picking up — want a fresh angle?

> **[Attention]** You joined Hoymar a few weeks back but haven't placed your link yet — totally fine, just checking in.
>
> **[Interest]** Early-fall is one of our best-converting windows for {{trail packs / layering gear}} — might be worth a look if it fits what you cover.
>
> **[Desire]** Your 8% commission and code are both still active and waiting.
>
> **[Action]** One idea: {{one_concrete_placement_suggestion}}. Your link: `{{tracking_link}}`.

**Month 6 — final notice** (housekeeping tone, no threat):

**Subject:** Keeping your Hoymar account active

> We noticed your affiliate link hasn't seen activity yet. We'll archive inactive accounts after this to keep our records current — just reply and we'll keep yours open, no explanation needed. If we don't hear back, you can always re-apply later.

Then: **archive, don't delete** — suppression keeps the activation-rate metric honest and leaves the door open. A reactivated affiliate re-enters at **T2** (tools), not T1 — they don't need re-approval, they need a working asset and one action.

---

## Exit / suppression / re-entry rules

- **On activation** (T6 fires) → affiliate leaves the onboarding track entirely and moves to standard program comms. Continuing the drip past their first sale reads as nobody's watching.
- **Trigger overrides calendar**: if a behavior trigger (click, sale) fires within a day of a scheduled calendar touch, send the trigger email and skip the calendar one.
- **Unsubscribes** honored program-wide, immediately.
- **Re-entry from archive** → lands at T2, not T1.

---

## KPIs and when to judge them

- **Primary:** 30-day activation rate, per monthly approval cohort (judge each cohort only once its 30-day window closes — a blended all-time number hides whether things are improving).
- Median time-to-first-sale.
- Never-activated share at day 30.
- Per-touch open/click, to localize where the sequence loses people if it underperforms.

**Pass gate:** ~18% 30-day activation (TrackRev's cited median — vendor-published, not audited) is the number to aim for, not the ~31% top quartile and not Track360's "below 30% signals a problem" line — that 30% figure is a trigger to go investigate, not a launch bar; treating it as a ship gate would demand top-quartile performance on day one. **Since Hoymar hasn't launched this sequence yet, there's no data to report against these gates** — first real read happens when your first approval cohort's 30-day window closes. Set that date on your calendar now and I'd suggest reviewing per-touch engagement at the 2-week mark as an early signal, before the full 30-day number is even computable.

**Before this ships:** confirm the commission/payout numbers above (they're placeholders), confirm server-side tracking is actually live (if it isn't, everything above the fold in the KPI section is unmeasurable), and run the copy through your tone/humanizer pass.