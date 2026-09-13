I can't build the tile you described as stated. Two things need to change first, both hard rules in the affiliate-performance-dashboard skill, not stylistic preferences:

**1. $2.1M + $3.4M = $5.5M is a banned sum.** Sourced and influenced are reported as two separate, capped numbers, never added. Reasons that matter for a board room specifically:

- Any deal that qualifies as both sourced and influenced gets counted twice in your $5.5M — sourced takes precedence, influenced drops for that deal.
- Influenced ARR is a directional advocacy metric (a partner touched a deal originated elsewhere), not bookable revenue with the same evidentiary weight as sourced. Blending them into one number borrows credibility the influenced half hasn't earned.
- This exact move — sourced+influenced summed — is the single most common failure mode in affiliate/partner reporting decks. A board member who has seen a partner deck before will ask "is that double-counted?" and there needs to be a clean answer.

**2. I don't know if $2.1M/$3.4M are validated.** If your CRM number includes pipeline, unvalidated deals, or gross bookings rather than closed-won/validated ARR, the tile overstates. Flagging as an open item below — confirm before Thursday.

Here's the exec-view spec instead of the single tile.

---

```
EXEC VIEW - <program> partner-attributed ARR (board deck)
Source of truth : CRM, reconciled to billing where possible
Period          : trailing 12 months, validated/closed-won only, USD

TOP ROW (KPI tiles, each = value + delta vs stated prior period):
+----------------------+----------------------+----------------------+----------------------+
| NET PROGRAM          | COST OF SALE         | PARTNER-SOURCED ARR  | TOP-5 PARTNER        |
| CONTRIBUTION          |                      |                      | CONCENTRATION        |
| [NEEDS FEE DATA]      | [NEEDS FEE DATA]     | $2.1M                | [NEEDS PARTNER-LEVEL |
|                       |                      |                      |  BREAKDOWN]          |
+----------------------+----------------------+----------------------+----------------------+

SECOND ROW (paired tiles, visually distinct, never merged into one number):
+---------------------------------------+----------------------------------------------+
| PARTNER-SOURCED ARR                    | PARTNER-INFLUENCED ARR                        |
| $2.1M  (solid tile — bookable,         | $3.4M  (dashed border / "directional" label — |
| partner originated the deal)           | partner touched a deal sourced elsewhere)     |
+---------------------------------------+----------------------------------------------+
Caption under this row: "Reported separately per partner-performance standards.
Never summed — a deal counted as sourced is not also counted as influenced."
```

**Metric rows:**

| Metric                                | Definition                                                                                           | Tier                            | Target                                                           | Status                                               |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------- |
| Partner-sourced ARR                   | Trailing-12mo ARR from deals the partner originated, normalized to annual, validated/closed-won only | Floor (Business)                | growth trend                                                     | Ready: $2.1M                                         |
| Partner-influenced ARR                | Trailing-12mo ARR from deals a partner touched but didn't originate, same validation basis           | Menu (Business, capped display) | n/a — directional only                                           | Ready: $3.4M, pending validation confirmation        |
| Net program contribution              | Attributed net revenue − (commission + network/agency/placement fees)                                | Floor (Business)                | > $0 and growing                                                 | **Blocked** — no fee/commission spend given          |
| Cost of sale                          | (Commission + all fees) / attributed net revenue                                                     | Floor (Business)                | ≤ 25–30% typical for agency-heavy B2B [DERIVE from your history] | **Blocked** — same gap                               |
| Top-5 / top-10% partner concentration | Top-5 (or top-decile) validated revenue ÷ total program revenue                                      | Floor (Health/risk)             | flag if top-5 > 50% of revenue                                   | **Blocked** — no per-partner revenue breakdown given |

Concentration is not optional for your program shape specifically: ~250 partners that are mostly agencies and consultancies is a classic setup for a small number of large agency partners driving a disproportionate share. If that's true here, the board needs to see it next to the $2.1M/$3.4M, not after the fact — an agency exit can remove a double-digit percentage of sourced ARR in one quarter.

**Why the other two tiles are blocked, not omitted:** Net program contribution and cost of sale are floor metrics — the spec can't pass its own threshold without them — but I have no commission spend or fee figures from you, and no per-partner revenue table to rank concentration. They're placeholders with the formula already resolved, not decoration; drop in the two numbers (total commission+fees paid this year, and a per-partner revenue list) and the tiles compute themselves.

**Open items (surface these on the deck or resolve before Thursday):**

1. Confirm $2.1M and $3.4M are validated/closed-won, not pipeline or gross bookings — gross reporting is the single most common way these decks overstate the program.
2. Confirm the sourced/influenced split already applies sourced-precedence (no deal double-counted) — if your CRM computed these independently, they may already overlap.
3. Commission + network/agency fees for the year — needed for net program contribution and cost of sale, both board-level "is this profitable" questions.
4. Per-partner ARR breakdown — needed for top-5 concentration, the other board-level risk question ("who drives this, and what if they leave").
5. What counts as "influenced" in your CRM (touch within X days, any activity logged, etc.) — state it under the tile in one sentence; an undefined influenced metric collapses under one hard question from the board.

If items 3–4 can't be pulled by Thursday, ship the deck with sourced ARR ($2.1M) and influenced ARR ($3.4M) as the two capped tiles and a one-line note under Net Contribution/Cost of Sale/Concentration: "pending finance data, next update." That's a defensible partial deck. The summed $5.5M tile is not — it's the one number in this whole exercise a sharp board member is likeliest to unwind live, and it unwinds badly.
