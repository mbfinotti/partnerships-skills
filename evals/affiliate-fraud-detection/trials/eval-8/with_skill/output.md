## What this actually is

Zero observed traffic + last-click credit on customers who came in organically is not a low-incrementality dispute — it's the taxonomy's cookie-stuffing tell:

> "Tell: commissions on customers with no meaningful referral touchpoint."

Don't let DealBurrow's coupon-site-sounding name pull this into the "coupon partners are legitimate by default" bucket. That rule is for partners who *do* send traffic and just win last-click at checkout. DealBurrow apparently sends **no** traffic at all — that's a different, harder claim, and it needs technical evidence, not an incrementality test.

**The structural problem underneath it:** you track with a client-side pixel, and per the taxonomy, "a client-side pixel cannot distinguish a stuffed cookie from an organic one." That's exactly why this looks invisible from your data — your instrumentation is structurally blind to the one pattern you're describing. Fix the visibility gap before you trust any report this program produces going forward.

## Do this today (before the next payout)

1. **Throttle DealBurrow's pending commissions to zero.** Don't ban yet — an instant ban destroys the evidence a network report or legal referral would need. This is the "Hold & Investigate" band: reversible, hours of work, and it stops the bleeding immediately.
2. **Run the cookie-drop reproduction test.** Clean/incognito browser, visit DealBurrow's site and any pages/coupons they list for you, and check whether your affiliate cookie sets without a genuine click — hidden iframes, invisible pixels, injected redirects, forced redirects through intermediate domains. This is the single piece of evidence the rest of the case hangs on.
3. **Check for an extension/toolbar angle before you conclude it's stuffing.** If DealBurrow also runs a browser extension, the mechanism could instead be attribution hijacking (extension overwrites attribution seconds before checkout instead of standing down). Tell: last-click flipping from nothing/organic to DealBurrow right at purchase, with no upstream traffic. Same throttle-first response, but the reproduction test differs slightly (test the extension's checkout behavior, not just the site).
4. **Pull whatever server-side logs exist** (even partial: web server, CDN, order system) and check, for the flagged sales: referrer headers, redirect chains, and time between any "click" event and cookie-set. Near-zero time between click and cookie, or a redirect chain through unfamiliar intermediate domains, corroborates stuffing (Chachra, Savage & Voelker, IMC 2015: 84% of stuffed cookies in their sample arrived via typosquat/intermediate domains, 91%+ via redirects).
5. **Cross-check declared vs. observed.** What traffic source did DealBurrow declare at application (content? social? deals aggregation?) vs. what your logs actually show for their referred sales. Expect blank or mismatched referrers if this is stuffing.

None of this requires cross-account identity data (no `[LEGAL REVIEW]` gate) — it's server-log and reproduction-test work, which you can start immediately.

## Open a dossier now, not after you decide

```
DOSSIER — DealBurrow (platform/publisher ID: ___)
Rule(s) triggered   : commissions with no observed referral touchpoint (recurring);
                      [cookie-drop reproduction: PENDING — run today]
Baseline vs observed: 0 referrers/clicks recorded from this partner vs. N sales credited
Evidence             : reproduction test steps + screenshots (once run);
                      redirect-chain capture w/ timestamps (once run);
                      server-log excerpts, declared vs. observed referrer
Financial exposure   : $___ held pending / $___ already paid this cycle
Declared vs. observed traffic source: declared "___" ; observed "none/blank"
Prior history        : [note any prior flags on this partner]
Recommended action   : Hold & Investigate now → escalate to Suspend & Escalate
                      if reproduction confirms stuffing with technical evidence
Reviewer             : someone other than whoever raised the flag
Appeal               : not yet triggered (no enforcement action taken)
```

Fill the blanks as you run steps 2–5.

## Band the case correctly

- **Right now:** Hold & Investigate — throttle, cross-functional review (affiliate manager + finance, legal on call) within 24–48h. This is the default for a new flag and it's where you stay until you have confirmed technical evidence.
- **Move to Suspend & Escalate only if** the reproduction test confirms a cookie set without a click, or you find the hidden-iframe/redirect-injection mechanism directly. At that point: suspend, reverse/void the violation-period commissions, clawback anything already paid, terminate, send the evidence dossier to the affiliate network (they won't have caught this on their own — network compliance is reactive, acting on evidence you bring them, not proactive surveillance), and consider a legal referral if the dollar amount is material (cookie stuffing is prosecutable federal wire fraud in the US — the eBay cases are the only adjudicated numbers in this space: $28M/5 months+$25K fine, and $5.2M/15 months for a second operator).
- **If reproduction comes back clean** (no stuffing found) but the "no traffic" complaint persists, downgrade your working theory to attribution hijacking or a declared-source mismatch, not fraud, and revisit with the extension check from step 3.

## The two things that decide how much of this you can actually recover — tell me these

- **What's your commission validation/hold window today, and do you have clawback authority (negative-balance carry-forward, chargeback reserve) in your affiliate terms?** If commissions to DealBurrow have already *paid out* (not just accrued), whether you can get that money back depends entirely on this. No clawback clause means a confirmed fraud finding still can't recover money already sent — that gap gets fixed in the contract, not in a detection rule, and it's worth fixing before your next payout cycle regardless of how this specific case resolves.
- **Cookie window length and whether server-side postback capability exists at all** (even if unused) — determines whether you can move off the client-side pixel quickly or need a build cycle. Moving to server-side postbacks is the actual fix for "we can't tell if a cookie was stuffed" going forward; the pixel will keep producing exactly this ambiguity on every future case.

## Don't do, per the same evidence

- Don't ban DealBurrow before the reproduction test — you'll destroy the evidence you'd need for a network report or legal referral, and an unfounded fraud allegation is its own liability if you're wrong.
- Don't message DealBurrow using the word "fraud." Use neutral language: "your commissions are under review pending a routine quality check; expect an update by [date]." Keep the real reasoning and evidence internal.
- Don't treat "customers found us organically through search" as proof by itself — it's your team's belief, not measured data. The reproduction test and referrer audit are what actually establish it; use them to confirm or kill your own hypothesis before you act on it.

## After this case closes

Whichever way it resolves, feed it back into a standing rule so the next DealBurrow doesn't sit undetected for months: a signal like "commissions with zero observed referrer/click event, recurring" belongs in your rule set at Hold & Investigate by default, with the false-positive check named inline ("legitimate deep-linked/direct traffic with dropped referrer — check landing page and campaign calendar before treating as fraud"). That's a small addition once you've done the one-off work above — happy to help build the full standing rule set (baselines, monitoring cadence, KPI loop) once this case is resolved, since that's a materially bigger piece of work than today's cleanup.