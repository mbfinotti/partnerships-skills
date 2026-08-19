This is a compliance-program resourcing review, not a single-asset check — it uses this skill's Measurement and Ranked Choices sections rather than the Six-Layer Check. Building on that basis:

**Disclaimer required by this skill:** This is a compliance-process review against published regulator guidance, not legal advice. Counsel owns the legal call on liability exposure and on any partner-facing enforcement action; this review finds what counsel and the FTC's own monitoring checklist would find. Keep every `[COUNSEL]` marker below until counsel resolves it.

## Verdict: the math justifies *some* budget ask, but not the one being requested

**The numbers as given:**
- 143 assets reviewed / quarter ≈ 11/week with one reviewer.
- 62% first-pass rate → 38% fail rate → ~54 assets failed first review last quarter.
- This skill's Measurement KPI: first-pass rate sustained below 80% "signals an upstream defect: fix the brief and the onboarding, not just the assets." 62% is 18 points under that line — this isn't noise, it's the threshold the skill exists to flag.
- 30 of 55 affiliates (55% of the entire roster) are producing **the same three catalogued failures**, not 30 different problems. Cross-check each against `references/disclosure-wording.md` and the Common Failure Modes table:
  - Ad tag dumped at the end of a hashtag wall = the placement/truncation failure ("disclosure below the fold" / buried among other tags — FTC's own example of "likely missed").
  - "#collab" = a wording failure on the reject list, explicitly named ("reads as friendship or affiliation without payment").
  - Disclosure in bio only = the presence/placement failure named verbatim in the failure table ("viewers of one post never open the profile").

All three are pre-solved in this skill's own reference material with ready-to-paste fixes. A second reviewer doesn't change what these three patterns are — it just re-diagnoses them, asset by asset, forever.

## Why more reviewer capacity is the wrong lever here

Per the skill's own Ranked Choices, monitoring throughput (the "full-roster review" rung, which is what a second reviewer buys) sits at the **bottom of value-per-effort** and is explicitly something to "starve" by default — promoted only when a regulator has made contact, the vertical is regulated, or the same partner fails twice. Here, the failure isn't per-partner-twice, it's 55% of the *roster* failing the same three ways. That's the specific condition the skill flags as an upstream-guidance problem, not a monitoring-capacity problem:

- **Getting the rules to partners** ranks the approved wording bank highest value-per-effort (~1 hour to adapt) — precisely the fix for #2 and #3 above.
- Your roster is "self-serve — apply, auto-approve, no team contact." The skill is explicit: *"Delete the live-training rung for a self-serve roster that never meets the program team: a session nobody attends is not distribution."* That also kills "corrected line in the review reply" as a scaling fix — nobody reads it before their next post either, since there's no relationship to carry it. The only rungs that can reach a self-serve, no-contact roster are ones baked into the automated flow itself: an approved-wording one-pager surfaced at application/approval, or an **automated label scan** run before or alongside human review.
- All three of your recurring failures are text-detectable (hashtag placement, "#collab" string, bio-vs-post location) — exactly what an automated scan catches, and exactly the profile where the skill says a scan is *not* to be deleted (it only gets deleted when disclosures are spoken/on-screen, which yours aren't). Setup cost: about a week, one-time, vs. a permanent second salary reviewing the same three patterns quarter after quarter.

So the honest reallocation: a scan + wording bank likely suppresses a large share of the 38% fail rate at a fraction of the cost of a hire, and it's the only route that actually reaches partners you never talk to. What's left for a human reviewer afterward is judgment calls and the genuinely novel failures — a smaller, harder-to-automate queue, which is a more defensible use of a second FTE than re-flagging "#collab" 54 times a quarter.

## Where the hire *is* still defensible

Separate the two asks instead of bundling them:

1. **Coverage, not fail-rate.** With automatic approval and zero human contact, review is the *only* control point satisfying the FTC's own monitoring duty (16 CFR 255.1(d), step 3 of its Endorsement Guides FAQ: "periodically search for what network members are saying"). 143 assets against 55 affiliates posting continuously on self-serve is thin roster coverage regardless of pass rate — that's a legitimate, separate justification for more review bandwidth, tied to the "roster coverage" KPI, not to the 62% number.
2. **`[COUNSEL]`** — does automatic, no-human-touch approval itself carry exposure independent of downstream review volume? The FTC's guidance treats "guide, then monitor, then remediate" as three non-optional duties; an auto-approve flow with no guidance step at all (step 1–2 of the FTC checklist) may be the actual gap regulators would notice first, ahead of your review throughput. Worth a compliance-counsel read before the budget conversation, since fixing it (a gate or acknowledgment step at application) is cheaper than a hire and closes a duty this skill treats as mandatory, not optional.
3. **`[COUNSEL]`** — for the 30 repeat affiliates, check whether program terms back withholding commission or requiring a wording-bank acknowledgment before further payout; if they don't, that's a terms gap this skill can't close (see `affiliate-program-terms` sibling skill), and it caps what "remediation" can require of them going forward.

## Recommendation to bring instead of the as-written request

Lead with: adapt the wording bank into your approved lines (1 hour) + stand up an automated scan for these three patterns (~1 week) + a one-time terms/gate check with counsel on the auto-approve flow. Bring the second-reviewer ask as a *smaller* coverage request once the scan is filtering the catalogued 55%, framed against roster coverage (55 affiliates, review cadence) rather than against the 62% number — that number will move on its own once the upstream fix lands, and using it to justify headcount will look wrong in hindsight when it does.