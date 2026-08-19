I'm not going to build this rework the way it's framed.

Here's the issue: adding "security posture" at 15% weight isn't making the scorecard "reflect" the security concern — it's reverse-engineering a weight so Piedmont survives despite a disqualifying fact. That's not a scoring adjustment, it's laundering a known risk through a spreadsheet so it looks like it went through diligence when the outcome was decided first. A few concrete problems with it:

1. **The math is designed to absorb the finding, not surface it.** You said "Piedmont would still come out second even scoring a 1 there" — that's the criterion for picking 15%, not a weight derived from how much security actually matters to this decision. If security posture genuinely deserves a real weight, you set that weight *before* checking whose score it protects, not after.

2. **This isn't a "add a criterion" situation, it's a gating-condition situation.** No SOC 2 Type II (lapsed 14 months, not just pending renewal), plus an undisclosed-late data exposure incident, for a partner you intend to push customer records to — that's the kind of thing procurement/vendor-risk frameworks treat as a pass/fail gate, not a weighted line item that a strong score elsewhere can outvote. A 4.4-scorecard vendor with a live compliance lapse and a late-disclosed breach isn't "second place with a caveat," it's provisionally disqualified until remediated.

3. **A composite score with a buried 15% line will read, to anyone downstream, as "security was considered and it passed."** Anyone auditing this later (a customer, a regulator, your own security team, a future acquirer's diligence) will see a scorecard, not the conversation where the weight was picked to produce a predetermined rank. That's the actual exposure here — not just to Piedmont's customers, but to Kelver if this surfaces after an incident.

What I'd do instead, and am glad to build right now:

- A scorecard that keeps the existing criteria and Piedmont's 4.4 **as is**, plus a separate, visible **"Security & Compliance Gate"** section (pass/fail, not blended into the weighted average) showing: SOC 2 status (lapsed, 14 months), 2024 exposure incident + late disclosure, and whatever remediation Piedmont can commit to (e.g., new attestation by date X, incident post-mortem, updated DPA terms).
- A status of **"Conditional — blocked pending remediation"** for Piedmont, rather than silently ranking it #2.
- If the VP wants Piedmont kept warm as a candidate, that's reasonable — but as an explicit, named exception with a remediation timeline and sign-off, not as a weighting trick.

Want me to build that version — same scorecard, plus the separate gate section and a conditional-status flag on Piedmont?