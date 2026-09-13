# Building the SaveSnap Fraud Case — Kestrel Outdoors

## The report your CFO is reading is a known false-positive shape

38% last-click share, 6x program-average conversion, and almost no upstream traffic is the textbook signature of a **checkout-moment browser extension partner** — coupon/toolbar/extension partners sit right before purchase and win last-click credit on demand that other channels (paid search, email, content) actually created. That's a repricing problem by default, not fraud. A high last-click share is _never itself_ evidence of fraud on its own.

The same numbers are also consistent with **attribution hijacking**: the extension overwrites an earlier affiliate's cookie at checkout instead of standing down, stealing commission from whoever actually earned the sale (this is what PayPal's Honey extension was removed over). That _is_ fraud.

⚠️ These two explanations look identical in the CFO's report. Last-click share and conversion rate cannot distinguish them. Only technical evidence can. Terminating on the numbers alone risks litigating an unfounded fraud allegation against a legitimate partner — the single most expensive failure mode in affiliate enforcement, and its own liability.

## Step 1 — Protect the money today without accusing anyone (do this now, before the next payout)

Move SaveSnap to **Hold & Investigate**, not Suspend & Escalate:

- Throttle new commissions to zero, pending review. Reversible — pay them if the evidence clears them.
- Open a dossier (template below) and start a cross-functional review (affiliate manager + finance, legal on call) within 24–48h.
- **Do not** terminate, and never use the word "fraud" externally yet. Instant termination destroys the exact evidence a network complaint or legal escalation would need. Tell SaveSnap only that commissions are "under routine quality review, update by [date]."

Check today whether your contract already has clawback authority + negative-balance carry-forward. If it doesn't, clawing back paid commissions is itself a breach of your own terms — that gates whether the CFO's 90-day ask is even executable.

## Step 2 — Collect the evidence that actually separates fraud from legitimate poaching

| Check                                                                                                                                                                                                                    | What it tells you                                                                                           | Trips on                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Cookie-drop reproduction**: clean browser, visit your site with SaveSnap installed, watch whether an affiliate cookie sets without a genuine click                                                                     | Direct evidence of forced/cookie-stuffed clicks                                                             | Nothing legitimate — a clean positive is hard technical proof                                                 |
| **Stand-down / attribution-flip audit**: for checkouts where another affiliate's cookie was already present, does SaveSnap's cookie overwrite it in the final ~60 seconds before purchase, recurring across many orders? | Hijacking a sale another partner earned                                                                     | A partner correctly programmed to stand down never shows this pattern                                         |
| **Redirect-chain + referrer capture**: declared traffic source vs. observed referrers on SaveSnap-attributed orders                                                                                                      | Referrer obfuscation, misrepresented source                                                                 | Deep-linked or flash-sale traffic can look similar — check the landing page first                             |
| **Chargeback correlation**: chargeback rate on SaveSnap-attributed sales, rolling 30 days                                                                                                                                | Stolen-card fraud riding the extension's attribution                                                        | Product-quality issues can also spike chargebacks — compare against other affiliates' rate in the same window |
| **Session/CTIT timing**: time between cookie-set and purchase                                                                                                                                                            | Non-human, near-instant patterns (<2s is the published academic threshold, [ACADEMIC] Snyder & Kanich 2016) | AI-generated synthetic sessions can now fake this — don't rely on it alone                                    |

Cross-referencing device fingerprints or shared IPs across accounts is personal-data processing (`[LEGAL REVIEW]`) — state lawful basis, retention period, and who can see matched records, and route to counsel before running it. Not needed for the checks above; only if the trail points to a multi-account ring.

## Step 3 — Run this in parallel: an incrementality test tells you whether it's a fraud problem or a pricing problem

