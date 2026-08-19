This will be a draft for review by qualified counsel, not legal advice. Program terms are legally binding.

Before the clause itself, one thing needs to be surfaced rather than quietly drafted around:

**Your finance lead's premise is incorrect, and it matters a lot for this product specifically.** Cards do not "only go back 60 days." The standard Visa/Mastercard chargeback filing window is **120 days** from the transaction date. Worse, for "services not received" / "not as described" dispute codes — which is exactly what a subscriber who feels shortchanged on a *design-asset subscription* will file — the window runs **120 days from the expected delivery date**, capped at **540 days from the transaction date**. Because this is a 12-month subscription, "delivery" is understood to continue across the year, so a cardholder who disputes in month 10 or 11 is still inside the network's own filing limit. A 60-day clawback window leaves a tail of up to ~480 days of chargeback exposure with no contractual right to recover the commission already paid. This isn't a matter of drafting preference — it's arithmetic your finance lead has wrong, and I'm flagging it rather than silently drafting the clause to match a 60-day assumption that doesn't hold.

I've drafted the clause at the 60-day window you specified, since that's the instruction given, but I've marked the mismatch inline and you should not treat this section as complete without deciding how the uncovered tail gets covered (see the note after the clause).

---

## 15. Clawback & Reversal

**15.1 Reversal right.** Ravelin Studio may reverse, void, or deduct any commission — whether Pending, Cleared, or already Paid — that relates to a transaction that is later refunded, cancelled, charged back, disputed, or found to be fraudulent or in breach of these Terms. This right survives payment of the commission and survives termination of the affiliate's account.

**15.2 Reversal grounds.** A commission may be reversed only on one or more of the following grounds:

- (a) the underlying card transaction is charged back, disputed, or reversed by the cardholder or issuing bank for any reason;
- (b) the customer is refunded or the sale is cancelled under Ravelin Studio's refund policy;
- (c) the referral is found to result from a prohibited tactic under Section 6, fraud, or self-referral; or
- (d) the transaction is found to be unauthorized or made with a stolen or compromised card.

No commission may be reversed on any ground other than those listed above. `[LEGAL REVIEW: confirm this enumerated list matches Ravelin Studio's actual published refund/cancellation policy for the annual plan before publication — an enumerated ground that doesn't match the real refund policy creates a gap either way.]`

**15.3 Clawback window.** The reversal right under 15.1 may be exercised for **60 days** from the date the commission is paid to the affiliate. After this window closes, Ravelin Studio waives no right that arises independently under Section 16 (Chargeback Reserve & Negative Balances) or applicable law; the window in this clause governs contractual clawback against the affiliate only. `[LEGAL REVIEW: this 60-day window is materially shorter than the card networks' own dispute-filing limits for this product. Standard chargeback filing runs 120 days from the transaction date; "services not received / not as described" codes — the category a subscription complaint is most likely to fall under — run 120 days from the expected delivery date, capped at 540 days from the transaction date. For a 12-month subscription paid upfront, this leaves a chargeback tail of several hundred days with no contractual recovery mechanism. Counsel and finance should re-confirm the window is a deliberate trust/simplicity trade-off, not a factual assumption about card timelines — the assumption as stated is incorrect.]`

**15.4 Mechanism of recovery.** Where a reversed commission has already been paid, Ravelin Studio will recover it by deducting the amount from the affiliate's next payable commission balance, carried forward across payout cycles until fully recovered ("negative balance"). If the affiliate's account is closed or terminated before full recovery, Ravelin Studio may invoice the affiliate directly for the outstanding amount. See Section 16 for negative-balance carry-forward mechanics.

**15.5 No forfeiture beyond the reversed transaction.** Reversal under this Section is limited to the commission attributable to the specific reversed, refunded, or fraudulent transaction. It does not authorize forfeiture of other, unrelated earned commissions. `[LEGAL REVIEW: blanket forfeiture of unrelated earned commissions is legally contested and carries state escheatment exposure — do not broaden this clause beyond the transaction-specific reversal drafted here without counsel sign-off.]`

---

**What this clause does not fix, and needs a decision from you:** Because the 60-day window closes long before the real chargeback exposure does (especially the 540-day cap on service-type disputes), Section 15 alone leaves an uncovered tail — commission paid out and unrecoverable if a chargeback lands on day 61 through day ~540. The skill treats *some* control here as mandatory, not optional, once commissions are paid before the transaction is chargeback-safe (which is the case here — paid the month after clearing, well before any card dispute window closes). Given card-only, upfront, annual billing, you're squarely in the situation this is meant to cover.

Two ways to close the gap, and you need at least one:

- **Negative-balance carry-forward** (drafted above at 15.4, near-zero extra effort): only recovers from affiliates who keep earning — useless against an affiliate who stops referring after being paid.
- **Chargeback reserve** (a withheld percentage, e.g. 10–15%, released quarterly): actual cash held against the tail, the only thing collectable from an affiliate who's left the program — but it's a standing operational job (release schedule, threshold, termination treatment) and needs its own `[LEGAL REVIEW]` on the escheatment question before publication.

Given card-only payment and a full year of dispute exposure, I'd recommend at minimum keeping 15.4's carry-forward and seriously considering the reserve — say the word and I'll draft Section 16 to match.