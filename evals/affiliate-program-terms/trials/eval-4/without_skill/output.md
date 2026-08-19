Before the draft — one thing worth flagging clearly, because it changes what number belongs in this clause: **the "cards only go back 60 days" premise is not accurate.** Visa and Mastercard chargeback windows generally run up to 120 days from the transaction (or from the promised delivery/cancellation date, for reason codes like "credit not processed" or "recurring billing canceled"), and fraud-related reason codes can permit disputes well beyond that. Exact limits vary by reason code and by your acquirer, so have your payment processor confirm the specific numbers — but 60 days will not cover the bulk of realistic dispute activity.

Concretely: a sale on day 1 gets paid to the affiliate around the 15th of the following month — commonly 15–45 days out. A 60-day clawback window closes only 15–45 days after that payout. Any chargeback landing after day 60 (very plausible on a $390 annual charge, which is exactly the kind of amount that triggers "I forgot I was on this" disputes 3-4 months in) is one Ravelin Studio eats in full while the affiliate keeps the commission.

I've drafted the section on a **120-day window** as the defensible default, with the mechanics written so you can drop the number back to 60 if you decide to accept that exposure knowingly — the number is the only thing that needs to change.

---

## 9. Clawback and Reversal of Commissions

**9.1 Reversible Transactions**
A commission is provisional until the underlying sale is final. Ravelin Studio may reverse, withhold, or deduct a commission if the referred transaction is, in whole or in part:

a) refunded to the customer, whether under Ravelin Studio's own refund policy or at Ravelin Studio's discretion;
b) charged back, disputed, or reversed by the customer's card issuer or payment network, for any reason;
c) identified as fraudulent, unauthorized, or made with a stolen or invalid payment method;
d) found to result from a referral that violates Section [X] (Prohibited Practices), including self-referrals, incentivized signups not permitted under these terms, or artificially generated traffic; or
e) otherwise voided, cancelled, or not settled in cleared funds to Ravelin Studio.

**9.2 Clawback Window**
A transaction under Section 9.1 is eligible for reversal if the triggering event (refund, chargeback, dispute, or fraud finding) occurs within **120 days** of the original transaction date, regardless of whether the commission has already been paid. Ravelin Studio may extend this window on a case-by-case basis for transactions under formal card-network dispute, fraud investigation, or legal hold, until that process resolves.

**9.3 Recoupment**
Where a reversal applies to a commission not yet paid, Ravelin Studio will simply not pay it. Where the commission has already been paid:

a) Ravelin Studio will deduct the reversed amount from the affiliate's next scheduled payment(s);
b) if future commissions are insufficient to cover the reversed amount within [90] days, Ravelin Studio may invoice the affiliate directly for the balance, payable within 30 days; and
c) Ravelin Studio may withhold any pending or future commission payment while a related dispute, chargeback, or fraud review is unresolved.

**9.4 Non-Qualifying Referrals**
Transactions found to violate Section 9.1(d) are void from inception and are not subject to the 120-day limit — Ravelin Studio may reverse them at any time upon discovery.

**9.5 Notice**
Ravelin Studio will note the reason for a reversal in the affiliate's dashboard or next statement. Reversals are not subject to appeal beyond providing Ravelin Studio with evidence that the underlying transaction was not in fact refunded, charged back, or fraudulent.

---

**If you want to keep 60 days anyway** despite the exposure above, only 9.2's number changes — everything else in the section stands as-is. I'd suggest at minimum pairing a shorter window with a reserve/holdback mechanism (e.g., paying only 80% of commission upfront and releasing the rest after 90–120 days) so the exposure doesn't fall entirely on already-disbursed funds.