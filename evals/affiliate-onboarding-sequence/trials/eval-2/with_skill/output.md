## Before the copy — one flag the skill requires I raise

The symptom you described — clicks visible in the affiliate dashboard, but activation reported at 4% — is the exact profile of check #1 in this skill's diagnostic order ("conversion trace"), not a copy problem. Cookie-only tracking with no server-side postback is a known dark hop: Safari/WebKit caps JS-set landing cookies at 24h under link decoration and clears script-writable storage after 7 days of no interaction. If any hop between click → recorded conversion → pending commission is silently dropping, your true activation could be materially higher than 4%, and a welcome-email rewrite won't show up in the number at all.

Per this skill's own failure-mode ranking, "rewrite touch 1" is explicitly the **last** move, not the first — it destroys your baseline before you know whether the fix worked. Recommended in parallel, cheap (an hour, once): manually trace one real click through to a paid commission this week. I'm delivering the rewrite you asked for below, but treat it as running alongside that trace, not instead of it.

Also, for context: 4% sits below even TrackRev's bottom-quartile 30-day activation (~6%), not just below the ~18% median — so "furious" isn't misplaced, but these are vendor-reported, not audited numbers, and shouldn't be quoted to your CMO as an industry-certified standard.

**Assumptions I made** (fill in the bracketed values — I won't invent real commission/payout numbers):
- Activation = first tracked sale within 30 days of approval (standard B2C default; confirm this matches your definition).
- Sender = automated program address (no named AM mentioned; self-serve is the right tier at 90 approvals/month regardless).
- Archetype mix unspecified, so copy below is written generically across content/coupon/social/email-list affiliates — if one archetype dominates your intake, the single action line in T2 should be swapped to match it.
- No humanizer skill in this session is built for English marketing/affiliate copy (the one loaded is for technical/simplified-English documentation, wrong register here), so I hand-applied the pass myself: no "unlock/seamless/embark," no stacked rule-of-three, no generic "Welcome to the family" energy. Have a second human pass before sending.

---

## T1 — Welcome (send: automatically, minutes after approval)

**Subject:** Your tracking link + code are live

Hey [First Name],

You're approved. Here's your link:

**[unique tracking link]**
Code: **[unique code]** — works even if someone skips the link.

Fastest way to get your first commission: drop that link into whatever you've already got that gets traffic — a post, a page, a pinned link, an email list. No new content needed to start.

The numbers: [COMMISSION_RATE]% per sale, tracked for [COOKIE_WINDOW] days after a click. Commissions clear after [HOLD_PERIOD] and pay out once you hit [PAYOUT_THRESHOLD]. One requirement: disclose that your link is an affiliate link wherever you post it — [link to disclosure guidance].

Two more emails coming this week: one with ready-to-use assets, one with a time-boxed bonus if you're fast. That's it — no drip of newsletters after that.

Questions, just reply.

[Program name]

---

## T2 — Tools (send: day 2–3, first follow-up)

**Subject:** One asset, one place to put it

Hey [First Name],

Quick one. Here's a swipe email you can send today, already written: **[asset hub link]**.

Also in there: product images, top sellers this month, and a banner set — grab whatever fits where you post.

One action that moves the needle fastest: send that email (or post that swipe copy) to your list/audience this week, with your link from the first email in it.

If you've already placed your link somewhere — you're done here, ignore this.

[Program name]

---

## T3 — Time-boxed nudge (send: day 7–10, second follow-up)

**Subject:** $[BONUS_AMOUNT] bonus if your first sale lands by [DEADLINE_DATE]

Hey [First Name],

Haven't seen your first click yet, so — fastest path in: post the swipe copy from the last email, or just drop your link in one place your audience already checks. Ten minutes, tops.

Do it and get your first tracked sale by [DEADLINE_DATE], and we'll add $[BONUS_AMOUNT] on top of your normal [COMMISSION_RATE]%.

Your link, again: **[unique tracking link]** / code **[unique code]**.

[Program name]

---

**Structural notes carried over from the skill (don't drop these when editing):** link/code sits in the first two lines of T1; each email asks exactly one action; the deadline in T3 is framed as a bonus with a finish line, never as a condition of staying in the program; if a real click/sale fires between sends, skip or delay the next calendar email rather than stacking two in one day. None of these three replace the never-activated branch (diagnostic → re-engagement → one final notice → archive) — that's a separate, still-open piece of the sequence if it doesn't already exist.