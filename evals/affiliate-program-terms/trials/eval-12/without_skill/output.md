## Short answer

No — one master agreement with two program-specific schedules. Not two fully separate agreements.

**Why not fully separate:** the boilerplate (independent contractor status, conduct rules, IP/trademark use, confidentiality, indemnification, termination for cause, dispute resolution, FTC compliance) is identical for both programs and duplicating it means two documents to keep in sync, two onboarding flows, two W-9/W-8 collections, and a fraud/policy violation in one program that doesn't automatically let you terminate the other.

**Why not one flat agreement either:** the commercial terms are genuinely incompatible in one clause set — recurring % with a 24-month cap and trailing-commission-on-termination logic (SaaS) vs. one-time % with a return/RMA clawback window (hardware). Cookie duration, clawback triggers, and "when is a commission earned" differ by design. Forcing both into one commission clause creates ambiguity exactly where money is at stake, and it also blocks you from sunsetting or changing terms on one line without touching the other.

**The one case a single flat contract breaks down completely:** an affiliate who drives a bundled order (SaaS *and* a scanner in the same cart/funnel). You need an explicit rule for splitting commission by line item — this is the actual reason to write this deliberately rather than copy a template.

Standard fix, used by most multi-line companies: **one Master Affiliate Agreement + Schedule A (SaaS) + Schedule B (DTC hardware)**. An affiliate signs the Master once; enrollment in either or both Schedules is tracked separately; either Schedule can be amended or terminated independently.

Below is the actual draft.

---

# KIRNWOOD MASTER AFFILIATE AGREEMENT

This Master Affiliate Agreement ("**Agreement**") is entered into between Kirnwood, Inc. ("**Company**") and the individual or entity enrolling as an affiliate ("**Affiliate**"). This Agreement governs Affiliate's participation in one or both commission programs described in **Schedule A** (SaaS Inventory Platform) and **Schedule B** (DTC Hardware Store), each a "**Program**" and together the "**Programs**"). Each Schedule is incorporated by reference and forms part of this Agreement only for the Program(s) Affiliate is enrolled in. If a Schedule conflicts with this Master Agreement, the Schedule controls for that Program.

**1. Enrollment.** Affiliate may enroll in Schedule A, Schedule B, or both. Enrollment in one Program does not require or imply enrollment in the other. Company will confirm active Program enrollment via the affiliate dashboard or tracking platform.

**2. Independent Contractor.** Affiliate is an independent contractor, not an employee, agent, partner, or joint venturer of Company. Affiliate is solely responsible for its own taxes, business licenses, and expenses.

**3. License.** Company grants Affiliate a limited, non-exclusive, non-transferable, revocable license to use Company-provided tracking links, creative assets, product names, and trademarks solely to promote the Program(s) Affiliate is enrolled in, per Company's brand guidelines. No other IP rights are granted.

**4. Affiliate Obligations — applies to both Programs.**
Affiliate must not:
- send unsolicited email/SMS in violation of CAN-SPAM, TCPA, or equivalent law;
- bid on Company's trademarks or confusingly similar terms in paid search;
- use cookie-stuffing, forced clicks, incentivized traffic, or self-referrals;
- make claims about pricing, features, capabilities, or specs beyond what Company publishes;
- misrepresent its relationship with Company (must disclose the affiliate relationship per FTC Endorsement Guides on every placement).

**5. Tracking & Attribution.** Attribution window and "qualifying action" are defined per Schedule, since they differ by Program. Last-click attribution applies unless a Schedule states otherwise. Company's tracking data is the sole basis for commission calculation, absent manifest error.

**6. Mixed-Cart / Bundled Orders.** When a single referred order contains both a Schedule A product (subscription) and a Schedule B product (hardware), Company will allocate commission per line item: the subscription line is commissioned under Schedule A terms, the hardware line under Schedule B terms, based on the listed price of each line at checkout.

**7. Payment.** Commissions across both Programs are aggregated and paid on a single monthly payment run, net 30 from month-end, provided the combined balance meets the $[X] minimum payout threshold; balances under threshold roll forward. Affiliate must provide a valid W-9 (US) or W-8BEN (non-US) before any payout. Company may withhold payment on any commission under active fraud review, in either Program, pending investigation.

**8. Confidentiality.** Each party will keep the other's non-public business, pricing, and performance information confidential, using it only to perform this Agreement.

**9. Indemnification.** Affiliate indemnifies Company against claims arising from Affiliate's marketing conduct, false claims, or breach of Section 4. Company indemnifies Affiliate against third-party IP claims arising solely from Affiliate's authorized use of Company-provided creative, per Schedule terms on product-specific liability (see Schedule B §7 for hardware product liability).

