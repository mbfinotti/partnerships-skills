# Concentration Addendum — Ravencourt Outdoors Affiliate Program

Note upfront: this is a partial deliverable, not a full dashboard spec — you gave me the two concentration decisions to answer, not full Interview answers (audience, validation window, active-partner definition, data sources). I've built what those two questions need and listed the rest under Open items rather than guessing at a full spec. No canonical affiliate-dashboard framework exists for any of this; treat every "VENDOR"/"SYNTH" tag below as calibration, not a standard.

## 1. The commission cap: don't throttle the top partner

Direct answer: **don't cap it as a blunt lever.** The prescribed response to a concentration breach is partner development in the next tier down plus top-partner retention work — not throttling the top partner. You're already past the working threshold that defines a breach (**top-5 partners over 50% of revenue** — you're at 61%), so the trigger is real, but the fix that trigger calls for is different from the one you're proposing.

Why not just cut their rate:
- A super-affiliate at 38% of validated revenue is your single largest revenue-concentration risk. Vendor data pegs the impact of **losing** a top affiliate at a 15-25% program revenue cut — cutting their commission is a softer version of the same risk: they can reprice their own placement toward a competitor program without you seeing it coming until volume drops.
- Commission architecture (what to pay, tiered curves, caps) isn't this skill's call — that's `affiliate-commission-structure`. What this dashboard *can* do is instrument the decision properly if you still want to test a reduction:
  - Run it as a **monitored test, not a silent cut**: change terms with this one partner, then watch their EPC, click-to-conversion, and reversal rate against their own rolling baseline (not the program average — their volume alone will swing it).
  - Track whether their *volume* migrates elsewhere (falling clicks/impressions on your program) vs. just their *conversion economics* changing — the first is the retention risk materializing, the second is a normal repricing response.
  - Put a named decision date and owner on the test. An open-ended "reduced rate" with no readout is how these quietly become permanent without anyone checking if it worked.
- Meanwhile, spend the actual effort on tier 2-5 (the other four names inside your 61%) and the tier below them: recruit/activate pushes, tail-activation work, and partner-type mix diversification are what structurally reduces concentration — the cap doesn't, it just changes who feels the squeeze.

## 2. Concentration tiles to build

**Executive view — quarterly recompute, portfolio review:**

```
+--------------------------------------------------------------------+
| TOP-1 PARTNER  | TOP-1% SHARE | TOP-5% SHARE | TOP-10% SHARE        |
| SHARE: 38% 🔴  | 38%          | 61%          | —  (compute)         |
+--------------------------------------------------------------------+
| Absolute top-5-partner share: 61% 🔴  (breach: threshold is 50%)    |
+--------------------------------------------------------------------+
```

| Metric | Definition | Tier | Viz | Target | Alert |
|---|---|---|---|---|---|
| Top-1 partner share | this partner's validated revenue / total program validated revenue, quarterly | Health | exec tile | own baseline (derive) | 🔴 breach if >30% [DERIVE from your own quarters] |
| Top-1% share | validated revenue from top 1% of *active* affiliates / total program revenue, quarterly | Health | exec tile | own baseline | — |
| Top-5% share | same, top 5% of active affiliates | Health | exec tile | own baseline | — |
| Top-10% share | same, top 10% of active affiliates | Health | exec tile | own baseline | — |
| Absolute top-5-partner share | sum of top 5 partners' validated revenue / total program revenue, quarterly | Health | exec tile, headline | <50% | 🔴 ≥50% [VENDOR threshold, band DERIVE] |

**Operator view — daily/continuous:**

| Metric | Definition | Alert |
|---|---|---|
| 1-partner share | dominant partner's validated revenue / rolling 24h-30d program revenue | 🟠 spike vs 2-SD 30-day rolling baseline, or +5pt in 7 days |

**Alerts register:**

| Alert | Threshold | Owner | Channel | Response |
|---|---|---|---|---|
| Single-partner share spike | rolling-baseline: >2 SD vs 30-day mean, or fixed +5pt/7d | Affiliate/partner manager | Chat | 24h |
| Concentration breach (top-5 ≥50%) | already firing — 61% | Program owner | Monthly/quarterly review | Named decision at next review |

All four percentile tiles recompute quarterly, same "active" definition every time, or the trend is fake. Rank order for build effort if you're phasing this in: **absolute top-5-partner share first** (you already have the number and it's already breached), then top-1%/top-5%/top-10%, then the daily single-partner operator tile + alert last (needs a rolling-baseline job, not just a quarterly query).

Report **validated**, never gross, revenue in every one of these — you already said "validated revenue" for the 38%/61%, so you're aligned on that already.

## 3. Sub-networks: no, don't split them

Direct answer: **no.** Splitting a sub-network into its underlying publishers to make the concentration numbers look better is exactly the failure mode this method calls out: *"Sub-network counted as many partners → partner counts and concentration both distorted → count one credited entity per conversion; break out sub-networks separately."* Doing it *because* it improves the optics is choosing the distortion on purpose, not fixing a data problem.

What to actually do instead:
- Keep each sub-network as **one row** for concentration, active-partner count, and commission/payment purposes — that's the entity you contract with and pay, and it's the credited entity per conversion.
- If your platform can see individual publisher IDs *underneath* the sub-network, build a **separate internal breakdown view** for that sub-network alone (its own mix, its own top publishers) — useful for understanding what's driving it, but this supplements the top-line concentration numbers, it never replaces them.
- This also means your true concentration picture might be worse than 38%/61% look, not better: if any of those top-5 rows *is* a sub-network, its hundreds of publishers are aggregated demand you don't have visibility into, sitting behind one commercial relationship. That's a bigger single point of failure than a single affiliate with the same share, not a smaller one — worth flagging on the exec view as a footnote against that partner's row ("sub-network — N sub-publishers") rather than hiding it.

## Open items

- Which of the top-5 (or the 38% partner) are actually sub-networks — flag them on the leaderboard, don't just fold them into "partner."
- "Active affiliate" definition undefined — the top-1%/5%/10% denominator depends on it; pick one (e.g., ≥1 validated order in 60 days) before the first quarterly recompute.
- Validation window and clawback policy not stated — needed before comparing this quarter's 38%/61% to any future quarter.
- Program size, commission model (flat CPA vs tiered), and who reads this (exec vs operator vs both) not stated — needed to size the rest of the dashboard beyond this concentration slice.
- Commission-cap decision itself: routing to `affiliate-commission-structure` for the actual rate design, since this skill instruments the test, it doesn't set the rate.