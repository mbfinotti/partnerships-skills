## Does the plan work? Two things don't — before the layout

**"Same tiles for everyone" breaks on contact with the skill's own negative example.** It exists to warn against exactly this ("One live leaderboard for everyone is a single view with a single refresh rate: executives get noise, operators get no alert design"). A CMO drowning in a partner leaderboard and reversal-by-reason chart won't look at it twice; affiliate managers without EPC/click-to-conversion/leaderboard will miss the daily anomalies they're supposed to catch. Executive and operator views differ in _metrics_, not just density.

**A separate fraud tool checked weekly breaks a stated ground rule**: "Keep fraud and compliance signals on the same view as performance, never in a separate tool — daily decision-makers need both at once." Reversal spikes and single-partner share spikes are money-at-risk signals; walling them off into a weekly-only tool means five days of exposure before anyone looks.

Neither problem kills "one thing everyone opens." Fix: **one dashboard, two tabs** (Executive / Operator), and the fraud signals live as an always-on alert strip on the Operator tab — the "weekly fraud check" becomes the _review ritual_ for that same strip, not a separate system.

One more correction: "live-refreshing" for the whole screen is itself a defect the skill calls out explicitly — one refresh rate for every tier is wrong. Only the operational tier (reversal %, click-to-conversion, pending$, single-partner share) should be near-live; contribution/cost-of-sale/concentration move slower and should refresh daily/monthly/quarterly, not continuously.

No canonical affiliate-dashboard framework exists — IAB/PMA publish guidance only, not a standard. This spec is one program's spec, not a branded methodology.

Since you asked for the finished deliverable rather than a round of interview questions, I built this on stated defaults (the B2C spine, last-click attribution, standard order-level dimensions) and flagged every guess in **Open items** — correct any of them and the spec updates accordingly.

---

