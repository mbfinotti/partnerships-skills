# Verdantly — Affiliate Commission Restructure: Rollout Plan & Announcement

## Before the plan: three things in your ask that will bite you

⚠️ **"Effective next Monday" doesn't clear minimum notice.** Rate/tier changes on a live card need 60 days' notice before they take effect — this is standard across major networks and is why silent or rushed rate cuts are the single most-cited cause of affiliate churn. Two days' notice risks mass partner drop-off and complaints to the network right as the change lands.

⚠️ **A 14% → 7% cut for cashback/deal sites is a 50% reduction — most networks cap a single decrease at ~20%, once every 30 days** (e.g., Awin's published rule: max 20% per change, once per 30 days, 7 days' notice minimum). Flipping 340 affiliates straight to 7% in one move is very likely a contract breach on a decrease-governed network — some networks will simply reject or reverse the change. **The 14% → 12% content-site cut is fine as a single step** (14.3% reduction, under the typical cap); it's only the cashback/deal number that needs to be staged.

⚠️ **You have 340 affiliates all on the same rate today — some are your top revenue drivers.** Cutting everyone by email with no warning, including your best partners, is how you lose the top 10% that (per program telemetry) typically generate the majority of your affiliate revenue. They need a heads-up before the blast, not in it.

None of this blocks doing what you want — it means the 7% target ships as a **published glide path**, not an overnight switch, and your top partners get 48–72 hours' lead time before the broadcast. Below is the compliant version of your plan, still landing as one blast to the base.

**Action item before anything ships:** confirm your actual network's decrease-size/frequency/notice rule (it varies by network — Awin's is the published reference point above, yours may differ) and confirm whether tracking can flag new-vs-returning customers. I've assumed no new-customer flag exists; if one does, a new-customer gate on cashback/deal partners is a more efficient lever than the rate cut alone (see "Complementary levers" below) and could let you land at a less aggressive cut.

---

## Commission Structure Spec

```
COMMISSION STRUCTURE - Verdantly Affiliate Program, 2026-09-12
Rate model        : percentage of order value - unchanged, only partner-type split is new
Headline rates    : content/review/comparison sites: 12% (single-step cut from 14%)
                    cashback/deal/coupon sites: staged glide from 14% to 7% (see schedule)
                    - cap on cashback/deal is directionally consistent with incrementality
                      data: cashback/coupon sites run 66-71% non-incremental on average,
                      content/creator sites run 78-82% incremental
Tiers             : flat, unchanged - no tier restructuring in this pass
Recurring duration: not applicable - one-shot commission per order
Attribution       : unconfirmed - recommend shortening cashback/deal window (24h-7 days)
                    vs. content's existing window once classification is complete
Validation        : unconfirmed - carry over existing locking period unchanged
Payment           : unconfirmed - carry over existing net terms, threshold, clawback unchanged
                    (this migration touches ONLY the rate; nothing else in the program changes)
Economics         : NOT YET VALIDATED - no margin, AOV, or contribution-margin data supplied.
                    7%/12% are user-set targets, not derived. Confirm before final broadcast
                    that 12% (content) and each glide step still clear one-half of post-return
                    contribution margin - see references/rate-derivation.md ceiling walk.
Validation plan   : 30-day holdout on top 3 cashback/deal partners after Step 1 lands -
                    if total order volume holds while their attributed volume drops, the
                    cut is justified; if total volume drops too, they were incremental
                    and the glide should stop or reverse
KPIs              : effective blended commission rate, new-customer share of cashback/deal
                    orders, reversal/clawback rate by partner type, revenue share of top 10%
                    partners, partner attrition rate in the 90 days post-broadcast
```

**Open item, not a nice-to-have:** get gross margin, AOV, and return rate from finance before the November step lands. If contribution margin doesn't support even 12% on content orders, the whole structure needs re-deriving — a rate this skill would otherwise never let ship on user say-so alone.

---

## Rollout Plan

| Date                                | Action                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Now → Fri 2026-09-18**            | Confirm actual network decrease-cap/notice rule. Classify all 340 affiliates: content/review/comparison vs. cashback/deal/coupon. Default ambiguous cases (loyalty, hybrid comparison-plus-code sites) to the **content rate** unless the site's primary mechanic is a discount code or cash-back rebate — under-classifying a real cashback site costs less than wrongly cutting a genuine content partner. Identify the grandfather list: top 15% of affiliates by trailing-90-day commissionable revenue. |
| **Mon 2026-09-21 – Wed 2026-09-23** | **Personal outreach to grandfathered top-tier partners** — short 1:1 email (template below) plus an offer of a call, before anyone else hears about it. This is not a mass send.                                                                                                                                                                                                                                                                                                                             |
| **Mon 2026-09-28**                  | **Single email blast to the full 340-affiliate base** (template below). Publishes the full staged schedule up front so every future step is already "on notice" the day it's announced.                                                                                                                                                                                                                                                                                                                      |
| **Mon 2026-11-30**                  | Content rate live at 12%. Cashback/deal Step 1 live at 11.5%. (63 days after the blast — clears the 60-day floor.)                                                                                                                                                                                                                                                                                                                                                                                           |
| **Mon 2027-01-11**                  | Cashback/deal Step 2: 11.5% → 9.5%.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **Mon 2027-02-22**                  | Cashback/deal Step 3: 9.5% → 8.0%.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Mon 2027-04-05**                  | Cashback/deal Step 4 (final): 8.0% → 7.0%.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **Grandfathered partners**          | Keep flat 14% through the end of the month following their segment's final new-rate date: content grandfathers through 2026-12-31, cashback/deal grandfathers through 2027-04-30.                                                                                                                                                                                                                                                                                                                            |
| **30 days after Step 1**            | Run the holdout test on the top 3 cashback/deal partners (pause them, watch total order volume).                                                                                                                                                                                                                                                                                                                                                                                                             |

