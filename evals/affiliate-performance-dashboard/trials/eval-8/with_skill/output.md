## Sanity check: don't send this yet — two of the three numbers are artifacts of the window change, not genuine improvement

Running this against the dashboard skill's ground rules (specifically: _"Never compare two periods with different validation windows — reversal lag makes the recent one look artificially good"_ and the reversal-lag failure mode: _"Recent periods look artificially good → compare only fully-validated periods; flag immature ones"_).

### Verdict on each number

**Q1 (15.1%) vs Q2 (11.4%) — invalid comparison, don't headline as "improvement."**
You changed the validation window mid-Q1 (start of March). That means:

- Q1 is a blended methodology — Jan/Feb orders locked under the old 30-day window, March orders under the new 60-day window, all inside one quarter number.
- Q2 is the first quarter run entirely on the 60-day window.

A longer validation window mechanically changes how much reversal activity gets caught _before_ a commission locks, independent of anything affiliates actually did differently. So some — possibly most — of the 15.1% → 11.4% drop could simply be the window doing its job, not the program getting cheaper. You have no way to separate "real improvement" from "methodology artifact" with the data as stated. This is the textbook case the skill calls out by name.

**August (9.2%) — this is not your best month, it's your least-mature month. Don't touch it.**
Today is Sep 12. Your validation window is 60 days, counted from the order date. The earliest August order (Aug 1) doesn't hit its day-60 mark until **Sep 30**; the last (Aug 31) not until **Oct 30**. That means **zero August orders have completed the validation window yet** — the 9.2% figure is validated-commission-so-far over revenue-so-far, with the entire remaining reversal/return/chargeback tail still to land. This is the exact reversal-lag trap the skill flags: immature periods always look better than they'll end up. Calling it "best month ever" and putting it on a dashboard headline is close to the negative-example failure mode in the skill's worked examples (gross/immature numbers presented as if final).

**Q2 (11.4%) is, on its own, legitimate** — every Q2 order has now passed its full 60-day window (last one matured Aug 29), so that number is mature and clean _within the new methodology_. It's just not comparable to Q1.

### Before you set 10% as a standing target

- You don't yet have a clean baseline. You have exactly one mature quarter (Q2) under the new 60-day window. One data point isn't a baseline — it's a start.
- Confirm the numerator on all three figures includes **validated commission + network fees + agency fees + placement/tenancy fees + bonuses**, not just commission. Excluding network/agency fees is the single most common way a program understates true cost of sale, and it would change whether 10% is even realistic.
- Tag whatever target you ship as `[DERIVE — provisional]`, not a confirmed benchmark, and commit to revisiting it after Q3 (the second full quarter on the stable window).

### What to send instead

1. **Kill the Q1→Q2 improvement headline.** Replace with: "Cost of sale under the new 60-day validation window: 11.4% (Q2, fully matured). Not comparable to pre-March figures — methodology changed mid-Q1." Annotate the window-change date directly on any trend chart that spans it, per the skill's rule that a validation-window change gets flagged on every chart it touches, never silently absorbed into a trend line.
2. **Pull August off the dashboard as a headline entirely** until it matures (earliest safe read: Oct 30, and even then check the tail hasn't shifted). If you want an early read, label it explicitly: "August — provisional, X% of validation window elapsed, will move."
3. **Set 10% as a working target, not a locked one** — label it provisional, and put "confirm baseline after Q3 close (fees included, full 60-day maturity)" as an open item next to it.
4. **Add a reversal-rate line next to cost of sale** on the same view. It's near-zero cost to add (same state machine), and it's what lets a reader tell "real improvement" from "window artifact" going forward — right now you're inferring that split from a single ratio, which is exactly what the reversal-rate metric exists to stop.

### Open items to confirm before finalizing

- Did the window change apply retroactively to Jan/Feb orders not yet locked, or only to orders placed from March 1 onward? This determines exactly how contaminated Q1 is.
- Do the 15.1% / 11.4% / 9.2% figures already include network + agency + placement fees, or commission only?
- Product return window is 30 days and validation window is now 60 — confirm chargebacks (which can lag further than returns) are also expected to close within 60 days for your processor; if not, even Q2's "mature" tag needs a caveat.

Bottom line: send Q2's 11.4% as a standalone, labeled number. Don't send the Q1 comparison or the August "best month" claim — both are the specific traps this skill's ground rules exist to catch, and both would get someone asking hard questions once the window fully matures and the real numbers move.
