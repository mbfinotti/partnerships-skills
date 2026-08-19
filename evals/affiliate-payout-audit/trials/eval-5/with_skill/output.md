Not good to go. This run fails before you even get to the math — the scope itself isn't frozen, and one of the "fixes" you applied actually destroys the evidence the audit needs. Here's the audit.

```
PAYOUT AUDIT - Northbeam Outfitters, run March-2026, period 2026-03-01..2026-03-31 (timezone UNDECLARED - see F-3), date basis: validation date (defaulted, not chosen)
Scope     : line count unknown (post-edit); proposed total $27,880 (currency unstated); sources: network export (validation-date default) vs order database
Checks    : 1 scope frozen: FAIL | 2 exports pulled: FAIL (pulled, then hand-edited) | 3 comparability: FAIL (date basis + timezone both mismatched)
            4 totals: BLOCKED (recompute worthless until export is un-edited and re-pulled) | 5 exceptions: BLOCKED (the exception queue is exactly what got overwritten)
            6 dedup: FAIL (14 order IDs collide with February's run) | 7 rate/tier: not reached | 8 lifecycle: not reached | 9 currency/tax/threshold: not reached
            10 sampling: not reached | 11 report: this document | 12 maker-checker: unconfirmed - state who calculated vs who releases before any re-run
Findings  :
  F-1 | blocker | value at risk unknown, ≥22 lines | You manually moved 22 lines into March so the count would match the order database.
        This isn't reconciliation, it's overwriting the exception queue by hand. Every one of those 22 lines was either a genuine
        March conversion misdated by the export, a genuine February conversion that doesn't belong here, or a duplicate - and
        moving it to make a count match answers that question by fiat instead of by matching stable order/transaction IDs.
        Action: discard the edited export. Re-pull the untouched network export and let checks 3-6 sort those 22 lines into
        matched / exception-queue / dedup-quarantine on their own. A count match produced by hand-editing is not evidence the
        run is correct - it's evidence the real discrepancy is still open.
  F-2 | blocker | affects entire run | Date basis is validation date by default, not a deliberate choice, while the internal
        source of truth is the order database. The skill default for reconciling to orders/billing is transaction date; validation
        date answers "what became payable this period," a different question. Comparing a validation-date export to an
        order-dated database is comparing two different event definitions.
        Action: re-pull the network export on transaction date specifically, before re-running the comparison.
  F-3 | blocker | boundary lines, count unknown | Three clocks are in play - network reports UTC, the order database stamps
        Europe/Berlin, your program calendar runs America/Chicago - and the stated window (March 1 00:00 - March 31 23:59:59)
        doesn't say in which one. Depending on which clock you mean, the same real-world instant near either edge of the
        window lands in February, March, or April in the other two systems. Nothing here has been normalized to a single
        timezone yet, so the "March 1-31" boundary is not actually defined.
        Action: pick one timezone for this run's scope (UTC is the natural choice - it's the network's own reporting basis and
        the thing being audited), convert both exports' timestamps into it, then re-apply the cutoff. Re-check every line within
        24h of either edge under both Berlin and Chicago time too, and flag any that move.
  F-4 | material | boundary instant | The window is closed (ends 23:59:59) rather than half-open. Combined with F-3's unresolved
        timezone, the last second of March is genuinely ambiguous and could double-count or drop a transaction sitting on
        that boundary.
        Action: redefine the window as 2026-03-01T00:00:00 <= t < 2026-04-01T00:00:00 in the single normalized timezone from F-3.
  F-5 | blocker | 14 order IDs | Fourteen order IDs in this run also appear in February's run (re-export after a late batch).
        Until you diff March's key set against February's, these are conversions about to be paid twice.
        Action: check whether February's run already paid these 14 IDs. If yes, remove them from March before totaling -
        nothing about March is paid yet, so this is a same-run correction, not an offset or clawback. If no, decide by the
        declared date basis (F-2) which period canonically owns each ID, and pay it exactly once.
Exceptions: none can be worked yet - F-1 overwrote the raw material the exception queue runs on. Re-derive it from the
            untouched export once F-2/F-3/F-4 are fixed.
Variance  : not computable. $27,880 is the output of a comparison built on a hand-edited export, a wrong-by-default date
            basis, and an undefined timezone boundary - it is not evidence of anything until the run is re-pulled clean.
Cleared   : 0 lines. Nothing in this run has passed the comparability gate yet.
Sign-off  : preparer and checker not yet confirmed as different people (interview item still open) - required regardless of
            the above; RELEASE: no. HOLD the entire run.
```

**What to do next, in order:**
1. Re-pull the Northbeam export on **transaction date**, not validation date.
2. Fix the scope to **one timezone** (recommend UTC) and convert both sources' timestamps into it before applying any cutoff; use a half-open window (`< April 1`, not `<= March 31 23:59:59`).
3. Throw away the 22 hand-moved lines' placement — let them fall out naturally as matched / exception / duplicate once 1–2 are fixed.
4. Diff this run's order IDs against February's paid key set; strip the 14 overlapping IDs that were already paid, or resolve them to a single owning period.
5. Only after that: reconcile totals, work the exception queue, recompute rate/tier, check lifecycle and tax/threshold, and get an independent checker (not you) to sign off before releasing anything.

Since nothing in this run is paid, every one of these is a **correct-before-release** fix — no offsets, no clawbacks, no partner-facing conversation needed. This is fixable in an afternoon; it's not fixable by moving lines until the count looks right.