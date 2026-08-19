## Verdict

The shared single-screen dashboard works for a 4-person team. The separate weekly fraud tool is the right call too — fraud review needs a queue/workflow, not a tile. Two things to get right before building:

- **"Live" and "45-day validation" fight each other.** A 45-day window means any number shown for the last ~6 weeks is provisional. If the screen doesn't visually separate *pending* from *approved*, the CMO will read pending pipeline as booked revenue on day one.
- **"Same tiles for everyone" is fine only if tiles are status-segmented and drillable.** The CMO wants trend/ROI, the managers want an actionable queue. One screen can serve both if the top layer is aggregate and every tile drills into affiliate-level detail on click — don't build four dashboards, but don't flatten the roles into one generic view either.

Everything below assumes last-click attribution (state that assumption to your team explicitly — it determines who gets paid on multi-touch journeys).

## Main dashboard

**Default window:** Approved revenue defaults to a trailing 30-day view (matches the cookie window, matches how marketing already thinks in months). Never default to "last 45 days" as headline revenue — that number always looks artificially high because it includes stuff not yet validated.

**Refresh cadence — show it, don't fake it:**
- Clicks / sessions: near-real-time (every 2–5 min, whatever the network API actually supports)
- Orders / revenue tiles: every 15–30 min (matches typical affiliate platform → order system sync)
- Put a small "as of HH:MM" timestamp on every tile individually — clicks and revenue will legitimately be out of sync with each other, and an unlabeled staleness gap is what triggers "why don't the numbers match" arguments.

### Layout (top to bottom, same for CMO/PM/managers)

**Row 1 — Program pulse (live)**
| Clicks today (sparkline) | Orders pending validation | Approved revenue (30d) | EPC (30d) | Conversion rate (30d) |

**Row 2 — Revenue detail (15-30min refresh)**
| Revenue by partner type — content / coupon-deal / cashback / influencer / comparison | Top 10 affiliates by approved revenue, with 7d trend arrow | New order volume 24h vs prior 24h | Affiliate-channel AOV vs site AOV |

Split by partner type is the one non-negotiable tile for B2C ecommerce: coupon/cashback sites usually drive most volume but thinnest margin and most fraud, content/influencer drive the opposite profile. Lumping them hides which partner type is actually profitable.

**Row 3 — Operational queue (what makes managers actually open the screen)**
| Approval rate (approved / approved+declined, last 45d cohort) | Avg time-to-validation | New affiliate applications awaiting review (count, actionable) | Commission accrued this period + days to next payout |

**Interaction, not extra screens:** click any affiliate name/row anywhere → same-screen drawer with their click/order history, status breakdown, cookie-to-conversion lag distribution. That's how one set of tiles serves a CMO doing a 10-second glance and a manager doing a 20-minute dig, without forking the dashboard.

**Status color convention, applied everywhere revenue appears:** grey = pending validation, green = approved, red = declined/reversed. Never show a bare revenue number without one of these three next to it.

## Fraud tool (separate, weekly, managers only)

Not a dashboard — a working queue. Batch-run weekly, but auto-alert if the pending-decision queue spikes mid-week (a burst right before an affiliate's orders would hit day 45 and auto-approve is exactly the pattern to catch before money moves).

**Checks to build in, ranked by how commonly they bite B2C ecommerce programs:**
1. **Cookie stuffing / click-to-order velocity** — click and checkout separated by seconds, no site engagement in between.
2. **Coupon code leakage / brand bidding** — affiliate's code showing up on coupon-aggregator sites they weren't given it for, or bidding on your branded search terms.
3. **Last-click theft** — a coupon-extension affiliate's click lands seconds before checkout after a paid/organic session already existed. Classic attribution poaching, not necessarily "fraud" but should be a judgment queue.
4. **Self-referral / employee abuse** — device fingerprint or IP overlap between an affiliate's own accounts and "referred" customers.
5. **Refund/return rate spike** vs. site baseline, per affiliate — chargeback laundering shows up here before it shows up in finance.
6. **New affiliate + immediate high-value spike** — one of the highest-signal combos for click farms.
7. **Geo mismatch** — order ship-to geography inconsistent with the affiliate's stated audience.

**Tool output, not a chart:** a ranked queue of flagged orders/affiliates with the evidence inline, an approve/decline/hold action per row, running total of "$ flagged, pending decision," and a per-affiliate decline-rate trend to catch chronic low-grade offenders who never trip a single hard rule. Exportable to finance for clawbacks.

## Open items to settle before building

- Which affiliate platform (Impact, PartnerStack, Awin, Everflow, Tapfiliate, in-house)? It decides what's actually "live" — some only sync conversion status a few times a day regardless of dashboard polling.
- Confirm last-click attribution is in fact your model — it changes what "approved revenue" even means when a customer touches two affiliates inside the 30-day cookie.