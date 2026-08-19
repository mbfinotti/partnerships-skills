## Building the case against SaveSnap

### First: reframe what the CFO is looking at

38% last-click share, near-zero upstream traffic, 6x conversion — this is the signature of **browser-extension last-click hijacking**, not automatically "fraud." Coupon/cashback extensions (Honey, Capital One Shopping, and this SaveSnap pattern) fire their tracking cookie at checkout, often on sessions the shopper already started through another channel (organic, paid, email, direct). That structurally produces high conversion (they only ever touch bottom-funnel sessions) and low upstream traffic (they never drove discovery).

That pattern alone is **not proof of fraud** — it could be:
- Legitimate but low-value: the extension really is disintermediating your other channels, without breaking any rule.
- A contract/terms problem: not disclosed as required, or violates your program's cookie-stuffing clause.
- Actual fraud: cookie forced without a genuine user action (invisible pixel fires, auto-injected coupon fields, cookie dropped on page load rather than on click).

Calling it "fraud" and clawing back 90 days without evidence exposes Kestrel to a breach-of-contract counterclaim from SaveSnap and reputational risk if this becomes public. Build the evidence first, then pick the remedy.

### Step 1 — Attribution forensics (path-level data, not summary reports)

1. Pull raw multi-touch paths for every SaveSnap-credited order in the last 90 days: full click history per order, not just last-click winner.
2. Compute **time between SaveSnap's click/cookie-fire and checkout completion**. Under 60–120 seconds on a large share of orders is the strongest single tell — it means the cookie dropped at checkout, not during product research.
3. Check whether each session had an **earlier, non-SaveSnap touch** (organic, paid, email, direct) before the SaveSnap click. If yes, SaveSnap is overwriting existing intent, not creating it.
4. Re-run the same 90 days of orders under first-click and under a position-based/U-shaped model. If SaveSnap's share collapses from 38% to low single digits, that's your quantified damage number — useful for negotiation and for the clawback ask, independent of the fraud question.
5. Segment new vs. returning customers. Extensions disproportionately "catch" returning customers who were already buying — check if SaveSnap's share skews heavily returning.

### Step 2 — Technical verification (does it look like manipulation, or just aggressive marketing)

1. Install the SaveSnap extension yourself and run controlled test purchases across several product categories.
2. Watch the network calls: does the affiliate pixel fire the moment you land on any Kestrel page (even without opening the extension), or only when you actively click "find savings"? Silent, page-load-triggered fires are the closest thing to a smoking gun.
3. Check the "phantom coupon" pattern: does SaveSnap pop up a coupon box at checkout that applies **no discount**, or a discount identical to a code already public on your own site? If the extension inserts itself and takes credit while providing zero incremental value to the shopper, that undermines any claim SaveSnap is driving the sale.
4. Confirm consent/disclosure: did the shopper affirmatively invoke SaveSnap on this visit, or did the extension auto-activate?

### Step 3 — The decisive test: incrementality holdout

Forensics prove correlation; a holdout proves causation, and it's the standard the network (and SaveSnap, if they push back) will respect.

1. Pick a comparable traffic segment (by geography, device, or a random split) and suppress SaveSnap's tracking/cookie for 2–3 weeks.
2. Compare conversion rate and revenue in the held-out segment vs. the segment where SaveSnap still fires.
3. If conversion barely moves, SaveSnap is capturing sales that would've happened anyway — clean evidence of non-incremental, last-click-poaching behavior, and the basis for both termination and a clawback ask.
4. If conversion drops meaningfully, the CFO's fraud theory doesn't hold — SaveSnap may be annoying but is genuinely converting incremental demand.

### Step 4 — Contract and policy review (run in parallel, not after)

1. Pull the actual affiliate agreement / network T&Cs (Impact, Awin, CJ, Rakuten Advertising — whichever hosts this program). Check the specific clawback clause: most only cover returns/chargebacks/canceled orders, not "we didn't like the attribution mix." If yours doesn't cover attribution disputes, a 90-day clawback needs either a fraud finding or a negotiated settlement — not a unilateral CFO decision.
2. Check the network's browser-extension/coupon-extension policy — most major networks (Impact, Awin) have a specific extension category with disclosure and cookie-behavior rules. If SaveSnap violates that policy, you have network-level leverage (the network can suspend/investigate, which is more defensible than a solo accusation).
3. Ask the network's compliance/fraud team whether SaveSnap is already flagged by other advertisers — this pattern is common enough that networks keep informal records.
4. If US-based, note the FTC's stance on cookie-stuffing and non-disclosed extension behavior — relevant context, not something to cite publicly.

### Decision matrix

| Evidence found | Defensible action |
|---|---|
| Cookie fires on page load without user action, or phantom coupons, or holdout shows no incrementality | Terminate for fraud/policy violation; clawback is defensible — cite the specific evidence, not just the last-click %. |
| Cookie only fires on genuine click, holdout shows real incrementality, but overwrites other channels | Not fraud — renegotiate to a lower "assist" commission tier or exclude last-24h-before-checkout attribution window. No clawback. |
| Mixed / inconclusive | Put SaveSnap on a shortened cookie window or non-last-click model for 30 days as a trial, re-measure, decide from there. |

### Sequencing

1. **Week 1**: Pull path-level data (Step 1) and start the network policy check (Step 4) in parallel.
2. **Week 1–2**: Run the manual technical test (Step 2) — this is fast and often decisive on its own.
3. **Weeks 2–4**: Run the incrementality holdout (Step 3) — this is the piece that turns "we suspect" into "we proved."
4. **Week 4**: Bring findings to legal/network before any termination or clawback notice goes out — don't let the CFO send a fraud accusation before the evidence package exists.

### What to tell the CFO now

Termination is likely justified either way — even a "legitimate but low-value" SaveSnap can be cut for margin reasons without calling it fraud. The 90-day clawback is the part that needs the evidence package above, because it converts a business decision into a legal claim. Get the holdout test and the technical check done before sending anything to SaveSnap in writing.