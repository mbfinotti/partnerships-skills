# PAYOUT AUDIT — Hollowbrook Goods affiliate program

```
PAYOUT AUDIT - Hollowbrook Goods, run [ID not provided], period [not provided] (timezone/date basis not provided)
Scope     : 2,184 lines, proposed total $31,400.00 [currency assumed USD]; sources: network conversion export vs order database
Structure : not provided - rate/tier recompute cannot be performed at line level
Checks    : 1 scope frozen: FAIL (period, timezone, date basis, materiality threshold, currency all unconfirmed) - BLOCKER
            2 exports pulled: partial (aggregate figures only, no line-level file supplied to this audit)
            3 comparability: UNRESOLVED (need confirmation both sides share event definition/date basis before trusting the 12/9 exception counts)
            4 totals reconciliation: cannot compute to the cent without line-level data
            5 exceptions: 21 one-sided records (12 + 9) - see below
            6 dedup: FAIL - 17 blank transaction IDs collapsed into 1 record
            7 rate/tier: NOT PERFORMED - no rate card or line-level export provided
            8 lifecycle/clawback: NOT PERFORMED - no validation-window or state data provided
            9 currency/tax/thresholds: NOT PERFORMED - no data provided
            10 sampling: recommend risk-based stratified once line-level data lands - 100% of F-1/F-2/F-4 lines + top earners + random remainder
Findings  :
  F-1 | blocker  | $ at risk: unrecoverable from aggregate | 17 lines (1 rolled-up record) |
        Blank transaction IDs collapsed by your analytics tool into a single record. QUARANTINE - do not release,
        do not estimate. Pull raw conversion logs (order ID, timestamp, SKU) predating the dedup step to
        reconstruct 17 discrete keys; if unrecoverable, hold the full rolled-up value pending manual reconstruction.
  F-2 | material  | $ at risk: unknown, pending line data | 9 lines |
        In network export, no matching order in the order database. Exception-queue default: possible over-credit.
        HOLD and investigate before approving; cross-check against DealVault's IP ranges below.
  F-3 | material/informational | $ at risk: n/a (addition, not overpay) | 12 lines |
        In order database, no matching network record. Exception-queue default: untracked sale, expect an
        inbound dispute. Decide and document a credit policy explicitly - do not let this resolve by default.
  F-4 | blocker - escalate, not adjudicated here | $ at risk: 140 lines on the highest-value SKU (largest
        single exposure in this run) | affiliate: DealVault |
        140 conversions in ~40 minutes from 3 IP ranges, concentrated on your single highest-value SKU. This is
        a coordinated-burst pattern outside this audit's scope. HOLD DealVault's entire payout - not just the
        140 lines - pending fraud review (see mbfinotti/partnerships-skills@affiliate-fraud-detection). Do not
        pay, offset, or absorb until that review rules.
Exceptions: 12 in-orders-not-in-network (untracked, dispute-risk, policy TBD) | 9 in-network-not-in-orders (over-credit, held)
Variance  : cannot be driven to a number - line-level data not supplied. Minimum safe cleared total = $31,400.00
            minus F-1 (17 lines) minus F-2 (9 lines) minus F-4 (140 lines), pending resolution of each.
Cleared   : 2,184 - 17 (quarantined) - 9 (held) - 140 (fraud hold) = 2,018 lines clearable now, and only once
            checks 7-9 are also run against real rate-card/lifecycle/tax data.
Sign-off  : preparer/checker not yet identified - confirm they are two different people before release (Gate 12).
```

## On "estimate the 17 blank ones at the average and move on"

No. That request is declined, for four reasons:

1. Your analytics tool dedupes on transaction ID; a blank ID isn't "one small conversion," it's the *identity field itself missing* for 17 records now fused into 1. There's no way to confirm any of the 17 independently — that's what dedup on a stable key exists to do, and it's the exact failure mode this audit type is built to catch (empty/malformed keys collapsing many conversions into one payable record).
2. A run-wide average blends every SKU and every partner. You don't know what mix of orders sits inside those 17 — and this run already shows the mix can be wildly non-uniform (140 DealVault conversions concentrated on a single highest-value SKU). Average is a bad estimator exactly when variance is high, and you have direct evidence variance is high.
3. Paying an estimate is still paying an amount nobody has verified as earned. Estimating doesn't resolve the finding, it launders it into the "cleared" total.
4. The correct action is quarantine: recover the underlying conversion logs (order ID, timestamp, SKU) from before the dedup step, rebuild 17 discrete keys, price each one against the real rate card, and release those 17 in a later run once resolved. If the raw logs are gone, hold the full rolled-up value — don't split the difference by guessing.

## On the 12 + 9 one-sided records

These are two different problems, not one "21 mismatches" bucket:

- **9 in network, not in orders** → possible over-credit. Hold these; investigate before approving. Worth checking whether any of the 9 share IPs or timing with DealVault's burst.
- **12 in orders, not in network** → untracked sales. These affiliates were likely never credited and will probably dispute. Decide your credit policy for these explicitly (backdate a credit, or don't) and document the decision — don't let silence be the policy.

## On DealVault

This is a fraud pattern (coordinated bursts, narrow IP ranges, single-SKU targeting), not a payout-math error — it's out of scope for this audit and gets escalated, not ruled on here. Hold DealVault's entire payout, including any lines outside the 140 that look clean, until fraud review clears or confirms the account. Given it's your highest-value SKU, this is very likely the largest dollar exposure in the whole run — larger than the blank-ID and exception issues combined.

## Still blocking full sign-off (Gate 1 — freeze the run scope)

I don't have: exact period start/end + timezone + date basis, the commission rate/tier structure, materiality threshold, validation-window length, whether any of this $31,400 is already paid, or tax-form status per payee. Checks 7–9 (rate/tier, lifecycle, currency/tax) can't be run without them. Supply those and a line-level export and I'll complete the recompute and turn "cleared: 2,018 lines" into corrected dollar figures.

## Remediation ranking (nothing here is stated as paid yet)

Since the $31,400 is proposed, not disbursed, offset/absorb/direct-recovery are off the table — the whole menu is **correct before release** (for anything we can price, once data arrives) and **hold/quarantine** (F-1, F-2, F-4) until each resolves. Don't release the run with these four findings outstanding — that's a blocker count above zero, and this skill's pass threshold requires zero blockers at release.