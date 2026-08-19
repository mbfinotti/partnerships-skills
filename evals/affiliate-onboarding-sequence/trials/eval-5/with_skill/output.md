## Is 19% bad?

No — don't pause the program on this number. Here's why, straight from the reliability-flagged benchmark data:

**Her 30% figure is being used the wrong way.** That's Track360's "below 30% signals onboarding problems" line. It's explicitly a *diagnostic trigger for investigating*, not a ship/fail gate. Used as a gate, it demands top-quartile performance on day one — Track360's own reference point sits in TrackRev's ~31% *top quartile*, not its ~18% median. Calling 30% "industry standard" and pausing the program over it misreads a vendor blog's flag-for-review threshold as a pass/fail bar.

**19% sits right around the actual median, not below it.** TrackRev's synthesis (no audited primary source, vendor data — treat directionally) puts 30-day activation at ~18% median, ~31% top quartile, ~6% bottom quartile. 19% lands at the median, not the bottom quartile where a real "our affiliates are bad" signal would show up. Separately, the practitioner-convergent range for affiliates who *ever* produce a single sale is 5-20% (Matt McWilliams: "95% of affiliates who sign up never make a single sale") — 19% at 30 days is a solid result against that backdrop, not a warning sign.

**None of this is audited data** — it's vendor-published and practitioner-convergent, useful for calibrating your own gate, not for quoting as fact to leadership.

## What to tell your head of growth

- The "30% industry standard" is a diagnostic trigger from one vendor blog, not a benchmark — using it as a pass/fail gate would require top-quartile performance from day one, which isn't what "standard" means.
- 19% at 30 days is at the practitioner-cited median for B2C affiliate activation. It's a normal result, not evidence the affiliate pool is bad.
- Before concluding it's a recruitment-quality problem, run the cheap diagnostic checks first (in order of information-per-effort): trace one conversion end-to-end (click → recorded conversion → commission) to confirm the number isn't understated by tracking loss, check that the approval email actually ships a working link/code, and read per-touch open/click rates. Any of those can produce exactly this symptom without the affiliates themselves being the problem. Re-recruiting is the most expensive, least-informative move on the list — it destroys your ability to tell later whether the sequence itself was ever the issue.

## What threshold to hold going forward

Set your working floor at **~18-20% activation at 30 days for B2C**, reviewed per monthly cohort. Below that, the fix path is: diagnose onboarding (provisioning, first touch, nudge, never-activated branch) — not recruitment. Above it, the sequence is doing its job; look for incremental gains (nudge timing, archetype-specific routing) rather than a rebuild.

Document that this gate is a vendor/practitioner figure, not an audited standard, so it doesn't get miscited the same way Track360's 30% just was — and note if your program's economics (commission structure, cookie window, archetype mix) justify holding a different number.

## Which number to report: 19%, not 11%

Report the **August cohort's 30-day rate (19%)**, not the all-time rate. The skill's own KPI framing is explicit on this: measure by monthly approval cohort, judged only when its window closes — a blended all-time rate hides whether the sequence is improving.

Your 11% all-time number is lower almost by construction, and that's not new information — it mixes in:
- Older cohorts approved before any onboarding fixes existed.
- Affiliates approved before tracking or provisioning was solid (a dark tracking hop understates activation regardless of true affiliate behavior).
- Long-dormant affiliates from early recruitment pushes who were never a fair test of the current sequence.

Reporting 11% next to a "30% standard" is what triggered the panic in the first place — it's the wrong metric held against the wrong bar. Keep 11% as a lagging, historical-trend footnote if useful ("all-time reference: 11%, reflecting pre-[fix date] cohorts"), but the number that should drive the pause/no-pause decision is the current cohort's 19% against your ~18-20% floor.