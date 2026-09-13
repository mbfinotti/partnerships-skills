## Recommendation: Don't release as-is. Hold two payees, fix the export, then release.

Your finance lead's "pay now, paperwork later" plan is backwards — withholding on undocumented payees isn't a bureaucratic nicety you can defer, it's the payer's own tax liability. "The amounts are small" is irrelevant; there's no de minimis exception once a payee crosses the $600/year reporting threshold, and both of your flagged payees are well above it.

### 1. Missing W-9, $4,800 owed

No W-9 = no certified TIN = **mandatory backup withholding at 24%** under IRC §3406, full stop. You have two compliant options:

- **Hold the $4,800** until the W-9 arrives, then pay in full — cleanest, no IRS deposit needed.
- **Pay now net of 24%**: send **$3,648**, withhold **$1,152**, and deposit it against your EIN (Form 945, annual backup-withholding return).

What you must not do: pay the full $4,800 with no W-9 on file. If this payee never furnishes a TIN and you didn't withhold, the IRS can hold **Larkfield** liable for the uncollected 24% plus penalties — the recipient's own tax situation is irrelevant to your exposure.

### 2. French publisher, W-8BEN-E dated 2022

W-8BEN-E forms expire on **December 31 of the third calendar year after signing**. A form signed in 2022 expired **12/31/2025** — it is dead for a June 2026 run. Two layers here:

- **Documentation**: request a refreshed W-8BEN-E now, before or concurrent with payment.
- **Withholding**: if this commission is genuinely foreign-source (the publisher performs its promotional/referral activity outside the US, which is the normal case for affiliate commissions), Chapter 3 NRA withholding (30%) shouldn't apply regardless of the form's status — foreign-source service income isn't FDAP subject to §1441. But without a _valid_ form on file, you lose your documented basis for that position, and under the presumption rules you're technically exposed to being treated as if paying an undocumented (possibly US) payee, which points back toward the 24% backup-withholding treatment until cured. Given the dollar amount is presumably not $4,800-level, weigh it, but don't let the form stay expired past this cycle — chase it in parallel with the payment, not after.

### 3. EU VAT-registered publishers, network-generated invoices

Self-billing is legal under EU VAT rules only with a **written self-billing agreement per publisher**, and each self-billed invoice must carry both the publisher's VAT number and the "Self-billing" notation (Directive 2006/112/EC, Art. 226(10a)), plus reverse-charge language where the service is cross-border B2B. This isn't a per-run blocker, but confirm agreements actually exist for all 38 — if the network started generating these invoices without them, every invoice issued so far is technically defective, for both you and the publisher.

### 4. PayPal fees netted out before the export

Reportable income (1099-NEC for US persons, and the equivalent record for 1042-S purposes on the foreign side) is the **gross commission earned**, not the amount net of your payment-processor fee — the fee is your cost of moving money, not a reduction in what the payee earned, unless your affiliate agreement explicitly makes the payee contractually responsible for it. Right now your export is silently understating income for every PayPal-paid payee. Fix: show gross commission and the PayPal fee as two separate lines. You can still _net-pay_ net of fee if the agreement supports it — just don't let that netting also shrink the reported income figure.

### Net effect on this run

Release the ~94 clean payees on schedule. For the flagged two:

- Withhold $1,152 from the $4,800 payee (or hold it entirely) instead of paying $4,800 gross.
- Chase the French W-8BEN-E now; don't block payment on it unless the amount is large enough that presumption-rule exposure worries you, but treat "expired form" as a live compliance item, not paperwork to backfill.

Get an actual accountant/tax counsel sign-off before you operationalize backup withholding and Form 945 deposits — these are the correct mechanics, but you want someone with eyes on your specific entity structure and past filings before you start withholding money from real people for the first time.
