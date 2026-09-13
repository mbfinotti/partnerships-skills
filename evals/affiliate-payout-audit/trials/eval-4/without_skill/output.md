## Verdict: **Hold — do not release as submitted.** All five items you flagged are real, and combined they represent a material overpayment. Recompute before disbursing.

_(Note: I did not open the payout file itself — it sits under `skill-wip/`, which I was told to leave alone. Everything below is reasoning from the facts you gave me, not from the 412 lines. Treat dollar estimates as directional; the source lines will give exact figures.)_

### 1. Halden Group — Jan 2025 referrals still billing 🔴 Real issue

20% capped at 12 months means the commission window for a January 2025 referral runs Jan–Dec 2025. If this is the March 2026 payout, those accounts are ~14 months past referral — past the cap entirely. Those lines should be **zeroed out**, not partially reduced.

- Confirm which March you're auditing. If it's March 2025, this isn't a violation yet (only month 2–3). If it's March 2026, it's a clean cap breach and the lines come out completely.

### 2. Meridian Freight — commissioned on pre-downgrade plan 🔴 Real issue

$180 is exactly 20% of $900 (the old plan), not 20% of $400 (the current plan, post Feb 10). The commission engine didn't pick up the downgrade. Correct line should be **$80**, a **$100 overstatement** on this one account alone. Check whether other accounts had mid-cycle plan changes this month — this looks like a systemic "commission recalculated on stale plan price" bug, not a one-off.

### 3. Three accounts on list price despite 20%-off annual promo 🔴 Real issue

Revenue share should track actual revenue collected, not list price — otherwise you're paying commission on revenue you never received. Recalculate those three lines at 20% of the discounted (promo) price. Flag whether this is a data-feed problem (CRM shows list price, discount applied only at billing) — if so, this will recur every month until fixed upstream, not just this cycle.

### 4. Sable Works — bought out in December, still has commission lines 🔴 Real issue, highest severity

A $12,000 lump-sum buyout of the recurring stream should have terminated all future commission lines for their referred accounts. Any line for Sable Works in this March payout is **double payment** — you already paid for that revenue stream once. Pull every Sable Works line entirely. This is the item worth escalating fastest: it's the cleanest case of paying twice for the same thing, and if it's been happening since December, check every payout run between the buyout and now, not just March.

### 5. Two trials converted 18 days ago, marked "approved" ⚠️ Real issue, different kind

Your terms give a 30-day validation window. Day 18 is inside that window — these should still be **pending**, not approved, regardless of dollar amount. This isn't necessarily an overpayment (the conversion may well hold), but approving early breaks your own policy and removes your ability to reverse cleanly if the customer churns or is disqualified before day 30. Revert status to pending and re-evaluate at day 30.

### Net effect

Every item you noticed moves money or violates a written term — none of these are "probably fine." Minimum required before release:

- Remove Halden Group's expired-cap lines (pending confirmation of which March).
- Correct Meridian Freight to $80.
- Recalculate the three promo accounts at net price.
- Remove all Sable Works lines.
- Revert the two 18-day trials to pending and exclude their payout this cycle.

Recompute the $48,712.40 total after these five corrections before this goes out. Given the buyout double-pay and the plan-price staleness bug both look systemic rather than one-off, it's worth a quick pass over the rest of the 412 lines for the same two failure modes before you sign off — not just the ones you happened to spot.
