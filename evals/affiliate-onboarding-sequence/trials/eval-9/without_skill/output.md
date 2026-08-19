## Diagnosis: one root cause behind all three symptoms

All three problems come from the same design flaw: the automation is **step/time-driven** ("send email N on day N") instead of **state-driven** ("check the affiliate's current status before every send"). A schedule, once started, has no way to know the world changed underneath it. Fix the state-check, and all three symptoms disappear together.

## Fix 1 — Stop mailing converted affiliates

**Add a suppression check, not a one-time exit trigger.** The bug isn't that there's no "made a sale" branch — it's that the check (if it exists) only runs at enrollment, so a conversion on day 3 never gets re-evaluated before the day-21 send fires.

1. Create a persistent affiliate-state field (`has_converted: true/false`, set by the sale event, not by a human) — this is your single source of truth, not the email tool's internal step position.
2. Add that field as a **suppression condition evaluated at send-time on every step**, not just at flow entry. Every ESP has this: Klaviyo "flow filters," ActiveCampaign "goals" with conditional exit, HubSpot "unenrollment triggers," Customer.io "exit conditions," Iterable "workflow exit criteria."
3. On the sale event, don't just skip the day-21 email — **exit the whole welcome drip** and move the affiliate to a distinct "activated" track (congrats/next-tier/upsell content). Killing one email but leaving them queued for the rest is the same bug in miniature.
4. Audit for the exact complaint you got: a sale that lands *after* an email is already queued/rendering needs the suppression check to run immediately before send, not only at nightly batch time.

## Fix 2 — Reactivating the 40 archived affiliates: don't restart at step 1

Restarting at the top assumes they're identical to a brand-new signup. They're not — some already passed the activation gate before going dormant, and dropping them back at day 0 re-triggers the exact bug in Fix 1 for anyone who'd already made a sale.

1. **Audit before re-adding**, segment into three cohorts:
   - Never made a sale → restart the welcome drip, but swap in "still with us?" framing for step 1, not the original cold-open copy.
   - Made 1+ sale before going dormant → skip the activation content entirely (including day-21), enter directly on a "reactivation / holiday push" track built for people who already know how the program works.
   - Explicit unsubscribe/complaint in their history → exclude from bulk reactivation; needs individual review or re-permission before any automated email, not just a list re-add.
2. Build reactivation as **its own flow/campaign with its own entry point**, not a re-add to the original list. Most ESPs block re-entry into a flow a contact already completed/exited by default — that's a feature, not a bug to route around by cloning the old sequence.
3. Give the reactivation flow the same send-time suppression check from Fix 1, so it inherits the fix instead of reintroducing the bug on a new 40-person batch.

## Fix 3 — Automation firing during a live human thread

The ESP and your inbox don't share state, so the automation has no idea a rep is mid-conversation. Treat "a human is actively engaged" as a suppression signal exactly like "has converted."

1. **Minimum fix:** a manual flag ("human handling," set/unset by whoever owns the thread) added to the same suppression check used in Fix 1. Give it a default expiry (e.g. auto-clear after 10 days of thread inactivity) so someone forgetting to unflag doesn't silence an affiliate forever.
2. **Better fix if your inbox is shared/CRM-integrated** (Front, Missive, Help Scout, or a CRM with email sync): wire inbound-reply detection to auto-suppress that contact via webhook — don't rely on reps remembering to flag manually. Manual flagging degrades under volume; detection doesn't.
3. Either way, this suppression must be checked **per-send**, same as conversion — a flag set after the day-14 email is already scheduled needs to block that specific send, not just future ones.

## The one structural change that fixes all three

Stop treating the affiliate's position in the sequence as the thing that controls sends. Instead:

- Maintain one status field per affiliate (`new` / `activated` / `dormant` / `reactivated` / `human_handling` / `unsubscribed`) as the system of record.
- Every scheduled send re-checks that status immediately before firing — not just at enrollment.
- Every state transition (sale made, human takes over thread, reactivation, unsubscribe) is an event that updates this field, and any flow (welcome, reactivation, future ones) reads from the same field instead of each maintaining its own logic.

This is the standard "goal + suppression list" pattern in lifecycle marketing — every major ESP supports it natively (Klaviyo flow filters, ActiveCampaign goals, HubSpot workflow re-/unenrollment triggers, Customer.io exit conditions, Iterable workflow exit criteria). You're not missing a feature; you're missing the re-check-at-send-time habit, and it's the same one-line fix in three different places.