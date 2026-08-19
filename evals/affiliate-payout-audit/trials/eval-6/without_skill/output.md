## What's actually broken

**Root cause: your validation window is shorter than your return window.** You approve/pay commission at day 7, but customers can still return at any point through day 30. Every payout batch is finalized before ~77% of the return window has even elapsed. That's not a rounding error — it's a structural guarantee that some fraction of "validated" sales will still reverse after the money is out the door.

🔴 **This explains the trend, not just the run.** 19% → 22% → 24% over three runs isn't three independent bad runs — it's the same undersized window compounding as volume or affiliate mix shifts. You will never stabilize this number by tightening review at day 7; the leak is between day 8 and day 30, which you've defined out of your own validation process.

🔴 **The 63 pending→paid lines are a separate, more dangerous problem.** A blended 24% reversal rate on returned merchandise is a commercial cost you can price in. A broken gate that force-approves commission with zero manual/automated check is an open door — it won't just admit legitimate fast-movers, it'll admit anything that doesn't trigger a *return* (self-referral, stolen-card fraud, duplicate clicks) and therefore never shows up as a "reversal" at all. These 63 are unverified, not just fast — treat them as such until you can show what approved them.

🔴 **~20 of 41 reversals with no note means you can't tell why money is coming back.** Without a reason code you can't separate "customer returned a sweater" (expected cost of doing business) from "affiliate self-referred and it got refunded" (fraud pattern) from "duplicate line, processing error." Right now the 19/22/24% trend is one undifferentiated number — it could be getting worse because returns are up, or because fraud is up, and those need opposite fixes.

## Fix this run before releasing $52,140

1. **Pull the 63 auto-approved lines out of the batch.** Route them back through whatever check pending→paid is supposed to enforce. Don't pay them on the theory that they're probably fine — that's exactly the assumption that let them skip review once already.
2. **Force a reason code on every reversal before it's netted against the run.** For the ~20 with empty notes, go get the reason (return, chargeback, fraud flag, duplicate). If it can't be produced, hold that amount in escrow rather than paying or writing it off blind.
3. **Pay only what's left after (1) and (2).** That's your real, defensible April number — not $52,140.

## Fix the program going forward

- ✅ **Close the window gap.** Either extend validation toward 30 days, or — to keep affiliates' cashflow complaint solved — split the payout: pay a partial share (e.g. 70-80%) at day 7, hold the rest in reserve, auto-release at day 30 if no return. This is the standard answer to "affiliates want fast money, but returns take 30 days" — you don't have to choose one deadline for both.
- ✅ **Patch the pending→paid bug.** Find whatever default rule or webhook is auto-approving without going through the gate, and close it. Then re-run the 63 through the real process retroactively.
- ✅ **Make the note field mandatory at the point a reversal is created**, not optional metadata filled in later — system-enforced, with a fixed reason taxonomy (return / chargeback / fraud / duplicate / manual adjustment).
- ✅ **Split the reversal-rate metric by cause.** One blended 19/22/24% number can't tell you if returns are rising (commercial) or fraud is rising (control failure). Track them separately — the fix is different for each.
- ✅ **Look at reversals and the 63 skip-approvals by affiliate ID before you close this out.** A program-wide rate hides concentration — if a handful of affiliates account for most of both, that's a targeted enforcement action (warn/suspend), not a program-wide policy change.
- ✅ **Set a trend trigger now, since you're 3-for-3 increasing:** e.g., two consecutive runs above a threshold auto-forces partial holdback on the next run until reviewed, so you're not relying on someone noticing the drift manually again.

One caveat on scope: I didn't find any files in this repo describing an internal "Quill and Hearth" payout system or export format — this repo's actual purpose is tracking *external* B2B SaaS affiliate programs you join, not operating your own apparel affiliate program. So the above is built entirely from the numbers you gave me, not from any repo data. If there's a system-of-record for this run elsewhere, worth pointing me at it to sanity-check the $52,140 recompute.