**10. Term & Termination.**
- Either party may terminate this Agreement, or Affiliate's enrollment in a single Schedule, for convenience with 30 days' written notice.
- Company may terminate this Agreement or any Schedule immediately for cause (fraud, Section 4 violation, insolvency).
- Terminating one Schedule does not terminate the Agreement or the other Schedule.
- Terminating this Agreement terminates both Schedules.
- Payment on termination follows the "Effect of Termination" clause in each applicable Schedule.

**11. Amendment.** Company may amend a Schedule's commission terms with 30 days' notice to enrolled Affiliates in that Program; continued promotion after the effective date constitutes acceptance. Amending one Schedule does not require re-execution of this Master Agreement or the other Schedule.

**12. Governing Law & Disputes.** [Governing law / venue / arbitration clause — to be set per counsel and jurisdiction.]

**13. Entire Agreement.** This Master Agreement plus its active Schedule(s) is the entire agreement between the parties regarding the Program(s), superseding prior affiliate terms for that Program.

---

## SCHEDULE A — SaaS Inventory Platform Affiliate Program

**1. Product.** Kirnwood Inventory, subscription SaaS, list price $240/month.

**2. Commission Rate.** 20% of Net Subscription Revenue actually collected from a referred customer, per billing cycle, for up to 24 consecutive paid months per unique referred customer ("**Commission Cap**"). Commission stops automatically upon the earlier of: the customer's cancellation, or the 24th commissioned payment — whichever comes first.

**3. Net Subscription Revenue.** Gross recurring subscription fee actually paid and not refunded, excluding taxes, one-time setup/onboarding fees, and any discounts applied. Annual prepayments are commissioned on the equivalent monthly-recognition schedule, still subject to the 24-month cap measured in months, not payments.

**4. Attribution Window.** 60 days, last-click, from first click to trial signup or paid signup.

**5. Commission Trigger & Holdback.** Commission accrues after the referred customer's first paid invoice clears and a 30-day holdback period passes (to net out early refunds/chargebacks). Trial-only signups that never convert to paid are not commissionable.

**6. Clawback.** Any commission is reversed if the underlying payment is refunded or charged back.

**7. Reactivation.** A churned customer who resubscribes more than 180 days after cancellation is treated as a new referral, restarting the 24-month cap; resubscription within 180 days continues the original count.

**8. Effect of Termination (trailing commission).**
- Termination **without cause** (e.g., Company discontinues the affiliate program): Affiliate continues to earn commission on already-referred, still-paying customers through the remainder of their 24-month cap.
- Termination **for cause**: all future commission accrual stops immediately upon termination; Company still pays out commission already earned and payable for periods before termination.

---

## SCHEDULE B — DTC Hardware Store Affiliate Program

**1. Product.** Kirnwood barcode scanners, priced $89–$450.

**2. Commission Rate.** 8% of Net Sale Price per unit, one-time, no recurring component.

**3. Net Sale Price.** Sale price actually paid, excluding taxes, shipping, and any discount applied.

**4. Attribution Window.** 30 days, last-click.

**5. Commission Trigger.** Commission accrues once the applicable return/RMA window ([30] days from delivery) closes without a return, refund, or warranty replacement.

**6. Clawback.** Full commission reversal if the unit is returned, refunded, or replaced under warranty within the return window. No clawback for warranty events occurring after the return window closes.

**7. Product Liability.** Company is the merchant of record and bears product liability and warranty obligations for the hardware. Affiliate's marketing must not make performance, safety, or compliance claims beyond Company's published specs; Affiliate bears no product liability but indemnifies Company for claims arising from Affiliate's own unauthorized claims about the product.

**8. Tax.** Company is responsible for sales tax collection/remittance as merchant of record; Affiliate has no independent tax collection obligation for referred hardware sales.

**9. Effect of Termination.** No trailing commission — Schedule B has no recurring component. Company pays out commission already earned (return window closed) as of the termination date; commission on orders still inside their return window at termination is paid once that window closes and no return occurred.

---

### Notes before you use this

- This is a solid starting structure, not a filed legal document — have counsel review before sending it to affiliates, particularly: state-level "affiliate nexus" sales-tax statutes (several US states treat affiliate relationships as creating sales tax nexus for the merchant), FTC Endorsement Guide wording, and arbitration/governing-law clause (left as placeholder above).
- Decide and fill in: minimum payout threshold, exact attribution windows (60/30 days are reasonable defaults, not required), and the hardware return-window length (align to your actual RMA policy).
- The 24-month recurring cap and the trailing-commission-on-termination clause are the two places companies get burned when they improvise — they're deliberately explicit above.