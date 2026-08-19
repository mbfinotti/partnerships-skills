## Verdict: Not as scoped. Conditional yes, different timeline.

The signals your engineer named are the right ones for self-referral rings. The three-week, ship-it plan is not — it skips a legal gate and the sequencing that makes the rest of the fraud program actually work.

### ✅ Why the approach is diagnostically correct

Self-referral and multi-account rings are exactly identified this way in the fraud taxonomy:
- **Self-referral tell**: registration IP, device, or billing details shared between the affiliate account and the "customer."
- **Ring tell**: shared device fingerprints, IPs, or payout destinations across supposedly unrelated accounts.

Device fingerprinting + billing-address/click-IP matching + email/phone cross-referencing is the standard toolkit for these two patterns. No objection to the *what*.

### 🔴 Why the *plan* fails

**1. Three weeks is the wrong estimate by an order of magnitude.**
This is the "cross-account identity" signal family, and it's rated as the most expensive of the four families that exist (list filtration, downstream outcomes, timing, cross-account identity):
- Effort: **a quarter** — lawful basis, retention design, access control, counsel sign-off — not three weeks.
- Compliance cost: **highest of all four**, by a wide margin.
- Efficiency: **worst of the four** (list filtration beats it, downstream outcomes beats it, timing beats it).

"He can have it live in three weeks" almost certainly means the matching logic, not the legal work around it. Those aren't optional extras — they're gating.

**2. It's missing a legal review, not a nice-to-have.**
Device fingerprinting, matching emails/phones/addresses across accounts, and comparing click IP to billing address are all personal-data processing, and some of it sits outside anything a cookie banner covers. The UK regulator's published position is that fingerprinting can require consent even outside advertising. Before this ships, someone has to state, in writing:
- The lawful basis (fraud prevention is a *commonly cited* basis, not an automatic one — "we needed it to catch fraud" is explicitly **not** a basis on its own).
- The retention period for matched records.
- Who can see the matched records.

Then route it to counsel. If that hasn't happened, "three weeks to live" is not a real date.

**3. Wrong build order.**
Cross-account identity work should never be the first thing built. The correct sequence is: list filtration → downstream outcomes → timing → cross-account identity last, and only against affiliates already watchlisted by the cheaper signals — not a blanket sweep matching every affiliate against every customer. Scoping it that way also shrinks the compliance surface (fewer records processed, easier to justify the lawful basis).

**4. No mention of the control that should exist before any detection rule.**
The single highest-leverage anti-fraud control at Orla is a **30-90 day commission hold/validation window** — not a detection algorithm. Delaying payment by two to four months is independently shown to eliminate over 70% of fraud at no cost to profit (Edelman & Brandi, *JMR* 2015). If Orla doesn't already have this, greenlight *that* first — it's an hour of platform config, reversible, and it protects money the ring-detection project won't touch for months.

### What to greenlight now, this week

| Do this | Cost | Why now |
|---|---|---|
| Confirm/set a 30-90 day hold window | ~1 hour | Highest value, lowest cost, protects money immediately |
| Confirm clawback + negative-balance carry-forward is in the affiliate terms | Legal review, but check status now | Without it, catching the ring still doesn't recover anything already paid |
| Run list filtration (data-center ASN, declared bots) if not already live | Near-zero | No personal data, clears volume before anything else is tuned |
| Pull 90 days of per-affiliate conversion, chargeback, and sales-concentration data | Analyst time | Self-referral rings usually show up cheaply first as sales concentration outliers (~80%+ of volume on a handful of accounts) — audit that list by hand before building anything |

If Orla's affiliate roster is small (roughly under 20 active partners), skip statistical/engineering-heavy detection entirely — an analyst reading the list by hand beats a matching pipeline at that scale.

### The identity-matching project itself: correct scope, correct timeline

Greenlight it as a **quarter-long project**, not three weeks, with this shape:
1. Legal sign-off first: lawful basis, retention period, access control — before any code touches customer PII.
2. Scope to affiliates already flagged by the cheap signals above, not a full-database sweep.
3. Output feeds **Hold & Investigate** by default (throttle commissions, open a dossier, cross-functional review in 24-48h) — shared device/IP/payout destination only justifies **Suspend & Escalate** once it's confirmed technical evidence, not on first match.
4. Name the false-positive check inline before it ships: shared IP can be an agency submitting on behalf of clients, a shared office/household network, or corporate NAT — not just a ring. Verify against the account profile before acting.

### Still need answers before this is locked

- Current hold window and whether clawback is contractually authorized today.
- Program size and monthly commission spend (decides manual review vs. automated scoring).
- Tracking setup: client-side pixel or server-side postback (self-referral evidence is much stronger with server-side data).
- Any prior confirmed self-referral incidents, and whether commission was recovered.

**Bottom line:** the technique is right, the three-week date isn't real, and shipping cross-account matching without the lawful-basis/retention/counsel sign-off exposes Orla legally for a control that won't even be the thing protecting the money — the hold window is. Greenlight the hold-window check and cheap signals this week; greenlight the identity-matching build as a quarter-long, legally-gated project, not a sprint.