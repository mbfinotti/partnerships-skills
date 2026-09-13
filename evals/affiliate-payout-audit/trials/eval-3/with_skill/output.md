## Short answer

Yes — absorb both, but not silently. Document them as findings, book them as write-offs with reason codes, and use them to fix the control gap that let both slip through. Direct recovery and offsetting are correctly off the table here — not because "eating it" is the lazy option, but because your own terms and your own facts eliminate the other rungs.

## Why the other remediation options are closed, not just inconvenient

The affiliate-payout-audit remediation ladder is: **correct before release → offset against future commission → absorb and document → fix it forward → direct recovery.** Two things here delete the top and bottom rungs outright:

- **Your platform's terms** ("once paid, cannot be taken back under any circumstances") are the PartnerStack-style clause the skill treats as a hard stop: _"If the terms or the platform forbid reclaiming a paid commission, delete offset and direct recovery; absorb and fix-it-forward are the whole menu."_ An offset is still "taking it back," just spread over future payouts — your terms don't carve out an exception for that.
- **No finance co-signer this cycle** independently deletes direct recovery on its own, terms aside.

So for both lines, "correct before release" is moot (money's already moved) and offset/direct recovery are structurally unavailable. What's left — absorb and document, plus fix it forward — is the actual right answer, not a fallback.

## Order 88412 — $148.80 (12% of $1,240)

This is the textbook **post-lock refund**: lock (Feb 10) → refund (Feb 19) → payment run (Feb 20) — the refund landed one day _before_ the money actually went out, but the record was already locked so nothing re-checked it. "The platform won't let me touch the record" is expected behavior at that state, not a bug to route around — locked/paid means no on-platform reversal, not "no longer owed."

- **Finding**: material, lifecycle-gate failure (reversal not applied before payment release), reason code `return/cancellation`.
- **Action**: absorb $148.80, documented against this affiliate.
- **Root cause worth fixing**: there was a full day between the refund and the payout run where a reversal check would have caught it for free. That's not a terms problem, it's a missing control between "locked" and "paid."

## PineRidge Deals — $3,110

Same rung, reinforced two ways at once: she's churned out with zero balance, so offset has no future earnings to land against even if terms allowed it, and the terms bar reclaiming paid commissions regardless.

- **Finding**: material, reason code `return/cancellation`, unrecoverable per the skill's own language for this exact situation ("a partner who churns out with a negative balance is an unrecoverable loss — report it as absorbed, never as recovered, and quantify it").
- **Action**: absorb $3,110, documented.
- **Worth a side glance, not action here**: a partner whose commissions turn out to be concentrated in returned orders right before she stops promoting is a pattern worth a fraud-review referral — that's outside this audit's scope (it checks correctness, not legitimacy), so flag it, don't rule on it.

## Total absorbed: $3,258.80

## Fix it forward (this is the part that actually saves you money next time)

Both errors are the same error class — refunds arriving after lock with no gate before payment — so fix the class, not just the two lines:

1. **Insert a reversal check between lock and payment release.** Even though a locked record can't be edited, the payment run can still exclude/delay a line that shows a refund posted since lock. This alone would have caught order 88412.
2. **Lengthen the validation/locking window** so it covers the realistic return curve for this program, rather than locking before returns typically land.
3. **Add a reserve/holdback** (retain a small % of each payout against late reversals) if your platform supports negative balances at all going forward — this is the standard way programs absorb this risk without needing terms to allow clawback.
4. Don't skip the checker just because finance is unavailable this cycle. Maker-checker is the one gate the skill says never to drop — get any second qualified reader (doesn't have to be finance) to sign off on the two write-off entries before you close them out. That sign-off is your evidence trail if either affiliate disputes the numbers later.

## One thing to verify before you close this out

Confirm the terms clause you quoted is program-wide and not limited to a specific commission type — if it only covers standard commissions and these two are booked under a different mechanism, the offset rung might reopen for order 88412 specifically (PineRidge's is closed either way since she's inactive). Worth a two-minute check before you finalize the write-off language.