Start with the **practical pause test** (cheapest, run it first — check your contract's notice obligations before flipping anything): pause SaveSnap commissions for 4–6 weeks and watch total conversion/revenue.

| Outcome             | What it means                                  | Action                                                                                                                                    |
| ------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| No revenue movement | SaveSnap was capturing demand, not creating it | Reprice to a lower commission tier, keep them as a partner — this is not fraud                                                            |
| Revenue drops       | SaveSnap is genuinely incremental              | Leave the rate alone; recalibrate whatever flagged them, and focus the fraud investigation strictly on the technical evidence from Step 2 |

Don't lean on either side of the incrementality debate as a given: one agency framework claims last-click overstates extension/coupon contribution by 30–40%; a comScore/Google study found 94% of coupon-affiliate-driven transactions were incremental. Both are cited with an agenda. Test your own program.

## Step 4 — Decision: what actually justifies the CFO's ask

| If the evidence shows                                                                                                                                   | Band                                 | Action                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 38% share + 6x conversion, nothing else — pause test shows no revenue movement                                                                          | **Watch → reprice**, not enforcement | Route to a lower commission tier via your payout-audit/commission-structure process, not fraud enforcement                                                                                                                                                                                                                                                                                                                                                                                                |
| Confirmed cookie-drop reproduction, OR a recurring attribution-flip pattern with no stand-down, OR chargeback rate >3%/30 days concentrated on SaveSnap | **Suspend & Escalate**               | Suspend → reverse/void the _violation-period_ commissions (not automatically all 90 days — clawback attaches to the commissions the dossier substantiates as fraudulent) → clawback paid amounts via negative-balance carry-forward, if your contract authorizes it → terminate → file the dossier with network compliance → legal review if cookie-stuffing is confirmed (federally prosecutable wire fraud; the only adjudicated figures are the eBay cases — $28M scheme: 5 months prison + $25K fine) |
| Ambiguous / partial signal                                                                                                                              | **Hold & Investigate**, extend       | Keep throttling, widen the sample, don't let "CFO wants it now" collapse this into Suspend & Escalate without evidence                                                                                                                                                                                                                                                                                                                                                                                    |

A blanket "claw back the last 90 days" only holds up if the dossier shows fraud running that whole period — size the clawback to what the evidence actually covers, not to a round number.

## Dossier template — fill this as you go

```
DOSSIER 2026-0XX — partner "SaveSnap" (platform ID: ___)
Rules triggered   : [list evidence hits from Step 2 with timestamps]
Baseline vs seen  : program avg conversion ___% vs SaveSnap ___%; last-click share ___%
Evidence          : cookie-drop repro [pass/fail]; stand-down audit [n flips, timing];
                    redirect/referrer capture; chargeback rate comparison
Financial exposure: commissions held $___; paid last 90d $___; at risk $___
Declared vs seen  : declared traffic source ___ ; observed referrers ___
Pause-test result : [pending / no movement / revenue drop, date range]
Prior history     : [any past flags on SaveSnap]
Recommendation    : [Watch-reprice / continue Hold / Suspend & Escalate], reviewer: [name, not the detecting analyst]
Appeal            : neutral notice sent [date]; 14-day window open until [date]
```

## What I still need from you to finalize this

1. Does your affiliate contract require extension partners to "stand down" when an earlier affiliate is already in the clickstream, and does it currently authorize clawback + negative-balance carry-forward? (This gates whether the 90-day clawback is executable at all.)
2. Client-side pixel or server-side postback tracking? Cookie-stuffing evidence needs server-side confirmation — a client pixel alone can't distinguish a stuffed cookie from an organic one.
3. Current commission validation/hold window length, and program size (affiliate count, monthly commission spend) — this determines whether manual review or scoring is the right investigation mode.
4. Any prior incidents with SaveSnap or other extension partners, and whether commission was ever recovered before.

## Framing this for the CFO

Report progress in commission-dollars held/recovered, not risk language: "$X held pending investigation, pause test running through [date], recommendation by [date]." Don't pre-commit to "fraud" in front of the CFO before the dossier is complete — if the evidence comes back clean, the honest recommendation is repricing, and walking that back after "terminate for fraud" was said out loud costs more credibility than taking two weeks to do this right.
