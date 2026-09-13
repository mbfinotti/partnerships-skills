# Verdanta Labs — May Partner Payout Review

**Scope:** 318 lines, ~$44K total, USD/EUR/GBP settled to USD. **Materiality threshold: $250.**

## 🔴 1. FX rate methodology — undocumented + directionally biased

- No documented rate-date convention (spot on initiation? settlement? T-1?) is a control gap on its own, independent of the size of any variance.
- A **consistent** ~1.8% deviation across all 5 EUR lines checked — same direction every time — is not rounding noise. Random FX timing differences don't line up 5-for-5. This is a **systematic** effect: most likely a built-in spread/margin the platform applies on conversion (common with payment processors — Wise, PayPal, Stripe-style FX all carry a 1.5–2.5% margin over ECB/mid-market), or a stale/fixed rate table.
- **Materiality is currently unknown, not "small."** You've only priced the effect on 5 lines. The real question is: _total EUR payout volume × 1.8%_. Given $44K total across 3 currencies, it doesn't take much EUR concentration to blow past the $250 threshold on this line alone — e.g. $14K of EUR volume × 1.8% ≈ $250. Don't close this out until you've pulled the EUR-only subtotal and done that multiplication.
- **Action:**
  - Get the platform's FX methodology in writing (rate source, timestamp, any embedded spread) — this should be in the contract or vendor terms, not something you have to reverse-engineer.
  - If it's an undisclosed spread, that's a payee-facing issue (partners are silently receiving less than a fair ECB conversion would give) as much as an accounting one — check what your partner agreement actually promises re: FX.
  - Quantify total EUR exposure before deciding this is or isn't material.

## 🟢 2. $3.87 aggregate variance, cent-level per line

- 318 lines, each off by ~1–2¢, aggregating to $3.87 is exactly the signature of **per-line rounding** (round-to-cent applied at the line level vs. at an aggregate/pre-rounding step), not an error. Max theoretical drift from independent ±0.5¢ rounding across 318 lines is well within this range.
- **$3.87 vs. $250 threshold: immaterial by two orders of magnitude.** No correction warranted.
- **Action:** Worth 5 minutes to check whether the per-line differences are all the _same sign_ (→ a rounding-rule mismatch, e.g. round-half-up vs. round-half-even — fixable and worth documenting) or mixed sign (→ pure floating-point/rounding noise — nothing to do). Either way, don't spend more time here; this is not where your risk is.

## 🟠 3. Sub-$50 payees — the amount is fine, the disappearance isn't

- Four payees sitting below the $50 minimum totaling $148.22 is normal minimum-payout-threshold behavior — carrying small balances forward is expected, and $148.22 is under materiality on its own.
- **The real flag is structural, not dollar-sized:** two payees who were below-minimum _last_ month are **absent from this month's file entirely**, rather than showing up again as a still-under-threshold carryover. If the mechanism is "accumulate until $50, then pay," those two balances should still be _somewhere_ — either rolled into this month's four, paid out via another channel, or explicitly written off. A payee that simply vanishes from the export means either:
  - their balance was paid outside this file (fine, but needs a cross-reference), or
  - the account was closed/churned and the balance zeroed without a record (needs a policy check — forfeiture shouldn't happen silently), or
  - an export/pagination bug dropped rows that still have real, owed balances (needs a data-integrity fix).
- **Action:** Trace those two specific payees by ID — pull last month's carryover balance and confirm where it landed this month (paid / rolled forward / written off). This is a small dollar amount but a broken audit trail, and it recurs every month you don't fix it — small missing amounts compound and are exactly what turns into a partner dispute later.

## Bottom line

| Issue                | $ impact                                                  | vs. $250 threshold                 | Status                                                   |
| -------------------- | --------------------------------------------------------- | ---------------------------------- | -------------------------------------------------------- |
| FX rate bias         | Unquantified — likely material once EUR volume is applied | Pending calculation                | 🔴 Escalate, get vendor documentation, size the exposure |
| Rounding variance    | $3.87                                                     | Immaterial                         | 🟢 No action, optionally document rounding rule          |
| Sub-threshold payees | $148.22 (visible); 2 accounts untraced                    | Immaterial in $, but a control gap | 🟠 Trace the 2 missing payees before closing the month   |

Nothing here individually crosses $250 in confirmed dollars, but the FX item is unquantified rather than small — treat it as open, not closed, until you've priced total EUR exposure. The rounding item is closed. The missing-payee item is closed on materiality but open on process — don't let it recur silently next month.
