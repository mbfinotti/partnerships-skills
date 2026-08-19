## Cratefox — Lifetime vs. 12-Month Recurring Commission

### The ceiling (derived from your numbers, not from what competitors publish)

```
Price                        $129/mo
Gross margin                 61%
Monthly churn                7.5% → average tenure = 1/0.075 = 13.3 months
Revenue LTV                  $129 × 13.3 = $1,720
Gross-profit LTV             $1,720 × 61% = $1,049
```

SaaS ceiling rule: total lifetime commission per customer must sit at **5-15% of LTV**, and never above **30-40% of gross profit**. On these numbers that's **$86-$258** (LTV leg) and **$315-$420** (margin leg) — the LTV leg is tighter, so **$258 per customer is the hard ceiling**, whichever duration model you pick.

### Gate check on lifetime, before pricing it

Lifetime commission is only supposed to be on the table when gross margin is above ~80%, churn is under ~5%, and competitors already pay it. Cratefox clears one of three:

| Condition | Threshold | Cratefox | Pass? |
|---|---|---|---|
| Gross margin | > ~80% | 61% | ✗ |
| Monthly churn | < ~5% | 7.5% | ✗ |
| Competitors pay lifetime | — | yes | ✓ |

Two of three fail. That's the honest headline: on this cost structure, lifetime is the wrong tool even though two competitors are using it to poach your affiliates. I priced it anyway below, since you asked for a side-by-side to decide — but the numbers explain why it fails.

### Side-by-side pricing

Both headline rates below are set at the maximum each duration model can carry while staying inside the $258 ceiling — so this is each structure's *best competitive pitch*, not an arbitrary pick.

| | **12-month cap** | **Lifetime (uncapped)** |
|---|---|---|
| Headline rate | 24% | 15% |
| Monthly commission | $30.96 | $19.35 |
| Expected paid months* | 8.1 | 13.3 |
| Expected cost / customer | **$250.81** | **$258.00** |
| % of revenue LTV | 14.6% | 15.0% (exactly at ceiling) |
| % of gross profit | 23.9% | 24.6% |
| Ceiling headroom | small buffer | **zero buffer** |
| Hard max per customer | $371.52 (12 × $30.96) | **none — unbounded** |
| Headline recruiters see | 24% | 15% |

*Expected paid months accounts for your actual churn curve (geometric survival at 92.5%/month), not raw average tenure — a 12-month cap doesn't collect on customers who churn before month 12, and stops collecting on the ones who outlive it.

**The trap the table doesn't show directly**: because commission is a straight % of revenue, the ratio per customer never drifts — a lifetime customer always costs you exactly 15% of whatever they pay in. The risk isn't ratio, it's tail exposure. At your churn rate, about **1 in 108 acquired customers is still active — and still paying full commission — five years after signup**. Every cohort you ever acquire under lifetime terms keeps a standing, non-expiring commission liability on the books; a 12-month cap lets each cohort's liability retire on schedule, so your run-rate liability plateaus instead of compounding as the affiliate base grows.

### Recommendation

Publish **24% capped at 12 months**, not lifetime:

- It's a headline number that beats or matches most SaaS affiliate cards, and it's the number your affiliates can put in a comparison table against the competitors' lifetime pitch.
- Expected cost ($250.81) is essentially identical to what a 15% lifetime deal would cost you on average — you're not "underpaying" to avoid lifetime, you're paying the same expected dollar for a bounded, modelable liability instead of an open-ended one.
- Finance can hard-cap exposure at $371.52/customer. Lifetime has no such number, ever.

To blunt the specific competitive pressure (affiliates leaving for "lifetime" branding) without taking on the liability, add a **renewal bonus**: 5-10% of month-13+ renewal revenue, paid in arrears on confirmed billing. It keeps top affiliates earning past month 12 — which is the actual thing "lifetime" is selling them — without an unbounded per-customer tail. This is the standard fix for exactly this situation (losing affiliates to lifetime-advertising competitors on a product that can't structurally support lifetime).

### What's still open

- I don't have your current blended CAC, so I can't run the second half of the pass check (projected cost per acquired customer vs. blended CAC) — get that number before you finalize either option; if 12-month-cap cost ($250.81) is already above blended CAC, tighten the cap or headline further rather than reaching for lifetime to compete.
- If you go with 24%/12-month + renewal bonus, give existing affiliates at least 60 days' notice and grandfather current top performers at their existing terms for one cycle before rolling it out broadly — silent rate changes are the documented cause of the churn you're already seeing.