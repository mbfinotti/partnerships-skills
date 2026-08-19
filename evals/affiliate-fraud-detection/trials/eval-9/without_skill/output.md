## The core problem: the hold is solving the wrong failure mode

A 60-day hold protects against disputes that surface *early* — stolen cards, immediate refund requests, remorse cancellations. Your losses came from disputes at **month 11 and month 14** — 9 to 12 months after commissions were already paid out. The hold expired long before the fraud signal appeared. Extending it to 90 or 120 days won't fix this; the problem isn't hold *length*, it's that hold and clawback rights are the same mechanism.

At $890/sale, $18K ≈ 20 disputed subscriptions concentrated in 2 of 120 affiliates — a targeted pattern, not background noise.

## What's likely happening

Month 11/14 timing on an *annual* plan points to one of two patterns, both affiliate-side:
- **Self-referral / friendly fraud**: affiliate refers complicit "customers" (themselves, associates, or paid signups) who use the product for the full term, then dispute the charge as "unrecognized" once your hold window has closed — keeping both the year of service and the commission.
- **Renewal-adjacent disputes**: customers signed up for reasons unrelated to the product (incentivized/misleading offer from the affiliate), get billed on renewal, and dispute rather than cancel.

Either way, the affiliate already has the money, and your hold released it before the risk materialized.

## Immediate actions on the two affiliates

1. **Suspend both pending investigation** — pause new commission accrual and any unpaid balance.
2. **Audit their full referral history**, not just the disputed accounts: signup IPs, device fingerprints, card BINs, email patterns, time-to-first-use. Self-referral rings cluster.
3. **Claw back the $18K** from any current/future balance owed to them, and terminate for cause if the audit confirms self-dealing — cite it explicitly in the termination notice.

## Structural fixes

1. **Decouple "hold" from "clawback rights."** Add a contract clause: *any* chargeback, at any point in the subscription term, is deductible from the affiliate's account — via reserve, negative balance, or offset against future commissions — regardless of when it occurs. The hold controls cash-flow timing; clawback rights should never expire while a customer relationship exists.
2. **Split commission payout, don't just delay it.** Pay a partial commission at day 60 (e.g. 50%), and the remainder at the point risk actually resolves — renewal, or month 12 for an annual plan. This aligns payment timing with when your real dispute exposure occurs, instead of an arbitrary 60-day guess.
3. **Add a rolling reserve.** Withhold a fixed % (5–10%) of every affiliate's commissions into a reserve that only pays out quarterly, net of that period's clawbacks. This gives you a recovery pool even for chargebacks that land after normal payout.
4. **Monitor per-affiliate chargeback rate, not just aggregate.** Set a threshold (e.g. >2% of an affiliate's referred customers charge back within the subscription term) that auto-flags for manual review and pauses payout — this would have caught these two affiliates well before $18K.
5. **Watch for concentration/velocity signals at signup**, not just at dispute time: shared cards/IPs/devices across "different" referred customers from the same affiliate, or an affiliate whose referred customers show unusually low product usage.
6. **Tighten the affiliate agreement**: explicitly prohibit incentivized or self-referred signups, require disclosure of traffic sources, and state that any confirmed violation triggers full clawback plus forfeiture of pending balances — not just the disputed transactions.

## Priority order

Do 1–3 (the two affiliates) this week. Do 4 (clawback clause + reserve) before your next commission run — it's a contract/process change, not engineering work. Build the per-affiliate monitoring (7) over the next month; it's what turns this from "we noticed after $18K" into "we caught it at $2K."