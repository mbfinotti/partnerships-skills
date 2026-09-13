## Short answer: No — not under the reading almost everyone would assume, though the payments are internally consistent with each other.

**The math, both ways:**

_If bands are graduated (marginal), like a tax bracket — each dollar taxed only at its own tier's rate:_

| Partner              | Calculation                                           | Correct payout |
| -------------------- | ----------------------------------------------------- | -------------- |
| Brightpath ($26,000) | 10,000×20% + 15,000×25% + 1,000×30% = 2,000+3,750+300 | **$6,050**     |
| Onda ($25,000)       | 10,000×20% + 15,000×25% = 2,000+3,750                 | **$5,750**     |

_If bands are a "cliff" — the entire volume gets paid at the rate of whichever tier it lands in:_

| Partner                                 | Calculation  | Payout     |
| --------------------------------------- | ------------ | ---------- |
| Brightpath ($26,000, in the >$25k tier) | 30% × 26,000 | **$7,800** |
| Onda ($25,000, in the $10k–$25k tier)   | 25% × 25,000 | **$6,250** |

## What actually happened

The platform paid **$7,800 to Brightpath and $6,250 to Onda** — which match the _cliff_ method exactly, not the graduated one. So:

- ✅ The two payouts are consistent with **each other** (same methodology applied both times).
- ⚠️ Under the graduated reading — the standard interpretation for rate cards phrased "up to X / X–Y / above Y" — both were **overpaid**: Brightpath by **$1,750** ($7,800 vs $6,050), Onda by **$500** ($6,250 vs $5,750).

## Why this matters beyond the two invoices

The cliff method creates a hard notch at each boundary: a partner referring $24,999 earns 25% (~$6,250), but one referring $25,001 jumps straight to 30% on the *whole* amount (~$7,500) — a $1,250+ swing for $2 of extra volume. That kind of discontinuity is almost never the intent when a rate card is written as ascending bands; it's the classic tell that either the platform's calculation logic defaulted to "highest-tier-wins" instead of true tiering, or someone built it that way deliberately. Since your rate card text is silent on which model applies, neither partner is technically "wrong" to have been paid this way — but it's very unlikely to be what was intended, and it will get more expensive (and more visible) every time a partner crosses a boundary.

## One thing I can't resolve for you

The rate card was refreshed **two weeks ago**. The quarter you're re-auditing predates that refresh. Before finalizing any "correct" number, confirm whether the 20/25/30 bands you quoted are the version that was actually in force during the quarter being disputed, or the post-refresh version — comparing last quarter's payouts against the _current_ card would be the wrong baseline even if you settle the graduated-vs-cliff question. I don't have access to the pre-refresh card or the underlying PDF/ledger, so this needs to be pulled and checked before you close the audit.

## Recommended next step

Get an explicit, written ruling (not just a verbal assumption) on band combination — graduated vs. cliff — and apply it retroactively and consistently. If graduated is confirmed as intended: claw back or net against future payouts $1,750 from Brightpath and $500 from Onda, and fix the underlying calculation so it doesn't keep firing this way at every future boundary crossing.
