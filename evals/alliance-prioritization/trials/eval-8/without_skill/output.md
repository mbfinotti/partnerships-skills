# Alliance Scorecard v2 — Process Redesign for the FY Plan Re-Run

## What actually broke last time

The scorecard didn't fail on math — it failed on sequencing. Weights were set (by you, alone) *after* you already had a point of view on the ranking, then presented as a finished number. The CRO couldn't tell whether "integration depth" outweighed "account overlap" because you believed it or because the room had agreed to it. Once someone can plausibly say "made up," 90 minutes of argument is the correct outcome, not a malfunction.

Two things need fixing before candidate 8 (this quarter, then every quarter after):

1. **Weights must come from the committee's own stated judgments, not from you** — collected before anyone sees candidate data, so no one can suspect the weights were reverse-engineered to fit a preferred answer.
2. **The two arguments must never happen in the same room at the same time**: "what matters" (weighting) and "who scores well" (candidate evaluation) are different debates. Mixing them is exactly how a scoring fight turns into a philosophy fight.

Everything below separates those two steps and makes the weighting step itself defensible.

---

## Step 0 — Pin the objective sentence (15 min, async, before anything else)

Before criteria, before weights: get one sentence signed off — what is this hire supposed to do for the FY plan? "Alliance manager who expands ARR through existing accounts" and "alliance manager who opens new logos through partner co-sell" produce *legitimately different* weightings on integration depth vs. account overlap. Part of last quarter's fight may have been two people optimizing for different objectives without realizing it.

**Action:** send the CRO + committee one sentence: *"For these 4 hires, we are optimizing for: ___."* Get explicit agreement or edits before Step 1. Do not proceed without this.

---

## Step 1 — Criteria definitions with observable indicators

Vague criteria are what let "made up" stick. Every criterion needs a definition anyone could score the same way independently. Draft (adjust to your real list — you mentioned at least these two):

| Criterion | Definition | Observable evidence |
|---|---|---|
| Integration depth | Technical/co-sell infrastructure already live between the two orgs | # of live API integrations, joint deal desk existing (Y/N), co-sell motion documented, months since last joint GTM activity |
| Account overlap | Overlap between the alliance's customer base and our target segment | % of their top-200 accounts matching our ICP list, # of shared existing customers, overlap direction (expansion vs. cannibalization risk) |

Do this for every criterion in the scorecard (likely 5-7 total). If a criterion can't be given an observable indicator, it's an opinion wearing a criterion's clothes — cut it or merge it.

---

## Step 2 — Weight elicitation: pairwise, individual, before the meeting

Don't ask people to "assign 100 points across 6 criteria" cold — that's where numbers get "made up," because people anchor on gut feel with no forcing function. Use **pairwise comparison** instead: for every pair of criteria, each committee member (CRO included) answers only "which matters more for our Step 0 objective, and how much — slightly / moderately / strongly?"

- With 6 criteria that's 15 pairs — a 10-minute form, done **individually, asynchronously, before the meeting**. No one sees anyone else's answers.
- Aggregate via geometric mean per pair, then derive weights (standard AHP eigenvector step, or an off-the-shelf pairwise-comparison calculator — 15 pairs, trivial in a spreadsheet).
- Compute a **consistency ratio** on each person's answers. This is the single biggest defensibility win: it tells you (and can tell the room) whether someone's own judgments were internally coherent, independent of whether you agree with them. "Your own answers imply integration depth > overlap > overlap > integration depth" is a self-inflicted objection, not one you have to win against them.

**Why this fixes the CRO problem specifically:** the weights are now provably the aggregate of the CRO's own stated comparisons, plus everyone else's. If the CRO objects to the resulting weight on integration depth, the objection is now "I want to revise my own pairwise answer," which is a 30-second fix, not a re-litigation of the whole scorecard.

---

## Step 3 — Surface disagreement before the meeting, not during it

After aggregating, look at variance across committee members per criterion. If the CRO's implied weight on a criterion is far from the group's, that's a **known, named disagreement** you bring into the room deliberately — as its own 10-minute agenda item, resolved by discussion and re-vote, before candidates are ever mentioned. This replaces an ambush ("why does the scorecard say X") with a scheduled decision.

**Pre-read, sent 3+ days before the meeting:** aggregated weights, each person's individual weights (anonymized if you think that gets more honest input, attributed if you want accountability — pick one and be consistent), and the 1-2 disagreements flagged for discussion.

---

## Step 4 — Score candidates against evidence, not impression

Once weights are locked (end of Step 3, still before scoring), score each of the 7 candidates 0-4 per criterion using **anchored rubrics** (write what a 0, 2, and 4 look like per criterion, in advance — same idea as Step 1's indicators but for scoring, not weighting). Every score needs a one-line evidence citation. No naked numbers — "3, because 4 of their top 50 accounts overlap our ICP list (source: partner CRM export, dated)."

Whoever fills this in should ideally not be you alone — split across 2 people who know the candidates operationally, then reconcile disagreements >1 point before the meeting.

---

## Step 5 — Sensitivity analysis (this is what actually stops the re-open)

Before the meeting, run the ranking under:
- The locked weights.
- ±20% perturbation on each weight, one at a time.
- Each individual committee member's own weights (not just the aggregate).

Report: **which candidates are in the top 4 under every one of these scenarios (stable), and which are only in/out near the cutline (contested).** If candidate #4 and #5 swap depending on whose weights you use, say that explicitly rather than presenting a single ranked list as false-precision. This is the difference between "the model says X" (attackable) and "X is robust to every reasonable disagreement about weights, and here's the one seat that genuinely depends on a judgment call the committee needs to make live" (defensible, and turns the CRO into a participant in the one decision that's actually contestable, instead of a critic of the whole exercise).

---

## Step 6 — The meeting itself (re-run, 6 weeks out)

Agenda, in order, time-boxed:
1. Reconfirm Step 0 objective sentence (2 min — usually a formality, occasionally not).
2. Resolve the named weight disagreements from Step 3 (10-15 min, hard cap).
3. Present locked weights + sensitivity summary — stable top-4, contested seat(s) if any (5 min).
4. Discuss only the contested seat(s), with evidence, not the whole list (remaining time).
5. Sign-off, recorded.

Nothing about criteria or weights should be discussed after step 2 closes. If someone tries to reopen a weight during candidate discussion, that's now visibly out of process — point back to the pre-read they had 3 days to comment on.

---

## Making it stick beyond this cycle

- **Freeze the weights for 2-3 review cycles.** Re-litigating weights every quarter recreates last quarter's fight on a schedule. Weights get reopened only via an explicit "reopen weighting" request, itself a scheduled agenda item, not a walk-in objection.
- **Version the scorecard.** One doc: objective sentence, criteria + indicators, locked weights with the pairwise data behind them, consistency ratios, scoring rubric anchors. Every future portfolio review starts from this doc and only touches Step 4 (score new candidates) unless weighting was explicitly reopened.
- **Keep the disagreement log.** Each cycle, log who disagreed on what and how it was resolved. After 2-3 cycles this becomes the strongest evidence that the process — not any one person's preference — is producing the ranking.

The core shift: last quarter, the scorecard was *your* argument that the committee could accept or reject. This version is *the committee's* argument (specifically, provably including the CRO's own stated judgments) that you're just running the math on. That's what a CRO can't call "made up" a second time — they'd be objecting to their own pairwise answers.