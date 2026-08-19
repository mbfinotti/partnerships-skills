# Bellfort affiliate onboarding — flow-control fix

All three messes trace to the same gap: the sequence has no **exit, suppression, or re-entry logic** — it only has a calendar. Fix per `copy-and-sequence-logic.md`.

## 1. Day-3 sale still gets the full drip (including the day-21 bonus)

**Root cause:** no "exit on activation" rule. The automation checks the calendar, never checks whether the activation event already fired.

**Fix — add a pre-send guard on every remaining calendar touch:**

```
before sending any T-n calendar touch:
  if activation_event.fired == true:
    cancel remaining calendar touches
    fire T6 "celebration" touch once (if not already sent)
    hand off to standard program comms
    STOP — do not evaluate further touches
```

- Apply this to **every** touch downstream of T1, not just T21. The day-21 "make your first sale" email is the one that embarrassed you, but T2/T3/T4 have the same silent bug.
- The day-21 touch itself should be conditioned in its trigger definition, not patched after: **`T5 trigger = day 21, only if not activated`** — that "only if" clause is the actual bug fix, not an afterthought.
- On activation, fire a distinct T6 email: no ask, just confirm the sale tracked and state when commission approves/pays. Don't let the drip go silent with no acknowledgment — that's how you get "do you people not see my orders?"
- Backfill: run activation_event.fired against everyone currently mid-sequence today, before the next scheduled send, so this doesn't happen once more before the fix ships.

## 2. Reactivating ~40 affiliates from the archive for the holiday push

**Rule: re-entry is T2, never T1.** They're already approved and already attested to terms — sending T1 again re-asks them to accept terms they already accepted and re-explains the program to people who joined it once. Drop them at **T2 (tools)**: one asset, one action, dated for the holiday push.

Before you batch them in, split the 40 by *why* they're in the archive — the skill's branch draws this distinction for a reason:

- **Never-activated** (archived after zero clicks ever) → T2 as designed: fresh asset, plain "here's your link, here's what to do with it."
- **Dormant** (was active, went quiet — had a click or a sale historically) → they don't need onboarding, they need a win-back note. Consider skipping straight to a T3-style "here's the holiday assets, how are you promoting this year" instead of the generic tools email — sending a former-producer the same email as a never-clicked affiliate reads as your system not remembering them, which is the same complaint as issue #1.

Practically: tag the reactivation batch with `archive_reason` before re-entry, route accordingly, and re-provision their link/code (don't assume the old one is still live — that's the day-0 provisioning pre-condition, and a dead link on a reactivated affiliate is worse than on a new one).

## 3. Affiliates mid-thread with you over email, automation still firing

**Rule: suppress calendar touches while an AM reply thread is open.**

```
before sending any calendar touch:
  if affiliate.has_open_reply_thread_with_AM == true:
    skip this send (do not cancel — just skip)
    re-check at next scheduled touch
  when thread closes:
    resume calendar touches from the next unsent offset
    (don't stack the skipped ones — send only what's next, not a backlog)
```

- This is a **pause**, not an exit — different from #1. The affiliate hasn't activated or gone dark; they're just talking to a human right now, and a bot email mid-conversation makes the human conversation look fake.
- Decide now, not ad hoc, whether **behavior-triggered transactional notices** (commission approved, payout sent) still fire during an open thread. The skill flags this deliberately: those can survive suppression only if Bellfort's affiliate terms and applicable law say so — check the terms, don't assume either way.
- Mark "thread open" the moment the AM replies personally (not autoresponder), and clear it on AM's own judgment call ("resolved") or after N days of silence from the affiliate — pick N and write it down so it's not a per-case guess.

## Consolidated Exits block for the Bellfort sequence plan

```
Exits       : on activation -> cancel remaining calendar touches, fire T6 once,
              hand off to standard program comms
            : on AM reply thread open -> skip calendar sends, resume at next
              unsent offset when thread closes; transactional sends: confirm
              against terms/law before deciding they survive suppression
            : on never-activated entry -> ends main sequence, branch's own
              final-notice/archive rules take over
Re-entry    : reactivated-from-archive affiliates enter at T2, not T1
            : never-activated archive reason -> generic T2 (asset + action)
            : dormant archive reason -> T3-style win-back framing instead
```

## One thing to check before you ship this

Trace whether the current automation platform can evaluate `activation_event.fired` and `has_open_reply_thread` as pre-send conditions natively, or whether this needs a webhook/flag written from your order system and inbox into the automation tool. If it's flag-based, the flag is the actual fix — the guard logic above is trivial once the flag exists, and worthless without it.