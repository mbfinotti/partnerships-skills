## Before anything else

This is a draft for review by qualified counsel, not legal advice. Program terms — including the data protection clause below — are legally binding once affiliates click "I agree." Every `[LEGAL REVIEW: ...]` marker must stay in the document until your DPO/counsel has actually cleared that specific point — don't strip them for a "clean" version to send round.

I'm answering scoped to what you asked (the GDPR role question + the Data Protection clause), not drafting the full 20-section agreement. I assumed: in-house program (you said "our own first-party script," not a network), no personal data currently shared back to affiliates (no lead lists, no co-branded data pools), and the tracking script runs solely on Kastellan's own domain/app. If any of those are wrong, the answer below changes — say so and I'll redo it.

## The straight answer

**Not processors — on your specific facts.** GDPR Art. 4(8) defines a processor as an entity that processes personal data _on behalf of_ and _under the instructions of_ a controller. Your affiliates never touch personal data in that sense: they publish a link containing an affiliate ID (not personal data), the visitor clicks through, and from that point your own first-party script — running on your domain, under your sole control — does 100% of the cookie-setting, attribution and conversion logic. Nothing personal-data-shaped flows from Kastellan to the affiliate, and nothing flows back except "affiliate X gets credit for a sale." There's no instruction relationship because there's no processing relationship to instruct.

To the (minor) extent an affiliate's own site logs its own visitors clicking your banner, that's the affiliate acting as an **independent controller of its own website analytics** — its own purpose, its own means, nothing to do with you.

**Why this isn't a dodge of the "genuinely disputed" GDPR question**, per the skill I'm required to follow here: the processor/joint-controller/independent-controller dispute exists because most affiliate architectures _do_ involve data flowing through a third party — a network's tracking pixel, a co-branded landing page, shared lead files. Your first-party-only architecture removes the fact pattern the dispute is about. For reference, the three readings you'd need if that architecture ever changes:

| Position               | Who takes it                                  | Would apply to you if...                                                                                   |
| ---------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Processor              | SaaS tracking-vendor pattern                  | You started routing personal data through affiliate-controlled pixels/tech                                 |
| Joint controller       | One major affiliate network's public position | You and an affiliate jointly decided a shared tracking/data pool (co-branded funnels)                      |
| Independent controller | Another major network's public position       | Affiliate collects any data on its own site for its own purposes (this residual case applies to you today) |

`[LEGAL REVIEW]` — this is one of the field's three genuinely contested areas; the recommendation above is the drafting team's position for counsel to ratify, not settled law. Confirm before the terms go out, and re-open it immediately if the tracking architecture ever changes (e.g., you start sharing conversion/lead data with affiliates, or an affiliate network gets added later).

**Adjacent flag, not answered in depth here:** your NL/DE/FR affiliates are EU business users, which puts the EU Platform-to-Business Regulation's amendment/termination notice rules in scope for an in-house program too — that's a separate `[LEGAL REVIEW]` question from the GDPR role question and isn't resolved by the first-party-tracking fact above. Flag it for counsel separately when you draft Amendment/Termination.

## Data Protection clause (Section 9 of the terms)

```
9. Data Protection

9.1 Roles. Company is a data controller for personal data processed in
connection with the Program, including all data collected through the
Company Tracking Script on Company's own domains and applications.
[LEGAL REVIEW: GDPR role allocation for the affiliate is genuinely
disputed across the industry — processor vs. joint controller vs.
independent controller. The position below is the program's intended
position, not a settled legal conclusion; confirm with counsel before
this clause is finalized.]

Based on the Program's architecture — attribution and conversion
tracking performed exclusively by the Company Tracking Script on
Company's own domain, with no personal data transmitted by Company to
Affiliate and none transmitted by Affiliate to Company beyond
Affiliate's own account and payment details — Affiliate does not
process personal data on Company's behalf or under Company's
instructions within the meaning of Article 4(8) GDPR, and is not a
data processor to Company under this Agreement. To the extent
Affiliate processes any personal data on its own website or other
properties (for example, its own visitor or server logs), it does so
as an independent controller, for its own purposes, and not on
Company's behalf.

9.2 Change of data flows. If the parties' data flows change such that
Company discloses personal data to Affiliate, or Affiliate processes
personal data on Company's behalf — including if Company begins
sharing lead or conversion records with Affiliate, or if a network or
third-party tracking technology is added to the funnel — the parties
will execute Company's then-current Data Processing Agreement before
such processing begins, and the role allocation in Clause 9.1 will be
reassessed. [LEGAL REVIEW]

9.3 Affiliate's own compliance obligations. Affiliate will comply with
all applicable data protection and e-privacy law with respect to any
personal data it processes on its own properties in connection with
the Program, including obtaining any consent required before placing
tracking technology or cookies on its own site. Affiliate will not
attempt to de-anonymize, enrich, or cross-reference any Affiliate Link
identifier with independently held personal data to re-identify
Company's prospects or customers.

9.4 No scraping or harvesting. Affiliate will not collect, scrape, or
otherwise obtain personal data belonging to Company's prospects or
customers from the Company platform, and will not use any
Program-related data for any purpose other than administering its own
participation in the Program.

9.5 International transfers. Because no personal data is transmitted
between the parties under the roles described in Clause 9.1, no
cross-border transfer mechanism (e.g., Standard Contractual Clauses)
is currently required for the Company-Affiliate relationship itself.
Company's own processing of personal data collected via the Company
Tracking Script is governed by Company's Privacy Policy and, where
applicable, Company's Data Processing Agreements with its own
sub-processors. [LEGAL REVIEW: reconfirm if a US-based affiliate
relationship or vendor is later added to the tracking chain.]
```

## One thing worth flagging to your DPO now, not later

Cookie consent is independent of the role question above: EU ePrivacy/GDPR rules require consent before you set the tracking cookie your first-party script uses to attribute conversions — "first-party" is a data-protection-role argument, not a consent exemption. If that consent flow isn't already wired in for NL/DE/FR visitors, that's a bigger near-term exposure than the processor question was.
