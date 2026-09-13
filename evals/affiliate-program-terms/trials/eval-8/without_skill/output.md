## Straight answer for your DPO

**Affiliates are independent (separate) data controllers — not processors, not joint controllers.**

### Why

A processor relationship (Art. 28 GDPR) requires the third party to process personal data _on Kastellan's behalf, for Kastellan's purposes, under Kastellan's instructions_, with no purpose of its own. That's not what's happening here:

- Tracking runs on **Kastellan's own first-party script**, on kastellan's own domain. The affiliate places a plain referral link/banner on their own site — no script, pixel, or cookie of theirs touches the visitor before the click. All attribution (referral cookie, click, conversion event) is collected and processed by Kastellan, for Kastellan's own purpose, using Kastellan's own means.
- The affiliate decides, independently, **how to promote you** (channel, audience, content, their own site/list/ads). That's processing of _their own_ audience's data, for _their own_ purpose. Kastellan has no say in it.
- No party jointly decides purpose _and_ means of a shared processing operation (the CJEU's _Fashion ID_ test for joint controllership). Contrast this with an embedded third-party pixel/SDK on the affiliate's own site collecting data before any click — that _would_ push toward joint controllership. You don't have that here.

So: two controllers, each responsible for their own leg, disclosing data to each other at defined points rather than one instructing the other.

### The one thing that changes this

If, for commission-dispute purposes, Kastellan ever hands an affiliate **identifiable lead data** (name/email of the referred person, not just a count and a euro amount), that's a controller-to-controller **disclosure**, not a processing instruction — status stays the same — but it now triggers two extra obligations:

1. A lawful basis + transparency for that disclosure (legitimate interest, disclosed in your privacy notice).
2. For **US affiliates specifically**: this becomes a restricted international transfer (GDPR Ch. V). You need a transfer mechanism — Art. 46 SCCs, **Module 1 (controller-to-controller)** — because there's no EU adequacy decision covering an individual/small US affiliate unless they're self-certified under the EU-US Data Privacy Framework (rare for solo affiliates).

**Recommendation:** don't create that problem — report conversions to affiliates as aggregated counts/amounts only ("3 conversions, €450 owed"), never the underlying lead's name or email. Then no lead personal data ever crosses the Kastellan → affiliate boundary, no SCCs needed, and the whole question becomes moot for NL/DE/FR/US alike. The only personal data flowing _from_ the affiliate _to_ Kastellan is the affiliate's own onboarding/payment data (name, bank/PayPal, tax ID) — that's a normal vendor/payee relationship, Kastellan is sole controller of it, no GDPR novelty there.

One adjacent flag, not what was asked but the DPO will hit it next: the first-party attribution cookie is very likely **not "strictly necessary"** under the ePrivacy rules, so it needs cookie consent like any other marketing/analytics cookie — separate issue from controller/processor status, worth closing in the same pass.

---

## Data protection clause — drop into the affiliate terms

```
## Data Protection

1. Independent controllers. Each party processes personal data in connection
   with this Agreement as an independent data controller under Regulation
   (EU) 2016/679 ("GDPR"), not as a processor or joint controller of the
   other. Neither party acts on the other's instructions when processing
   personal data under this clause.

2. Scope of each party's processing.
   a. Kastellan processes referral tracking data (click ID, referral
      timestamp, attribution cookie, conversion event) collected via its
      own first-party tracking mechanism on its own domain, for the purpose
      of attributing signups to the correct Affiliate and calculating
      commission.
   b. Affiliate processes personal data of its own audience (e.g. site
      visitors, subscribers, contacts) in the course of promoting
      Kastellan's services, using means and channels Affiliate alone
      determines. Kastellan has no visibility into, and gives no
      instruction regarding, this processing.

3. Data shared between the parties. Kastellan will share with Affiliate
   only aggregated conversion and commission data (counts and amounts).
   Kastellan will not share personal data identifying an individual
   referred lead or customer unless required to resolve a specific
   commission dispute, in which case only the minimum data necessary is
   shared, on Kastellan's legitimate interest basis (Art. 6(1)(f) GDPR),
   and Affiliate agrees to use it solely to resolve that dispute and to
   delete it once resolved.

4. International transfer. Where personal data is shared under Section 3
   with an Affiliate located outside the EEA, the parties agree such
   transfer is governed by the EU Standard Contractual Clauses (Controller
   to Controller, Module One, Commission Implementing Decision (EU)
   2021/914), incorporated by reference and attached as Annex [X].

5. Affiliate's own compliance. Affiliate is solely responsible for its own
   GDPR compliance regarding the personal data it processes to promote
   Kastellan's services, including lawful basis, its own privacy notice,
   and any cookie/tracking consent required on its own properties.
   Affiliate must not use tracking mechanisms (cookies, pixels, SDKs) that
   collect Kastellan visitor or customer data outside Kastellan's own
   first-party tracking without Kastellan's prior written consent — doing
   so may change the parties' respective data protection roles and
   requires a separate agreement.

6. Security and breach notice. Each party maintains appropriate technical
   and organizational measures for the personal data it controls. Each
   party notifies the other without undue delay upon becoming aware of a
   personal data breach that is reasonably likely to affect data
   originating from or shared under this Agreement.
```

Have your DPO confirm two things before this goes out: (a) that the commission-dispute path really only fires rarely and stays aggregate by default (point 3), and (b) get the Module 1 SCCs annex actually drafted/attached rather than just referenced, or a US affiliate agreement is unenforceable on the transfer point if challenged.
