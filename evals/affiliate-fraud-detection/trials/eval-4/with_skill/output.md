## Short answer: No — stop the deletion, and don't count on the network.

Two things in what you've described work against you, and one is still reversible if you act today.

### 1. Don't delete the account this afternoon

Deleting the account destroys the evidence that any enforcement action — clawback, network report, chargeback dispute — has to stand on. Instant bans are the single most common way programs end up with a confirmed fraud case and no way to act on it: no dossier survives, and network compliance and card issuers act on evidence, not on your say-so.

Before anything else, today:

- **Suspend/throttle commissions to zero**, don't delete the account or the affiliate record.
- **Export and lock down**, tied to this affiliate's ID: click logs, conversion/order records, redirect-chain and tracking-URL data, chargeback records with dates and order IDs, IP/geo on the flagged orders, and the affiliate's application/registration data (email, phone, billing/payout destination).
- Check for **shared IP or payout destination between this affiliate's account and the buyer accounts** on the charged-back orders — that's the self-referral tell, and it's the single strongest thing to put in a network dossier.

### 2. The email you sent is a liability, not a closed loop

Telling a partner "we caught you committing fraud" before you've built the evidence file does two things against you:

- It's now written proof of an accusation your dossier may not yet support — if this turns out to be a product-quality problem or a false positive, that email is exposure (breach of contract / defamation risk), not a clean paper trail.
- It tips your hand. If there's a self-referral ring or stolen-card operation behind this, they now know to stop, move payout destinations, or dispute everything preemptively.

Standard practice going forward: never use the word "fraud" with a flagged partner. Neutral language only — "your account is under review pending a routine quality check." Route this to legal before any further contact, given the wording already used. Give them a written appeal path (~14 days, evidence in writing, reviewed by someone other than whoever flagged it) even though you've already jumped past that step.

### 3. "The network will pick it up" is false — that's the actual risk here

Networks earn a cut of commission volume. Their compliance teams are reactive: they act on evidence-backed complaints from you, not brand-specific surveillance. If you delete the account and walk away, nothing happens on their end — the affiliate can re-apply to another brand on the same network tomorrow, and any cross-program blacklist only exists if you file it.

What actually gets action: send network compliance a dossier with the affiliate/publisher ID, the specific rule triggered with timestamps, baseline vs. observed values, evidence artifacts (IP/geo mismatches, shared payout destination if found, redirect-chain capture), and financial exposure ($ held, $ paid, $ at risk). Request suspension and cross-program flagging explicitly — don't assume it's implied.

### 4. Check the number before you finalize the verdict

7% chargebacks in a month clears the common suspend-tier threshold (>3% rolling 30 days), so escalating is defensible _if_ it's this affiliate's own traffic, not a program-wide problem. Before the dossier goes out:

- Compare against your **other affiliates' chargeback rate for the same period** — a spike across the board points to a product/fulfillment issue, not this partner.
- Check the **order-level detail behind the 7%**: same failure reason each time (stolen card, not-as-described, never-received)? Concentrated in a few geos or a short click-to-conversion window? That's what turns "elevated rate" into "fraud" rather than "this partner drives risky segments."

### 5. Recover the money — this is the part that's easy to miss

- Is clawback contractually authorized on this program (negative-balance carry-forward, chargeback reserve)? If not, any commissions already paid to this affiliate are gone — you can suspend the account but you can't get the money back. Fix this in terms for every partner, not just this one.
- Chargeback filing windows run 120 days (standard) to 540 days (services/delayed-delivery codes) from the transaction — longer than almost any hold window. If your current validation/hold window is short (or nonexistent), more of this affiliate's pending commissions than you think are still exposed. Check what's still lockable today.

### 6. After this case closes

- One flagged affiliate on one signal (chargeback rate alone) is a reasonable trigger to suspend, but it's not a standing fraud control. If this program doesn't already have a 30–90 day commission hold window and clawback/negative-balance/chargeback-reserve clauses in the affiliate terms, that's the actual gap this incident exposed — cheaper and higher-leverage to fix than any detection rule.
- If the evidence shows deliberate stolen-card fraud and the dollar amount is material, that's a legal referral (FTC reportfraud.ftc.gov, FBI ic3.gov), separate from the network report.

**Two things I'd want answered before calling this closed:** do you currently have clawback authority in this affiliate's contract, and what's your program's chargeback rate for everyone else this same month? Both change what you can still recover and whether "fraud" is actually the right label here.
