## What's wrong with the current slide

**87% approval rate is the wrong headline, and it's also mis-computed.** 120 approved / 140 applications = **85.7%**, not 87% — small, but worth fixing before it goes on a slide.

More importantly, per this skill's own guidance: *"Applications and approvals alone are vanity metrics — a recruit who never promotes cost you the outreach and returned nothing."* Your platform dashboard shows approvals and payouts because that's a program-health view, not an outreach-effectiveness view. Pulling only from it means you're reporting how generous your approval process is, not whether recruitment worked.

## What to report instead

Report the full outreach funnel, not one ratio pulled from the middle of it:

| Stage | Count | Rate | Base |
|---|---|---|---|
| Contacted | 640 | — | — |
| Applied | 140 | 21.9% | of contacted |
| Approved | 120 | 18.8% / 85.7% | of contacted / of applied |
| **Activated** (≥1 click or sale in-quarter) | **?** | **?** | of approved |

The last row is the one missing, and it's the actual KPI that matters. Applications and approvals measure your funnel and your review process; activation measures whether recruitment produced anything. Pull it from the affiliate platform: for each of the 120 approved this quarter, check whether they generated at least one click or sale within 30/60 days of approval. Report that share. The skill's practitioner benchmark for a mature program is **~20% of affiliates producing ≥1 click/week** — self-reported, not independently measured, so cite it as context, not as a target you're graded against.

Two more things worth putting on the slide, both computable from what you already have:

- **Application rate (21.9% of contacted)** is a better read on list quality and pitch fit than approval rate is. Cold-outreach reply-rate norms run **3–9%** (verified study, general cold outreach, not affiliate-specific) — a 21.9% application rate off 640 contacts is genuinely strong, assuming "contacted" means a real first-touch send and not just a list size. Frame it that way instead of leading with approvals.
- **Segment the 21.9% and the 85.7% by tier and by which pitch angle/touch got the reply**, if you tracked that. Aggregate rates hide whether it was tier-1 personalization or a mass send that drove the numbers — you can't repeat what you can't attribute.

## How to track this going forward

Keep the outreach pipeline in a CRM or spreadsheet, separate from the platform dashboard — the platform will never show you "contacted" or "replied," only "applied" onward:

**Columns:** prospect, tier (1/2/3), segment/jurisdiction, date contacted, touch # and channel per attempt, angle used, reply date, applied date, approved date, first click date, first sale/commission date, status.

**Cadence:** update weekly while a campaign is active; roll it up for the quarterly review rather than starting a fresh count from the platform each time.

**Report every quarter:**
1. Funnel with rates at each stage (table above), not a single ratio.
2. Split by tier and by angle — which sourcing/personalization actually converts.
3. Activation rate of that quarter's approved cohort, checked at a fixed window (30/60/90 days) so quarters are comparable.
4. Reply/application rate against the 3–9% cold-outreach benchmark, so leadership has a reference point instead of a bare percentage.

**Don't do:** compare quarters where the activation-check window differs (a cohort checked at 30 days will always look worse than one checked at 90), or sum "applied" and "approved" into one number.

If you also want the *program-side* view — net program contribution, cost of sale, top-partner concentration, i.e. whether the whole affiliate program is profitable, not just whether this quarter's recruiting worked — that's a separate artifact (dashboard spec) from a different skill in this same skill set (`affiliate-performance-dashboard`), since it pulls from billing/orders rather than the outreach pipeline. Say the word if you want that built next; it needs its own short interview (program size, data sources, who reads it) before it can be specified.