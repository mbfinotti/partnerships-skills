## Affiliate Program Board Dashboard — 14-Month Review

### Name the constraint up front, don't hide it

Put this as a one-liner on slide 1 or in dashboard header, not buried in an appendix:

> "Partner ID is not currently passed from the affiliate platform into billing/CRM. We can measure acquisition and initial conversion with full confidence. Post-conversion metrics (retention, expansion) below are from a manual sample match, not automated — flagged accordingly."

This buys you credibility. A board that later discovers the gap on its own will trust every number less; a board told upfront trusts the ones you do show.

---

### Section A — Program Reach & Growth (source: affiliate platform export, high confidence)

- **Cumulative partners recruited** vs **active partners** (≥1 conversion ever) — 180 recruited is a vanity number; active count is the real one.
- **New partners recruited / month**, last 6 months — is recruiting still working or has it plateaued.
- **Conversions / month**, last 14 months, as a trend line — this is the headline chart.
- **% of partners with ≥1 conversion in trailing 90 days** — active vs dormant. Affiliate programs typically run 10–20% active; know your number before the board asks.

### Section B — Partner Concentration (source: same export)

- **Top 10 / top 20 partner share of total conversions** (Pareto chart). Boards ask "is this one partner or a real channel" — answer it before they do.
- **Median time-to-first-conversion** for partners who ever convert — tells you if the onboarding/enablement motion works or if it's a slow burn.
- **List of top 10 partners by conversions and by commission paid**, side by side — sometimes your biggest earner isn't your most efficient one.

### Section C — Conversion Economics (source: affiliate platform, call it "conversion economics," never "ROI" or "LTV")

- **Total commissions paid (14mo)** vs **total attributed initial contract value** at point of conversion — this is the only revenue figure the affiliate platform actually has, so label the ratio as **"payback on initial deal"**, not CAC and not ROI. Using either of those words invites a board member to ask about churn-adjusted LTV, which you can't answer at scale yet.
- **Blended commission per conversion**, trended — rising cost per conversion is an early warning sign worth surfacing even if you can't yet tie it to downstream value.

### Section D — Post-Conversion Signal (source: manual sample match — directional, label it clearly)

This is the section that actually answers "is this program worth investing more in," and it's the one you build by hand in the next two weeks, not the one you wait on engineering for.

**How to build it without a warehouse, in a spreadsheet, in ~2–3 days:**

1. Export all affiliate-attributed conversions (customer email/company, partner, date, initial deal value).
2. VLOOKUP/match by email domain or company name against your billing export (current plan, MRR, status) and CRM export (open opportunities, churn/downgrade flags, support escalations if tracked).
3. This is a one-time manual join of ~180–300 rows — tedious but entirely doable solo in the time you have.

**What to report from it:**

- **90/180-day retention rate of affiliate-sourced customers** vs company-wide average for the same cohort window.
- **Expansion rate** (upgraded/added seats) vs company average.
- **Current blended MRR of affiliate cohort** as a rough LTV proxy vs company average.
- Sample size and the caveat: _"directional, from a manual one-time match of N accounts, not a live pipeline."_

If the affiliate cohort retains/expands at or above company average, that's your strongest slide — it justifies budget. If it's below average, better the board hears it from you with a plan than discovers it later.

---

### Section E — The Ask (one slide, closes the deck)

Don't end on data — end on the fix:

- **What**: pass a partner/affiliate identifier as a hidden field or coupon-style code through signup into CRM and billing (custom field), so every future conversion is natively joinable.
- **Cost**: typically a small, one-time engineering task (form field + webhook/API write), not a data warehouse project.
- **Payoff**: next quarter's dashboard replaces Section D's manual sample with live, automated retention/expansion/LTV by channel — turning "conversion economics" into real program ROI.

---

### What NOT to put on the dashboard

- Don't show partner-level LTV or ROI — you don't have it, and a single wrong number here undermines the whole deck.
- Don't show "total pipeline influenced" unless you can defend the attribution logic live — vanity metrics get picked apart fastest in board Q&A.
- Don't bury the data-gap caveat in small print — say it out loud when you present Section D.

**Bottom line for the board:** the program is measurably recruiting and converting (Sections A–C, solid data); early signal on whether those customers stick and grow is positive/negative direction only (Section D, manual, labeled as such); closing the identifier gap (Section E) is a small ask that upgrades every future board deck from "trust me" to "here's the number."
