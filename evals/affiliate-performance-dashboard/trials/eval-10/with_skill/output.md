## Straight answer for your VP conversation

**There is no named framework to give her — and citing one would burn credibility the first time someone checks.** The skill I used to build this response says so explicitly: no standards body (IAB, PMA — trade bodies only) has ever standardized affiliate metric definitions or published a canonical "framework." Anything sold to you as one is a vendor or consultant's branding exercise. If she wants a name in the room, don't invent one — cite the one piece of this that _is_ real and named:

> **Croll & Yoskovitz's tiered metric hierarchy** (from _Lean Analytics_), applied to affiliate reporting — business/headline tier → input/driver tier → health/guardrail tier — with every metric screened against their four good-metric criteria: comparative, a ratio or rate, understandable, and behavior-changing.

Layered under that name, three more borrowed (also real, also citable, not one unified "brand"): incrementality measurement (holdout/geo-lift), the attributed-ROAS-vs-ROI split, and a sourced-vs-influenced separation rule. Say it as "a tiered metric hierarchy, Lean Analytics-style, with incrementality and ROAS/ROI discipline built in" — that's honest and it's still a name she can repeat.

## Your current KPI set is the textbook failure case

Total clicks, affiliate signups, and gross commissions are, almost verbatim, the anti-pattern this method calls out first:

| Your current KPI                  | Why it fails                                                                                                                                                                                                                                                                       |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Total clicks (1M/mo target)       | Vanity metric — informs no decision. Diagnostic at best, never a headline.                                                                                                                                                                                                         |
| Affiliate signups (200/mo target) | Same problem — a count, not a rate; tells you nothing changed in behavior.                                                                                                                                                                                                         |
| Gross commissions earned          | The single most common practitioner error. Gross is always the bigger, flattering number — it hides reversals, clawbacks, and hasn't been validated. Reporting it instead of validated/approved commission makes the program look cheaper and more productive than it actually is. |

## What to present instead

**Headline tier (what she sees first, what answers "is this program profitable and who drives it"):**

1. **Net program contribution** — `attributed net revenue − (validated commission + network fees + agency fees + placement fees)`. This is the actual profitability number; nothing else belongs above it.
2. **Cost of sale / commission-to-revenue** — `(validated commission + network + agency + placement fees + bonuses) / attributed net revenue`. Forces every hidden fee into the number gross commissions was hiding.
3. **Top-N partner concentration** — top 1%/5%/10% of active partners' share of validated revenue. Board-level risk metric: one partner's exit shouldn't be able to erase the program unseen.
4. **Partner-sourced MRR/ARR** — only if this is a B2B/recurring-commission program; skip for pure B2C.

**Demote, don't delete:** clicks and signups move to the input/driver tier as diagnostics ("is traffic volume healthy") — never headline, never a target with a bonus attached to it. Gross commissions gets replaced by **validated/approved commission**, with pending shown separately, never summed in.

One honest caveat to give her along with this: which exact metrics populate the floor beyond those three universal ones (and how they're sliced — by partner, partner type, geography) depends on your program type and data maturity — B2B SaaS vs. B2C ecommerce, validation window, whether partner ID reaches billing. If you want the full dashboard spec (not just the headline set for this meeting), that's a short follow-on conversation, not more work on your end today.
