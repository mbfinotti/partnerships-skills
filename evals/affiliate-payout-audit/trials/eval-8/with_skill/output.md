# PAYOUT AUDIT — Larkfield Systems, June run, 96 payees, proposed $71,300

**Note on scope**: no export or line-level file was provided, so checks 1–8 (comparability, reconciliation, dedup, rate/tier, lifecycle) cannot be executed here — I'm answering only the questions the prompt actually raises, which all land in check 9 (currency, tax, thresholds) plus one comparability issue. Get me the platform export + billing/order extract if you want the full twelve-point sequence run before every future release.

## Answer: No — not as a single release. Hold 2 payees, resolve 1 open reconciliation question, reject the "withhold nothing" instruction, then release the rest.

## Findings

**F-1 | blocker | $4,800 | 1 US individual payee** — No W-9 on file. A US payee without a valid W-9 must not be paid gross: IRS backup withholding (24%) applies regardless of amount. There is no materiality exception for this — it's a filing obligation, not a rounding question. Action: withhold 24% ($1,152), pay $3,648, remit the withheld amount per backup-withholding procedure; release the balance once a valid W-9 arrives (or continue backup withholding on this payee going forward if it doesn't).

**F-2 | blocker (payee-scoped) | 1 EU (French) payee** — W-8BEN-E dated 2022. A W-8BEN-E is valid only through December 31 of the third calendar year after signing — this one expired **2025-12-31**. It is now expired, which the skill's rule treats identically to missing: "expired or mismatched forms count as missing." Hold this payee's line until a current form is collected.

**F-3 | blocker | control, not a dollar amount** — Finance's instruction to withhold nothing and "sort paperwork out after payment" is the wrong call and should not be followed as stated:
- It's not a discretionary materiality decision. Backup withholding on a missing W-9 is an IRS requirement independent of dollar size — $4,800 or $48 makes no difference.
- Paying an EU payee against an expired form isn't a paperwork lag either; the form's validity window has a hard legal date, already passed.
- The instruction also reads as a single person overriding a compliance control on their own authority right before release — which is itself the condition the maker-checker gate exists to catch. Whoever calculates this run should not be the same person who decides to skip withholding and release; get an independent checker's sign-off on this specific decision, in writing, before touching these two lines.
- If finance wants to accept the compliance risk anyway, that has to be an explicit, documented risk acceptance from someone with authority to accept it — not a default baked silently into the release.

**F-4 | open item, not yet a finding | 38 EU publishers** — Your network self-bills these publishers (generates the invoices on their behalf). That's a legitimate model, but the audit still has to verify the self-billed invoices match the audited commission total per publisher for the period, and that each cites the reverse-charge basis (Art. 196, Directive 2006/112/EC) against a VIES-verified VAT number. You haven't told me you've checked this — confirm it before treating the 38 EU lines as clean. This is check work, not a blocker by default, but don't skip it just because the network automated the paperwork.

**F-5 | material, needs resolution before the total is trustworthy | scope: PayPal-paid lines** — PayPal fees are being deducted from the commission line *before* it reaches your export. That means the $71,300 figure (and each affected payee's line) is net of a payment-rail fee, not the gross commission — which breaks the audit's basic rule: the audit verifies the *gross* commission, and any fee deducted downstream must be disclosed in the program terms, not silently netted in. Two separate problems follow from this:
1. **You can't sign off on $71,300 as "the commission run" until you know what it would be gross of fees** — the reconciliation you'd run against your source of truth needs the gross figure, or it will show a phantom variance that isn't an error, it's just the fee.
2. **Disclosure**: check the program terms — do they say PayPal payees bear this fee? If yes, this is just a reporting-accuracy fix (show gross and fee as two lines, not one netted line). If the terms are silent or say the program/platform bears it, you're underpaying every PayPal-fee-bearing payee by the fee amount, which is a payee-facing finding, not just a cosmetic one.

Get the gross figures from the network/PayPal before release; don't just wave this through because the net number is what's sitting in the export.

## What can release now vs. what can't

- **Hold**: the 1 payee with no W-9 ($4,800, pay $3,648 net after backup withholding once decision is confirmed) and the 1 French payee with the expired W-8BEN-E.
- **Confirm before releasing**: the 38 EU self-billed invoices reconcile to commission totals (F-4), and the true gross commission behind the PayPal-fee-netted lines (F-5) — this second one could still change the $71,300 total, so don't release those lines until you know the number is right.
- **Release**: the remaining payees not touched by F-1, F-2, F-4, or F-5, once someone other than the run's preparer has reviewed and signed off — that's your maker-checker gate, and it's the one control that would have stopped this from shipping wrong if it had been in place already.

## Sign-off

Preparer: (whoever built this run) | Checker: must be a different person, not the finance lead who proposed skipping withholding, since that's the decision under review | Release decision: **partial release** — clear everything except the 2 held payees and the 38+PayPal lines pending F-4/F-5 confirmation.