## Payout review — Thistlewood Home, February

Three separate issues here, and the first one alone likely invalidates the $31,406.18 number.

### 1. You're adding two overlapping measurements, not two independent counts

1,904 (network, 7-day window) + 1,671 (in-house, 30-day window) = 3,575 treats these as separate conversions. They're not — they're two different systems measuring the _same_ underlying purchases with different attribution windows. A 30-day tracker will naturally re-catch a large share of what the 7-day network export already caught, plus some conversions the network's shorter window missed entirely.

- Summing them double-counts every conversion both systems agree on.
- The correct number is a **deduplicated union**, found by matching individual conversions (order ID, customer ID, or click ID) between the two exports — not by adding aggregate totals.
- Depending on real overlap, true unique conversions could be anywhere from ~1,904 (if in-house is almost fully a subset) to 3,575 (if the two systems tracked almost disjoint sets — unlikely given they're watching the same store).

### 2. The payout is probably inflated, possibly by a lot

$31,406.18 / 3,575 ≈ $8.79 per conversion. If real overlap is high and unique conversions land closer to ~1,900–2,200, the correct payout is roughly **$16,700–$19,300** — nearly half what you're about to release. You won't know the real number until you dedupe at the conversion level.

### 3. The $2,900 gap is not noise

$28,500 vs $31,406.18 is a ~10% variance on a five-figure payout. "Normal tracking noise" is a label, not an explanation — and it happens to point the same direction as issue #1 (your spreadsheet estimate is closer to reality because it's less exposed to the double-count). Reconcile it as a line-item difference (which conversions are in the calculated run but not the spreadsheet, and vice versa) before treating it as acceptable drift.

### Before you hit release Friday

1. Pull raw, conversion-level exports (not aggregates) from the network and the in-house tracker for February.
2. Match records by order ID / customer ID / click ID across both sources.
3. Compute the deduplicated unique conversion count and the actual overlap rate between systems.
4. Recompute the payout on that deduplicated count.
5. Reconcile the $2,900 gap explicitly against the dedup output — it should mostly disappear once double-counting is removed.
6. Report the exec team the **deduplicated** conversion count, not 3,575 — footnote the two raw source counts and the overlap % for transparency.
7. Have one other person on the team review the reconciliation output before you release the payment. Four-person team is exactly why this matters: there's no one else in the loop today, and this is money leaving the company.

Going forward, write the dedup logic down somewhere durable (this repo's `memory/` or a program-specific note) so next month isn't a from-scratch reconciliation.
