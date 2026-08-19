## My read: don't scrap it — the data doesn't support that diagnosis

Your numbers (61% → 54% → 9% → ~40% → ~40%) are a **V-shape**, not a decay curve. Real "email fatigue across the sequence" looks like a steady slide (61 → 45 → 30 → 20 → 15). Yours dips hard at one touch and recovers on the next two. That shape points at touch 3 specifically, not the format.

This matters because there's a documented single-hub swap pattern (monday.com, via PartnerStack — one company, not an industry standard) that this skill's reference material gates explicitly:

> "Reach for the hub only when the per-touch engagement data shows opens decaying **across the whole sequence** — never because one touch underperforms, which is a copy problem the hub does not solve."

Your data is the second case, not the first.

## What's actually wrong with touch 3

Touch 3 is the "connection" slot — a reply-seeking, personal check-in. It's going out from **program@**, an automated/generic address. The house rule for this exact touch type: *"the named AM for the connection touch and anything asking for a reply — a reply-seeking email from a no-reply address answers itself."* That's almost certainly your 9%: affiliates see an automated address asking them to justify their promotion plan, and it reads as either a compliance check or spam-adjacent, so they skip it. Then touch 4 shows up with an actual asset/nudge and engagement recovers on its own — further evidence the sequence itself is fine.

## Cost comparison

- **Fix touch 3**: change the sender (named AM if one exists, or reframe as an automated asset-delivery touch instead of a personal ask) and rewrite the copy so it isn't an interrogation. ~an hour, reversible in an hour.
- **Replace the drip with a hub**: a quarter of dev time, plus it becomes a standing maintenance job (video goes stale, assets drift), and if it underperforms you're rebuilding the exact sequence you deleted.

That ratio alone should decide it for a single mis-sent touch.

## What you'd lose by going fully self-serve

- **The push mechanism.** A hub only works for affiliates who go look at it. Touch 1 is already getting 61% opens / 28% clicks without anyone visiting anything voluntarily — that's evidence email-based outreach is working, not that people are tired of it.
- **The behavior-trigger layer** — first-click celebration, no-click-by-day-N nudge, no-click on a payout-setup step. None of that exists on a static page.
- **The time-boxed activation nudge** — "earn X by \<date>" only works as a scheduled push with a deadline; a hub page can't create urgency on its own.
- **The never-activated branch's entry signal.** You detect "never activated" by the absence of clicks on a schedule of sends. No sends, no signal — you'd need to build separate visit-tracking on the hub to replace it.
- Also worth flagging: the monday.com case people cite for this isn't actually "fully self-serve" — it kept weekly kickoff calls, certification courses, and sandbox access alongside the hub. It's a hybrid/high-touch build with a good asset hub attached, not a replacement for outreach.

## What I'd do instead

1. **Keep touches 1, 2, 4, 5** — they're performing at or above the range this pattern usually sees.
2. **Build the hub anyway** — it's a good idea, just not as a replacement. Point T2 and T4 at it as the persistent asset location instead of attaching files inline. This is literally the documented fix for the "welcome dump" failure mode, and it gives affiliates a self-serve fallback without removing the sends that are getting attention.
3. **Fix touch 3 only**: swap program@ for a named AM if you have one, or convert it from "reply and justify your plan" into either (a) an automated low-effort nudge like T4's, or (b) a true behavior trigger — only fire it at affiliates who *haven't* clicked yet by day 7, instead of blind-sending it to everyone including people who already converted from touch 1.
4. Before committing dev time either way, two checks worth doing first (near-zero to an hour each, cheaper than a quarter of build):
   - Trace whether touch 1/2's clicks are converting at all — confirms the activation numbers behind this are real before you optimize around them.
   - Split touch 3's 9% by archetype or by whether a named AM exists for that segment — you may find it's fine for one group and collapsing only for another, which changes the fix.
5. Only reconsider the hub-swap if, after fixing touch 3, opens still decay start-to-finish rather than dipping and recovering — and even then, the pattern here says collapse T2–T4 only, keep T1 and the trigger layer.

One gap I can't fill from what you've given me: I don't know your activation definition (first click/sale/deal), the window, or whether tracking is server-side — those determine whether "9% opens" is even the right thing to be worried about versus actual conversion. If you want the full plan built out properly rather than just patching touch 3, happy to run the intake questions for that.