```
DASHBOARD SPEC - [Program name]
Header    : audiences: CMO (exec, monthly-paced reads) + program owner (both tabs,
            daily) + 2 affiliate managers (operator, daily); source of truth: orders
            database, reconciled to affiliate-network export (network stays source
            for clicks/traffic only); timezone [CONFIRM], transaction-date basis for
            orders / validation-date basis for payables, currency [CONFIRM], 30-day
            cookie, 45-day validation window, attribution model assumed last-click
            [CONFIRM]
Data foundation: billing/orders spine (default - cheapest, matches "no analyst
            hours specified"). Promote to customer-file join only if new-to-file
            needs identity resolution beyond order history [CONFIRM data sources].

Metrics   :
 Net program contribution | attributed net revenue (net of returns, excl.
   tax/shipping) - (validated commission + network fees + agency fees +
   placement fees), monthly, validated only | Business | Orders DB | tile
   + 13-mo line | positive & growing | 2 consecutive down months | [DERIVE]
 Cost of sale | (validated commission + network + agency + placement fees) /
   attributed net revenue, monthly | Business | Orders DB + platform | tile
   | own target [DERIVE] | breach target | [DERIVE]
 Attributed ROAS vs ROI | ROAS = attributed rev / program spend; ROI =
   attributed rev / (program spend + COGS); labeled "last-click, 30-day
   cookie"; monthly | Business | Orders DB + finance | paired tiles | own
   baseline | -20% vs 3-mo mean | formulas [VENDOR glossary], targets [DERIVE]
 Top-10% / top-5-partner concentration | top-decile / top-5 validated revenue
   / total program revenue, quarterly | Business+Health | Orders DB | exec
   tile | own band | top-5 >= 50% | threshold [VENDOR], band [DERIVE]
 New-to-file rate | first-ever customers / affiliate-attributed orders,
   order-level, monthly, by partner type | Input | Orders DB (partner ID
   stamped at order) | line by partner type | >= own baseline [DERIVE]
   | drop below baseline | [DERIVE]
 Reversal / return rate | reversed orders / total attributed orders,
   validation-date basis, continuous | Health | Orders DB | line vs band
   | < own band [DERIVE] | > 2 SD vs 30-day mean | [DERIVE]; >10% signals
   quality problem [VENDOR]
 AOV net of returns, by partner type | net order revenue / orders, excl.
   tax+shipping, monthly | Input | Orders DB | bars | own baseline | n/a,
   diagnostic | [DERIVE]
 Click-to-conversion rate | orders / unique clicks x 100, per partner,
   continuous | Input | Network export + Orders DB | line | own baseline
   | -2 SD vs 30-day mean | click convention [CONFIRM: unique/bot-filtered]
 Active-affiliate rate | affiliates with >=1 validated order in 60 days /
   enrolled, monthly | Health | Network | tile | own band | < own band
   - X pts | [DERIVE]; 10-30% typical [VENDOR]
 Checkout-adjacent revenue share | coupon+cashback+extension validated
   revenue / program revenue, monthly | Health | Network | stacked area
   | own band | +10pt in a quarter -> incrementality review | [DERIVE]

Views     : ONE dashboard, ONE URL, TWO tabs (program owner has both; CMO
            defaults to Exec; affiliate managers default to Operator):

  EXEC tab (CMO + program owner, daily-refresh, not continuous):
  +-------------------------------------------------------------------+
  | NET CONTRIBUTION  | COST OF SALE | ROAS/ROI    | TOP-5 SHARE       |
  +-------------------+--------------+-------------+-------------------+
  | Revenue trend (13 mo)              | Revenue by partner type      |
  +-------------------------------------+-------------------------------+
  | Checkout-adjacent share (stacked)                                  |
  +-------------------------------------------------------------------+
  | ALERT STRIP: concentration breach | reversal trend | window changes|
  +-------------------------------------------------------------------+

  OPERATOR tab (program owner + 2 affiliate managers, near-continuous):
  +-------------------------------------------------------------------+
  | CLICK-CONV %  | REVERSAL % | PENDING vs   | 1-PARTNER SHARE        |
  | (vs 30d)      | (vs band)  | APPROVED $   |                        |
  +---------------+------------+--------------+------------------------+
  | Daily validated conversions (6 wk)  | Reversals by reason          |
  +---------------------------------------+-------------------------------+
  | Affiliate leaderboard: validated comm | orders | new-to-file% |     |
  | reversal% | AOV | delta vs prior period (sortable, full tail)      |
  +-------------------------------------------------------------------+
  | ALERT STRIP: reversal spike | 1-partner share spike | click-conv   |
  | anomaly | [brand-bidding flag, if PPC partners exist]              |
  +-------------------------------------------------------------------+

Dimensions: partner, partner type (content/coupon/cashback/sub-network/
            influencer/email/PPC), product category, geography, device.
            Landing page / creative parked - see Open items.

Cadence   : continuous/daily - click-conv, reversal%, pending vs approved,
            1-partner share, compliance flags (Operator tab)
            weekly - new partners onboarded, conversion-to-active, tail
            activation (recruiting/activation review)
            monthly - net contribution, cost of sale, ROAS/ROI, new-to-file,
            active-affiliate rate (CMO + program owner business review)
            quarterly - top-10%/top-5 concentration, checkout-adjacent
            share trend, cohort curves (commission-architecture review)

Alerts    : reversal-rate spike > 2 SD vs 30-day rolling mean -> affiliate
            managers, [channel CONFIRM], same-day response
            single-partner share +10pt in 7 days -> program owner,
            [channel CONFIRM], 24h
            click-to-conversion anomaly -2 SD vs 30-day mean -> affiliate
            managers, [channel CONFIRM], 48h
            brand-bidding/trademark flag -> parked, promote immediately
            if any partner runs paid search (see Open items)

            Weekly ritual (replaces the standalone "fraud tool"): every
            [day CONFIRM], program owner + both affiliate managers walk
            the Operator alert strip and alert log together - same data,
            scheduled attention, not a separate system. Deep fraud-rule
            definitions still belong to the fraud-detection skill; this
            dashboard only surfaces the signals.

Open items: - Program size/age, commission model detail, monthly spend -
              not provided; needed to set realistic [DERIVE] targets/bands.
            - Timezone, currency, exact attribution model (assumed
              last-click) - unconfirmed.
            - Whether partner ID reaches the order record today - if not,
              new-to-file and AOV-by-partner-type are not computable yet;
              stamping it is a week of work per the skill's cost model.
            - Whether partner type/promotional method is captured per
              partner - assumed yes; if not, demote partner-type slicing
              and checkout-adjacent share until classification exists.
            - Refresh capability (live query vs daily batch) - assumed
              sufficient for the continuous tier; confirm before promising
              near-real-time tiles.
            - EPC and time-to-first-conversion - next candidates after
              the above nine, cheap once click convention and link-
              activation timestamps are confirmed; parked, not deleted.
            - Brand-bidding alert - needs SERP monitoring; only worth
              building once PPC partners are in the program.
            - Existing review meetings, current pain point, deadline for
              v1, and analyst hours available - none stated; all of these
              re-rank the menu above and should be confirmed before build.
```

**Why this passes the threshold once the Open items are answered:** contribution, cost of sale, and top-5 share sit on one view (Exec); every row states formula/window/counting method; every alert has an owner and response time; validated-not-gross throughout; sourced/influenced summation isn't a risk here since B2C has no sourced-vs-influenced split. What it does _not_ yet pass: several targets are placeholders until program history exists to derive real bands, and three data-availability assumptions (partner ID on order, partner-type capture, refresh capability) are unconfirmed — treat those as the first things to verify before anyone builds this in a BI tool.
