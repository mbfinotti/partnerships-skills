## Verdict: HOLD — do not release the $48,712.40 run as proposed

I read the skill in full plus all five reference docs (`rate-and-tier-verification.md`, `lifecycle-and-clawback.md`, `reconciliation-and-dedup.md`, `currency-tax-and-payment.md`, `audit-report-examples.md`). One important caveat up front: **no platform export or billing extract exists in this repo** — I only have the narrative you gave me. So this is a targeted rate/tier + lifecycle review of your five flagged items (gates 7–8), not the full 12-gate reconciliation (gates 1–6, 9 need the actual export). All five of your "not sure if it matters" items matter — three are blockers.

```
PAYOUT AUDIT - Calyx Ops partner program, run <id>, period <unconfirmed> (<tz>, <date basis>)
Scope     : 412 lines, proposed total $48,712.40 USD; sources: partner-reported run only -
            NO platform export / billing extract supplied, so gates 2-6 and 9 could not run
Structure : 20% recurring rev-share, 12-month cap, 30-day validation window
Checks    : 1 scope: INCOMPLETE (period/tz/date basis not confirmed) | 2 exports: FAIL (none provided)
            3 comparability: n/a | 4 totals: n/a (no second source) | 5 exceptions: n/a | 6 dedup: n/a
            7 rate/tier: FAIL (3 findings)  | 8 lifecycle: FAIL (2 findings) | 9 currency/tax: not raised, unchecked
            10 sampling: targeted review of 5 preparer-flagged items only - not a full or random sample
Findings  :
  F-1 | blocker  | value unknown, all Sable Works lines | Partner was bought out for $12,000 lump sum in
        Dec 2025; a buyout ends the recurring stream permanently. Any recurring line for a bought-out
        account is a straight overpay, full stop - it doesn't matter what the account is billing now.
        ACTION: strip every Sable Works line from this run. Then check the Jan/Feb runs - if any
        post-buyout lines were already paid, that's a direct-recovery or offset case, not "absorb."

  F-2 | blocker  | value unknown, all Halden Group Jan-2025-cohort lines | Accounts referred/first
        billed Jan 2025, still billing monthly, cap is 12 months. This run's billing event is ~month 14 -
        two months past the cap on the cohort you named, meaning last run (~month 13) likely already
        breached it too. This is the "systematic, compounding overpay" pattern the cap rule exists to
        prevent - it doesn't self-correct.
        ACTION: zero these lines. Pull the account-level first-billed dates to confirm exactly which
        Halden lines are past month 12, and check whether the prior run needs an offset for month 13.
        FIX FORWARD: this is a second run touching the same finding class (cap math) - add an automated
        month-index cutoff so month 13 can't generate a line at all.

  F-3 | blocker  | value unknown, 2 trial-conversion lines | Trials converted 18 days ago, marked
        "approved" against a 30-day validation window - 12 days early. This is a skipped state
        (pending -> approved without the window elapsing), the exact failure mode gate 8 exists to catch.
        ACTION: revert both to pending; hold to the run in which day 30 has actually passed.

  F-4 | material | $100.00, 1 line (Meridian Freight) | Line reads $180 = 20% x $900, the
        pre-downgrade plan price. The account moved to the $400/month plan Feb 10, before this
        period closed - the commission was computed on a plan the customer wasn't paying by period end.
        ACTION: recompute off the settled invoice, not the old plan price. Straight-line that's
        20% x $400 = $80 (adjust only if the settled Feb invoice was prorated across $900/$400 for the
        split month - pull the actual invoice, don't assume). Correct before release: -$100 at minimum.

  F-5 | material | value unknown, 3 lines | Commissioned on plan list price while those customers are
        on a 20%-off annual promo. Commission base must be the settled/discounted amount the customer
        actually paid, never list price - this inflates the base by 25% (list = discounted / 0.8) on
        all three lines.
        ACTION: recompute each at 20% x (list price x 0.8) against the actual settled invoice; correct
        before release.

Exceptions: not evaluated - gate 5 needs a second source (billing/CRM extract) that wasn't supplied.

Variance  : cannot be driven to zero without the full export. Known so far: F-4 confirms -$100.00;
            F-1/F-2/F-5 are real but unquantified without line-level data. Reporting an "unexplained
            variance below materiality, PASS" here would be exactly the negative-example failure the
            skill calls out - so I'm not doing that. Variance is open, not closed.

Cleared   : 0 lines certified clean. 5 items held/corrected above; the other ~407 lines are unaudited,
            not presumed-clean - that distinction matters for gate 1 ("no silent gaps").

Sign-off  : cannot complete - 3 blockers outstanding, full population unreconciled.
```

### What actually needs to happen before this releases

1. **Pull the real platform export + billing/CRM extract** for the period and hand them over (or point me at where they live) — everything above the line is confirmed by your description alone; everything below needs the data to close.
2. Strip Sable Works entirely, zero the Halden Group month-13+ lines, revert the two 18-day trials to pending, and correct Meridian Freight to the settled post-downgrade base and the three promo accounts to the discounted base.
3. Re-run gates 1–6, 9–11 against the export once you have it — this review only covered the items you happened to notice; a 412-line run this dense with rate/tier and lifecycle errors in a 5-item spot check is a strong signal there are more you didn't notice.
4. **Maker-checker**: confirm whoever calculated this run isn't also the one releasing it. Given three blockers, that gate matters more here than usual, not less.

None of your "not sure if it matters" items are noise — Sable Works and Halden Group in particular are structural (a paid-off stream still running, a cap not enforced), which means they've likely already leaked into prior runs too. Worth pulling the last 2–3 runs for the same two checks once this one is fixed.