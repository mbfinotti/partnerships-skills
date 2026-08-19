# Alliance Prioritization Memo — Hanmere Group Partnership Candidates

**Note on method before the memo:** the skill this runs on (`alliance-prioritization`) is built as an interview-then-rank process — normally I'd ask about goal, capacity, data availability, and portfolio context one question at a time before scoring anything. You asked for the finished deliverable in one shot, so below I state the assumptions I had to make in place of those answers, flag every input I don't actually have evidence for, and still run the full method rather than skip steps. Treat the assumptions and open questions as the first thing to correct, not fine print.

**Assumptions made in place of the interview:**
- Strategic goal: hybrid — B2B pipeline into banks (risk-engine licensing) **and** B2C incremental revenue/distribution (consumer app). Confirm which one dominates; it changes the weight split.
- Portfolio cadence: treated as a compounding asset (a scorecard you'll re-run), not a one-off — because the list mixes B2B and B2C, not because you said so.
- Capacity: 9 alliance-manager-months, as given. This is manager capacity, separate from the 5 engineer-months quoted for Ostrander, which is a build cost, not alliance-manager load.
- Only two candidates arrived with real names and real facts (Ostrander, Verrow Athletic). The other bank-side tech alliance and the second consumer co-brand are scored as placeholders below — **that scoring is illustrative, not decision-grade.** See Open Questions.

---

## Candidates (5 considered)

| # | Candidate | Type | Status entering scorecard |
|---|---|---|---|
| 1 | Ostrander | B2B tech alliance | **Removed at pre-filter** — wrong mode, see below |
| 2 | Bank-Side Tech Alliance B *(name withheld/unprovided)* | B2B tech alliance | Scored |
| 3 | Verrow Athletic | B2C co-brand | **Removed at gate** — brand safety fail |
| 4 | Consumer Co-Brand B *(name withheld/unprovided)* | B2C co-brand | Scored |

Only 2 of 5 candidates reach the scorecard. That's not a thin result — the other three were correctly decided at earlier, cheaper stages, which is what staging is for.

---

## Pre-filter: ally vs. acquire vs. build (Dyer, Kale & Singh, 2004)

**Ostrander — removed here, before any gate or score.**

The whole synergy on offer is one model you could rebuild in ~5 engineer-months. Run the test the method requires before treating "partnering is faster" as the answer:

- **What an alliance would cost you that build doesn't:** a permanent dependency on a single-product shop, inside the exact capability (the risk engine) you license to banks as your core product. That's not a peripheral integration — it's outsourcing part of what you sell.
- **Viability exposure:** "small analytics shop, one product" is close to the textbook profile the financial-viability gate exists to catch. Even under an alliance, you'd need to clear that gate — and a single-model vendor concentrates your risk exactly where the gate is most sensitive.
- **Speed is the only argument for ally**, and it's real — but 5 engineer-months is a one-time, bounded cost that ends in owned IP and no royalty stream. An alliance here is recurring cost plus dependency, for a capability gap you can close yourself in under half a year.

**Verdict: build.** Removed from the alliance list, not scored. This is the correct target for `mbfinotti/partnerships-skills@partner-economics` if you want the build-cost/license-cost math spelled out, not for this ranking.

**Exception that would flip this:** if there's a specific bank deal on the table this quarter that dies without Ostrander's model live before your build finishes, that's a licensing bridge, not a strategic alliance — score it as a short, capped, conditional-go with an explicit sunset date tied to your own build's ship date, never as a flagship candidate. I don't have evidence of that urgency; flagged below as an open question.

---

## Must-pass gates (run in full, on all 5 — see note)

Gate-strictness call: the default is staged (desk gates on the whole longlist, expensive reviews only on survivors). With 5 candidates, staging barely saves anything, so I ran the full set on everyone rather than defaulting to staged.

| Candidate | Financial viability | Security/compliance | Legal/antitrust | Brand safety (B2C) | Three-laws | Exit path | Result |
|---|---|---|---|---|---|---|---|
| Ostrander | — | — | — | n/a | — | — | Removed at pre-filter, not gated |
| Bank Alliance B | Assumed pass *(unverified)* | Assumed pass *(unverified)* | Assumed pass *(unverified)* | n/a | Assumed pass *(unverified)* | Assumed pass *(unverified)* | **Provisional pass** |
| **Verrow Athletic** | Pass | Pass | Pass | **FAIL — unresolved supply-chain labor controversy** | n/a | n/a | **Gate failure — removed** |
| Consumer Co-Brand B | Assumed pass *(unverified)* | Assumed pass *(unverified)* | Assumed pass *(unverified)* | Assumed pass *(unverified)* | Assumed pass *(unverified)* | Assumed pass *(unverified)* | **Provisional pass** |

### On the finance lead's suggestion (15% deduction for Verrow Athletic's brand risk)

**Rejecting this, explicitly.** The brand-safety gate is defined as pass/fail specifically because it fails when there's "an unresolved brand-safety flag, active controversy, or values conflict" — and "unresolved" is your own word for the labor story. Averaging it into the composite as a 15% haircut does three things wrong at once:

1. It trades a gate against a score, which is the named failure mode this method exists to prevent ("a SOC 2 failure is not worth any number of scorecard points" — the same logic applies to an unresolved labor controversy).
2. It lets Verrow's genuinely strong pipeline number (best of the five, by your account) buy back points that a pass/fail issue shouldn't be able to buy back at any price.
3. For a **consumer finance app**, the contagion channel runs in a direction worth naming: co-branding research (Simonin & Ruth, 1998) finds brand-pairing attitudes spill over onto both partners, and the spillover isn't symmetric — the more "trust brand" you are, the more exposed you are to a partner's unresolved controversy, not less. Finance is a trust-sensitive category. That argues for taking this gate *more* seriously here, not softening it.

Verrow Athletic does not get scored. It gets a gate failure and a re-entry trigger (below), full stop.

---

## Scorecard (survivors only: 2 candidates)

Weight distribution: **type-segmented**, not the plain-justified default — the list mixes a B2B tech alliance and a B2C co-brand, and the method explicitly says these must never share one weight set. Complementarity/compatibility still anchor both sets, per the only fit construct with peer-reviewed support.

### B2B tech alliance criteria (Bank Alliance B)

| Criterion | Weight | Justification |
|---|---|---|
| Resource complementarity | 25% | Highest-weighted by design — the only fit construct with independent replication |
| Organizational compatibility | 20% | Same anchor construct; bank deal cadence is where integrations usually die |
| Goal fit (pipeline to banks) | 15% | Direct line to the licensing side of the business |
| JVP strength | 15% | Ties with alliance readiness — value story and delivery capability are both necessary, neither substitutes |
| Alliance readiness | 15% | Same rationale as above |
| Verified overlap | 10% | Capped by design — overlap flags warm accounts, doesn't predict success |

### B2C co-brand criteria (Consumer Co-Brand B)

| Criterion | Weight | Justification |
|---|---|---|
| Brand fit / attitude congruence | 25% | B2C analog of complementarity; the only B2C fit construct with peer-reviewed backing |
| Compatibility (marketing cadence) | 15% | Lower than B2B because co-brand campaigns are shorter-cycle than integration work |
| Goal fit (consumer app growth) | 15% | Direct line to distribution goal |
| JVP strength | 15% | Same necessity logic as B2B set |
| Alliance readiness | 15% | Same |
| Verified audience overlap | 15% | Capped, but weighted slightly above the B2B set — reach is closer to the actual currency in B2C |

### Scores (1–5, evidence-anchored where possible)

| Candidate | Complementarity/Brand fit | Compatibility | Goal fit | JVP | Readiness | Overlap | **Composite** | Effort (mgr-mo) | **Value ÷ Effort** |
|---|---|---|---|---|---|---|---|---|---|
| Bank Alliance B | 4 *(GUESS)* | 3 *(GUESS)* | 4 *(GUESS)* | 3 *(GUESS)* | 3 *(GUESS)* | 3 *(GUESS)* | **3.55** | 4 | **0.89** |
| Consumer Co-Brand B | 3 *(GUESS)* | 4 *(GUESS)* | 3 *(GUESS)* | 3 *(GUESS)* | 4 *(GUESS)* | 3 *(GUESS)* | **3.30** | 3 | **1.10** |

Every score above is marked GUESS because I have no evidence file, closed-won sample, or audience audit behind either unnamed candidate — only category labels. **Do not take this table into a sign-off meeting as-is.** It exists to show the mechanics correctly; it is not decision-grade until real scores replace the guesses.

**Risk composite:**
- Bank Alliance B: risk not assessed — no data on roadmap dependency or platform terms was supplied.
- Consumer Co-Brand B: risk not assessed — no audience-fraud or reputational-contagion screen was supplied.

Both need the Das & Teng relational/performance pass and, if either sits on a partner's platform, the envelopment check, before this ranking is final.

---

## Sensitivity (±20% per weight, one at a time)

With only two survivors and a 0.21 gap in value÷effort (0.89 vs 1.10 — outside the ~5% tie-band), a ±20% shift on any single weight in either set doesn't have room to flip the order on the numbers as given. **This is a weak sensitivity result, not a strong one** — it's stable because the inputs are guesses with a wide gap, not because real data was stress-tested. Re-run this once actual scores land; a real gap that size would be meaningful, an illustrative one isn't.

---

## Capacity line (9 alliance-manager-months)

Effort-sum: Bank Alliance B (4) + Consumer Co-Brand B (3) = 7 of 9 manager-months. Both fit inside capacity with 2 months of headroom — no candidate needs to be cut on capacity grounds this round. The headroom is exactly enough to absorb a small conditional-go scope for Ostrander *if and only if* a real deal urgency shows up (see Open Questions) — do not pre-spend it.

---

## Shortlist

| Candidate | Verdict | First-value milestone | Owner | Gate date |
|---|---|---|---|---|
| Bank Alliance B | **Conditional-go** — pending real scorecard data | Integration live + first joint bank opportunity | TBD | Re-score within 2 weeks |
| Consumer Co-Brand B | **Conditional-go** — pending real scorecard data | Co-brand campaign live + attributed-revenue baseline | TBD | Re-score within 2 weeks |

Both are conditional-go rather than go, because a go on guessed scores is exactly the false precision this method exists to prevent. The condition is identical for both: replace the GUESS cells with real evidence, then confirm the ranking holds.

---

## Below the line

| Candidate | Verdict | Reason | Re-entry trigger |
|---|---|---|---|
| Ostrander | **Kill (as an alliance)** | Wrong mode — build dominates on IP control, cost, and dependency risk for a 5-engineer-month capability that sits inside your core licensed product | Only reopens if a named bank deal requires the capability before your own build ships — then it's a capped, dated bridge license, not a strategic alliance |
| Verrow Athletic | **Recycle** | Gate failure (unresolved brand-safety controversy), not a fit or value problem — it has the strongest pipeline contribution of the five | Independently verified resolution of the labor story (third-party audit or certified remediation — not a press statement) triggers immediate re-score, given its pipeline strength |

---

## Open questions (mandatory — this ranking is not final without these)

1. **Real names and data for Bank Alliance B and Consumer Co-Brand B.** Everything scored above them is a guess; the ranking between them is illustrative only.
2. **Is there a live bank deal that needs Ostrander's model before your own build (≈5 engineer-months) ships?** This is the one fact that would flip Ostrander from "kill" to "capped bridge license."
3. **What counts as "resolved" for Verrow Athletic?** Define the evidence bar (independent audit vs. company statement) now, before the campaign team lobbies to call it resolved informally.
4. **Single dominant goal or genuine hybrid?** If pipeline-to-banks is actually the priority over consumer distribution, the B2C co-brand's weight set — and its place in this round's 9 manager-months — should be revisited.
5. **Account-overlap and audience-overlap data** — none was supplied; both overlap scores above are capped guesses, not the 10-15% they're weighted at.

---

## Next portfolio review

Re-run this ranking the moment any of these fire: real data lands for the two unnamed candidates, Verrow Athletic's labor story resolves (or escalates), or a bank deal creates urgency on Ostrander. Otherwise, review on the standard quarterly cadence.