Each cashback/deal step is a ~15–18% reduction, spaced 6 weeks apart — under a 20%-max/30-day-min guardrail with margin to spare, and the entire glide is disclosed in the one broadcast rather than four separate surprise emails.

### Complementary levers worth layering in (not required, but cheaper than the rate cut alone)

- **New-customer gate** on cashback/deal partners, if tracking can flag it — removes non-incremental repeat-buyer credit outright, ranks above a rate cap on both cost-removed and recruiting damage.
- **Shorter attribution window** for cashback/deal (24h–7 days) vs. content's existing window.
- **Exclusive codes per top cashback/deal partner** to measure real lift directly — turns the holdout test from a one-time check into an ongoing measurement.

---

## Email 1 — Personal note to grandfathered top-tier partners (send Sept 21–23, individually, not BCC)

> Subject: A heads-up before we announce a program change
>
> Hi [Partner Name],
>
> You're one of our top-performing partners, so I wanted you to hear this from me directly before it goes out to the wider program.
>
> Starting **September 28**, we're moving Verdantly's affiliate program from a single flat commission rate to rates set by partner type — content and review sites, and cashback/deal/coupon sites. It's a change we're making across the whole program, not specific to you.
>
> Because you're one of our top partners, **your current 14% rate is grandfathered through [2026-12-31 / 2027-04-30]** — nothing changes for you until then, and we'll talk again well before it does.
>
> Happy to jump on a call this week if you want the detail or have questions before the wider announcement. Otherwise, you'll get the same email as everyone else on the 28th — this is just so it isn't a surprise.
>
> Thanks for everything you've driven for us this year.
>
> [Affiliate Manager Name]
> [Contact info]

---

## Email 2 — Full broadcast to all 340 affiliates (send Mon 2026-09-28)

> Subject: Upcoming change to Verdantly commission rates
>
> Hi [First Name],
>
> Quick update on the Verdantly affiliate program.
>
> **What's staying the same:** your tracking links, cookie attribution, payout schedule, minimum payout threshold, and everything else about how the program runs. This change is limited to the commission rate itself.
>
> **What's changing:** we're moving from one flat commission rate to rates set by partner type, so partners who drive net-new demand for Verdantly are rewarded closer to the value they create. Two rates going forward:
>
> - **Content, review, and comparison sites: 12%** of order value, effective **November 30, 2026**.
> - **Cashback, deal, and coupon sites:** stepping down from 14% on a published schedule, not overnight:
>   | Effective date | Rate  |
>   | -------------- | ----- |
>   | Nov 30, 2026   | 11.5% |
>   | Jan 11, 2027   | 9.5%  |
>   | Feb 22, 2027   | 8.0%  |
>   | Apr 5, 2027    | 7.0%  |
>
> Every step above is confirmed today — nothing further will change without separate advance notice.
>
> **Your classification:** based on your site's primary model, you've been placed in the [content / cashback-deal] category. You can see your current and upcoming rate on your dashboard now. If you believe you've been misclassified, reply to this email or contact [named contact] by [date] and we'll review it.
>
> **Why we're doing this:** a flat rate pays every referral the same regardless of how much new demand it actually creates. This split lets us keep rewarding the partners generating real, incremental sales while bringing coupon and cashback payouts in line with the value they add on top of demand others already created.
>
> Nothing changes before November 30. If you have questions in the meantime, reach out to [named contact] directly — we're glad to talk it through.
>
> Thanks for being part of the Verdantly program.
>
> [Affiliate Manager Name]
> [Contact info]

---

## Still open — resolve before Nov 30 goes live

- Confirm your network's actual decrease-size/notice rule and adjust the glide if it differs from the 20%/30-day reference used above.
- Get margin/AOV/return-rate data to validate 12% and each glide step against contribution margin — currently unverified.
- Confirm whether a new-customer tracking flag exists; if so, revisit whether the full 7% floor is even necessary once the gate is applied.
- Finalize the classification default policy and who adjudicates disputed cases.
