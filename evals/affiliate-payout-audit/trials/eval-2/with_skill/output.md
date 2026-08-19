# Kestrel Analytics — Payout Re-Audit (Brightpath Media, Onda Digital)

No named framework applies here — this borrows from account reconciliation / three-way match / maker-checker, same as any commission audit. Full audit report below.

## What I could and couldn't check

You gave me a PDF statement, two summary figures, and a rate card — no platform export, no billing/CRM extract, no exact period dates/timezone, no validation-window or tax-form status. That **blocks** reconciliation, dedup, and lifecycle checks entirely (checks 2–6, 8–9 below). It does **not** block the one check that actually matters here: **rate/tier recompute (check 7)** — a partner-disputed tier promotes this to the whole audit when nothing else is reachable, which is exactly your situation.

```
PAYOUT AUDIT - Kestrel Analytics, run "last quarter" (exact dates/timezone: NOT PROVIDED)
Scope     : 2 disputed lines; proposed total $14,050; source: network PDF statement only
            (no platform export, no billing/CRM extract to reconcile against)
Checks    : 1 Freeze scope        - PARTIAL (period is "last quarter", no exact dates/tz/date-basis)
            2 Pull exports        - BLOCKED (PDF only, no machine-readable export)
            3 Comparability       - N/A (single source)
            4 Reconcile to source - BLOCKED (no source of truth extract)
            5 Exception queue     - N/A
            6 Dedupe              - N/A (no line-level detail beyond these two totals)
            7 Rate/tier recompute - DONE (below)
            8 Lifecycle state     - BLOCKED (no validation-window data)
            9 Currency/tax/thresh - BLOCKED (no tax-form status; currency assumed single)
            10 Coverage method    - 100% of disputed lines (only 2 exist to check)
            11 Report             - this document
            12 Maker-checker      - NOT YET DONE (required before any release/correction)
```

## The actual math

Rate card: 20% on referred volume up to $10,000; 25% from $10,000–$25,000; 30% above $25,000.

**Brightpath Media — $26,000 referred:**
- Marginal (each band graduated): 20%×10,000 + 25%×15,000 + 30%×1,000 = 2,000 + 3,750 + 300 = **$6,050**
- Retroactive (whole volume re-rated at top band reached): 30%×26,000 = **$7,800**
- **Paid: $7,800 → matches retroactive exactly.**

**Onda Digital — $25,000 referred, sitting exactly on the boundary:**
- Your wording — "25% from $10,000 to $25,000" and "30% **above** $25,000" — puts $25,000 itself in the 25% band, not the 30% one. So the applicable single-rate reading of $25,000 is 25%, not 30%.
- Marginal: 20%×10,000 + 25%×15,000 = 2,000 + 3,750 = **$5,750**
- Retroactive at 25% flat: 25%×25,000 = **$6,250**
- **Paid: $6,250 → matches retroactive exactly.**

Both payouts are internally consistent with each other and arithmetically correct **under one specific method: full-volume ("back-to-dollar-one") retroactive tiering, with the $25,000 boundary correctly resolved into the 25% band.** There is no off-by-one, no double-count, no arithmetic slip in either line. The platform did the retroactive math right.

## The actual finding

This isn't a bug — it's the exact ambiguity the skill flags by name: *"if the results differ and the written structure is silent, raise a finding — the structure is ambiguous, not the math."* Your rate card states three bands and three rates. It says nothing about whether crossing a threshold re-rates all prior volume or only the marginal slice. The platform picked retroactive. Most affiliate programs default to marginal specifically to avoid the cliff effect this creates (two dollars of extra volume at $25,000 would jump Onda from $6,250 to a hypothetical $7,500.30 under a mis-set boundary — you got lucky the boundary read correctly here).

**So: are these numbers "right"? I can't certify that — and neither can you — until the method is written down.** They're right for retroactive tiering. They're wrong for marginal tiering, by a specific amount:

| Partner | Paid (retroactive) | Marginal | Variance if marginal is the intended method |
|---|---|---|---|
| Brightpath Media | $7,800 | $6,050 | **$1,750 overpaid** |
| Onda Digital | $6,250 | $5,750 | **$500 overpaid** |
| **Total** | **$14,050** | **$11,800** | **$2,250 at risk** |

## Second open item: the rate card refresh

You refreshed the rate card two weeks ago. Per the skill's terms-in-force rule, last quarter's commissions must be recomputed against **whatever card was legally in force on the original transaction dates**, never today's card. I used the 20/25/30% and $10k/$25k figures you quoted — confirm explicitly whether those are the pre-refresh figures that actually applied last quarter, or the just-refreshed ones. If the refresh changed either the rates or the breakpoints, every number above needs to be redone against the old card, not this one.

## Findings

- **F-1 (material, $2,250 at risk)** — Both disputed lines were paid via retroactive tiering; the written rate card never specifies method. Not a computational error — a structural ambiguity. **Action: hold both lines from any further movement until the intended method is confirmed in writing** (correct-before-release is available and free since these are disputed/likely still-reversible, not settled facts about intent).
- **F-2 (blocker)** — Unconfirmed whether the rate card figures used here are the version in force last quarter or the version refreshed two weeks ago. **Action: confirm the historical card text before treating any of the above as final.**
- **F-3 (informational, compounding)** — If retroactive is confirmed as the platform's actual standing behavior (not a one-off), every partner who ever crossed $10,000 or $25,000 in any period has been overpaid the same way, not just these two. This is a candidate for **fix-it-forward**: write the method explicitly into the rate card regardless of which method you land on, so this stops being adjudicated per dispute.

## Variance vs materiality

Recomputed-as-marginal total $11,800 vs proposed/paid $14,050 → **$2,250 net variance**, 100% concentrated in the two disputed lines. No materiality threshold was given, so I can't score this pass/fail against your policy — you'll need to supply that number.

## Cleared for release

**Zero lines.** Both are under active dispute and the underlying method is unresolved — releasing or re-affirming either number now would be certifying an interpretation nobody has actually decided on.

## Sign-off

Preparer: this audit. Checker: must be a different person per maker-checker — not yet done, and required before any correction or confirmation goes back to either partner. Release decision: **HOLD** both lines pending (1) written confirmation of marginal-vs-retroactive intent, and (2) confirmation of which rate-card version governed last quarter's transactions.