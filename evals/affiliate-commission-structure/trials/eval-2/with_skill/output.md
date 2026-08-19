## Verdict: No — don't go to 12% lifetime. Fix the duration, not the headline.

Your CFO is right that 25% lifetime is out of line, but your CEO's fix solves the wrong variable. Capping the duration removes more cost than cutting the rate does, and it's the only version of this that doesn't also gut the recruiting pitch.

### The math

Inputs: $89/mo, 84% gross margin, 3.3% monthly churn → average tenure = 1 ÷ 0.033 ≈ **30.3 months**.

- Revenue LTV = $89 × 30.3 ≈ **$2,697**
- Lifetime gross profit = $2,697 × 84% ≈ **$2,265**

For a flat % paid for the life of the account, total commission as a share of LTV **equals the headline rate itself** — that's what makes today's number easy to diagnose:

| Structure | Total paid/customer | % of LTV | % of gross profit | Passes ceiling? (5–15% LTV, ≤30–40% GP, both must hold) |
|---|---|---|---|---|
| **Current: 25% lifetime** | $674 | 25.0% | 29.8% | ❌ — LTV leg fails hard (25% vs 15% cap); GP leg only just scrapes in |
| **CEO's fix: 12% lifetime** | $324 | 12.0% | 14.3% | ✅ technically clears both legs |
| **25% capped at 12 months** *(headline unchanged)* | $267 | 9.9% | 11.8% | ✅ clears with more room, and cheaper than the CEO's plan |
| **30% capped at 12 months** | $320 | 11.9% | 14.1% | ✅ clears, at ~the same cost as 12% lifetime |
| **Taper: 25%→12.5% at month 6** | $200 | 7.4% | 8.8% | ✅ cheapest, but needs a second rate step |

So 12% lifetime isn't a math error — it does pass the margin ceiling. It's a worse trade than the alternatives sitting right next to it:

- **A 12-month cap at your current 25% headline already costs less** ($267 vs. $324) than dropping to 12% lifetime, with nothing about the recruiting-facing number changing at all.
- **A 12-month cap at 30%** costs essentially the same as 12% lifetime ($320 vs. $324) but the number affiliates see goes *up* (30% vs. 12%) instead of collapsing to less than half. 20–30% recurring is the standard B2B SaaS band (HubSpot pays 30%/12mo, Notion 50%/12mo, Hunter.io 30%/12mo) — 12% sits below the floor of what serious SaaS programs advertise, so the CEO's plan trades the recruiting story away, it doesn't save it.
- Duration, not the percentage, is what was actually driving the overpay: at your churn/margin, lifetime pays out 2.5x the 12-month-cap cost for the *same* headline. That's the lever to pull first.

**Lifetime is also structurally the wrong duration model here even before the number.** It only belongs on the menu at all when margin > ~80% (you're at 84%, fine), churn < ~5% (you're at 3.3%, fine), *and* competing programs in your space actually pay lifetime. That third condition you haven't confirmed — worth checking before anyone even considers keeping "lifetime" in the pitch, since without it lifetime is off the table regardless of rate.

### Recommendation

Migrate to **25% for 12 months, uncapped headline unchanged** as the default move — it's the smallest, easiest-to-announce change ("your rate doesn't change, only how long it runs"), cuts commission spend from $674 to $267/customer (−60%), and isn't a rate decrease at all, so it doesn't trip the network's rate-cut guardrails (most networks cap decreases at 20% per change, once per 30 days, with notice) — you're only changing duration.

If leadership wants to actively use this as a recruiting upgrade rather than a quiet fix, **30% capped at 12 months** costs about the same as the CEO's 12%-lifetime idea while more than doubling the advertised number.

Either way:

```
COMMISSION STRUCTURE — Stackline Ops affiliate program, 2026-09-12
Rate model        : % of recurring revenue (unchanged) — one field, constant effective rate at every plan size
Headline rate      : 25% (keep as-is) — recommended; or 30% if the goal is an explicit recruiting upgrade
Recurring duration : capped at 12 months, down from uncapped lifetime — 9.9%/11.9% of LTV vs 25% today,
                      inside the 5-15%-of-LTV / ≤30-40%-of-gross-margin band; lifetime removed from the menu
                      pending confirmation that competing programs actually pay lifetime
Attribution        : unchanged unless you want to revisit — 60-180 day cookie is the B2B SaaS norm for
                      long sales cycles
Validation         : tie to trial-to-paid conversion + refund window, 30-60 day hold (unchanged unless
                      current terms differ)
Payment            : net-30, $50-100 minimum threshold, standard clawback + negative-balance carry-forward
                      on refund/chargeback/in-window cancellation (unchanged)
Economics          : ceiling shown above; can't confirm the "below blended CAC" leg of the pass threshold
                      without your current CAC — send it and I'll close that check
Validation plan    : 30-day holdout on top-volume partners; track new-customer share before/after migration
KPIs               : cost per incremental affiliate customer vs. blended CAC, effective commission rate,
                      reversal/clawback rate, revenue share held by top 10% of partners
```

### One thing not to skip on rollout

Don't strip the lifetime tail out from under affiliates who already have customers on it. Grandfather every currently-enrolled affiliate's *existing* referred accounts at 25% lifetime, apply the 12-month cap only to customers referred after the change, give 60 days' notice, and have direct conversations with your top partners before the broadcast goes out. A silent or retroactive cut on money partners think they've already earned is the reliable way to trigger exactly the partner churn this move is trying to avoid.

**Open items before this is fully locked**: your current blended CAC (needed to confirm the "below CAC" leg, not just the margin-ceiling leg), and whether any real competitor in your space publishes lifetime terms (this determines whether lifetime should even stay on the table long-term, independent of rate).