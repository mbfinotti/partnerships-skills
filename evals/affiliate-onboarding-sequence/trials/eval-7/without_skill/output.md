**Short answer: don't scrap the drip — fix touch 3 first, then decide.**

The pattern you're describing doesn't support "email nurture is broken," it supports "touch 3 specifically is broken."

**What the numbers actually say**

- If fatigue/format were the problem, opens would decay monotonically: 61 → 54 → lower → lower → lower.
- Instead you get 61 → 54 → **9** → ~40 → ~40. That's a cliff, not a slope. Touches 4-5 recovering to 40% _after_ a 9% touch proves people are still willing to open your mail — something about touch 3 itself (sender, subject, framing) is tanking it, not "5 emails is too many."
- Prime suspects, in order I'd bet on: sending from `program@` (reads as ops/compliance mail, not part of the onboarding relationship the first two emails built) and the framing itself ("how do you plan to promote?" lands as homework/a survey, not value delivered).

**The risk in the hub-page plan**
A self-serve hub is a good asset to build regardless, but replacing _active, sequenced_ touches with a _passive_ page usually loses reach, not gains it — nobody visits a hub they weren't prompted to visit. You'd be trading a diagnosable, cheap problem (one bad email) for a quarter of dev time and an unproven assumption that self-serve converts as well as nurture for a relatively low-intent, un-cademic audience like new affiliates.

**Recommendation**

1. Build the hub page — it's a good investment either way (video walkthrough + assets in one place is genuinely useful, and it gives every touch something concrete to link to).
2. Don't kill the 5-touch sequence. Instead, gut touch 3: change sender to a named person, drop the "check-in" framing, make it "here's your promo toolkit" pointing at the hub.
3. A/B test that single change for 2-3 weeks before committing dev time to anything bigger.
4. If touch 3 recovers to ~40-50% like its neighbors, you've fixed the actual problem for a day of copywriting instead of a quarter of engineering. If it still tanks even with a good sender/framing, _then_ you have real evidence to justify the hub-only rebuild.

Bottom line: the data is telling you it's a sender/copy problem on one email, not a "the drip doesn't work" problem — test the cheap fix before greenlighting the expensive one.
