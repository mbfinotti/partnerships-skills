# Two things to flag before the deliverables

**Both jobs are genuinely one-shot here** — the skills these tasks route to require an interactive interview (one question per message) before drafting. Since you asked for the complete deliverable in this response, I've made explicit, labeled assumptions instead of interviewing, and flagged every place a wrong assumption changes the output. Confirm the flagged items and I'll revise.

**A routing conflict I found and resolved:** `affiliate-program-terms` explicitly refuses consumer refer-a-friend terms requests ("do not accept a consumer refer-a-friend terms request routed back here") and points to `referral-abuse-guardrails` instead. But `referral-abuse-guardrails` itself, in its own workflow, says to route clause drafting _back_ to `affiliate-program-terms`. That's a dead loop. Since one side explicitly refuses the job, I drafted the actual customer-facing terms language myself, inside the guardrail deliverable, rather than bouncing you between skills.

---

# JOB 1 — Refer-a-Friend Program: Guardrail Spec + Terms

> **This is a draft for review by qualified counsel, not legal advice. Program terms are legally binding once published.**

## Assumptions (confirm these — they change the design)

| #   | Assumption                                                                                                                           | Why it matters if wrong                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A1  | "Friend subscribes" = friend converts to a **paid** plan (not just starts a free trial or creates a workspace).                      | If "subscribes" can be satisfied by an email-only signup or free tier, the throwaway-email abuse you're seeing is structural, not a detection gap — the fix is moving the trigger, not just blocking bad emails. **This is almost certainly the actual root cause of what you're describing** — throwaway emails alone can't fake a paid conversion, so if fraud is happening on email alone, the qualifying event is likely lighter than "paid subscription" today. |
| A2  | Refund/cancellation window on Torvel's plans is **30 days**.                                                                         | Sets the reward hold length directly.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| A3  | "Existing customer" = an individual user account, not a company-wide entity; referrals are person-to-person, not company-to-company. | If referrals are actually company-to-company (a Torvel customer referring another business), add the B2B domain-overlap and pipeline-check controls below as mandatory, not optional.                                                                                                                                                                                                                                                                                |
| A4  | No professional/paid affiliate tier exists alongside this consumer program.                                                          | If one does, its terms are a separate document (`affiliate-program-terms` territory) — don't merge the two.                                                                                                                                                                                                                                                                                                                                                          |

## Root cause, stated plainly

Bare-signup or trial-only qualifying events are the single most common reason a $20-class program gets farmed with disposable emails — the event costs the abuser nothing. Fix the event before investing in detection; detection on top of a free event is a losing game.

- **If A1 is true** (credit only fires on paid conversion): the throwaway-email problem is a **verification gap**, not an event problem — the fix is the two cheap gates below (§Verification), which stop it directly.
- **If A1 is false**: escalate immediately — move the trigger to the referred account's **second paid invoice**, which survives sign-up-and-vanish and one-cycle refund farming. Nothing else in this spec fully holds until that's true.

## Guardrail Spec

```
REFERRAL GUARDRAIL SPEC — Torvel refer-a-friend, 2026-09
Qualifying event : Credit fires on the referred account's SECOND paid invoice
                   (survives the refund window and single-cycle cancellation).
                   [LEGAL REVIEW: confirm this doesn't conflict with any existing
                   marketing claim of "credit when they subscribe" already live]

Caps             : 25 rewards / referrer / calendar year ($500/year) — deliberately
                   kept under the $600 US 1099 reporting threshold (rising to $2,000
                   for tax year 2026) to avoid issuer reporting obligations at this
                   reward size [as of drafting — re-verify the current threshold].
                   Program ceiling: set a monthly currency cap across all referrers
                   so a single viral/leaked-code event is bounded, not unbounded.

Velocity         : Flag >5 successful referrals / referrer / 7 days [illustrative —
                   replace with p95–p99 of your own legitimate-referrer distribution
                   once you have 60+ days of data]. Cooldown on first breach, not a ban.

Hold policy      : 35 days = 30-day refund/cancellation window + 5 days processing
                   [LEGAL REVIEW: confirm against actual refund policy — if it's not
                   30 days, this number is wrong]. Show credit as "pending — releases
                   <date>" from day one; never a silent gap.

Eligibility      : - New-customer test beyond email match: no prior account on the
                     same payment instrument or billing email domain.
                   - Referrer's own household/second account excluded.
                   - A referee who was referred by anyone else in the prior 12 months
                     is ineligible — kills ring re-farming of the same lead without
                     touching genuine one-off referrals.
                   - No stacking with other active discounts/promo codes.

Verification     : - Email double opt-in on the referee's signup — confirm the inbox
                     is real before it counts toward anything.
                   - Disposable/temporary-domain blocking (mailinator.com, temp-mail
                     variants, etc.) at signup. This is the direct fix for the
                     throwaway-email pattern you're already seeing.
                   - Payment instrument arrives for free with the paid-conversion
                     qualifying event (A1) — no separate phone/SMS or KYC gate is
                     justified at $20 of exposure.
                   - [If A3 is false — referrals are company-to-company]: add a
                     domain-overlap check between referrer's and referee's billing
                     domain/admin contacts; a work-email check alone is weak against
                     a shell account with a real domain.

Monitoring       : Payment-instrument reuse (tier-1, deterministic, already in your
                   billing data) + referred-vs-organic cohort dashboard (retention,
                   refund rate, 90-day revenue), reviewed by referrer decile. If the
                   referred cohort doesn't beat organic on those three, you're buying
                   signups, not customers — that's a reward-design problem, not a
                   guardrail problem.

Enforcement      : 1. Withhold pre-payout, with a specific reason string
                      ("referred accounts must be new customers on a new payment
                      instrument; this one matched an existing account").
                   2. Pause the referral link/cooldown — reversible, for the
                      aggressive-bargain-hunter case.
                   3. Remove from the program after 2 confirmed violations.
                   4. Claw back a paid credit only for confirmed self-referral.
                      [LEGAL REVIEW: blanket forfeiture on termination is legally
                      contested — keep clawback narrow to fraud, never blanket]
                   Appeal channel published in every denial message; human-reviewed;
                   14-day response SLA [self-set default, not a regulatory standard].

Terms status     : Every rule above must be published BEFORE it's enforced against
                   any referral — see draft terms below. Publish first; grandfather
                   already-earned, already-paid credits regardless of what's found
                   later. [LEGAL REVIEW: unilateral amendment / notice mechanism —
                   UK promotional rules require withholding grounds to be set out in
                   advance; retroactive tightening is the named failure mode]
```

## Customer-facing Terms — draft text

_(Publish this as the "Refer-a-Friend Terms" page linked from the referral dashboard and at signup.)_

**1. How it works.** Torvel customers ("Referrers") in good standing may share a personal referral link. When a new customer ("Referee") signs up using that link and remains on a paid Torvel plan through their second billing cycle, the Referrer receives a $20 account credit.

**2. Eligibility.** The Referee must be a genuine new customer: no prior Torvel account associated with the same email domain, billing details, or payment instrument. Torvel may deny or delay a credit where these conditions are not met, with a stated reason (see §6).

**3. Limits.** Each Referrer may earn up to 25 credits ($500) per calendar year. Torvel may adjust program-wide monthly limits at its discretion; changes take effect on the date published and do not affect credits already earned. `[LEGAL REVIEW: "sole discretion" framing — US regulators treat reliance on fine print to deny an already-earned reward as a deception risk; keep denial grounds tied to the stated eligibility rule, not open discretion]`

**4. Timing.** Credits are issued after the Referee's second paid invoice, held for 30 days from issuance, and displayed as pending during that period.

**5. Prohibited conduct.** Referring yourself or an account you control, using a false or disposable email address, purchasing or exchanging referral links outside your personal network, and posting your referral link to public coupon or deal sites are all violations of these terms and may result in withheld or reversed credits and removal from the program.

**6. Enforcement.** Torvel will state the specific rule violated when withholding or reversing a credit and will provide an appeal channel with a response within 14 days. `[LEGAL REVIEW: confirm this doesn't conflict with any existing customer terms of service appeal process]`

**7. Changes to these terms.** Torvel may update these terms at any time; changes apply to referrals made after the effective date. Credits already earned under prior terms are honored. `[LEGAL REVIEW: notice mechanism / effective-date practice — treat any EU/UK business-customer exposure as a question for counsel rather than assumed out of scope]`

**8. Tax.** Referral credits may constitute taxable income to the Referrer under applicable law; Torvel may issue tax reporting where required. `[LEGAL REVIEW: confirm 1099/US reporting posture at the chosen annual cap]`

**9. Data.** By submitting a Referee's email address, the Referrer confirms they have the Referee's permission to share it. Torvel processes this data to administer the program. `[LEGAL REVIEW: lawful basis / controller role under UK GDPR given UK customers are in scope]`

**10. Governing law.** `[LEGAL REVIEW: pick a governing jurisdiction — Torvel operates in both the US and UK]`

---

# JOB 2 — TikTok #ad-behind-the-fold: Compliance Review

> **This is a compliance review against published regulator rules, not legal advice. Counsel owns the legal call; this review finds what counsel and regulators would find.**

**Asset:** TikTok short-form video · Paid affiliate relationship · Posted yesterday (live) · Audience: US + UK (Torvel, B2B SaaS)

## Six-Layer Check

| Layer                       | Verdict        | Evidence                                                                                                                                                                                                                                                                                                | Rule                                                                                             |
| --------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| 1. Presence                 | Pass           | A disclosure (#ad) exists in the caption.                                                                                                                                                                                                                                                               | —                                                                                                |
| 2. Wording                  | Pass (assumed) | "#ad" is an accepted label — _confirm it's literally "#ad" and not "#sp"/"#collab"/"#ambassador", which fail regardless of placement._                                                                                                                                                                  | CMA accepted list; ISBA/IMTB code                                                                |
| 3. Placement & prominence   | **Fail**       | Sits behind the "more" cut — not visible without a tap.                                                                                                                                                                                                                                                 | FTC 16 CFR 255.0(f) (visual: location); CMA: "should not have to scroll... for more information" |
| 4. Per-format requirement   | **Fail**       | Short-form video requires disclosure **in the video itself** — on-screen and spoken, before the endorsement — not caption/description alone. Not assessable from the artefact whether any on-screen or spoken disclosure exists in the video — **confirm this**, since it changes the remediation rung. | FTC Disclosures 101; CMA (beginning of videos)                                                   |
| 5. Truncation & portability | **Fail**       | This is the named textbook failure: a disclosure that dies behind a "more" cut, and doesn't survive a screenshot, embed, or cross-post.                                                                                                                                                                 | Common failure mode, both FTC and CMA                                                            |
| 6. Jurisdiction overlays    | **Fail (UK)**  | CMA is explicit: "your audience should not have to scroll or select the link for more information." Direct hit. CAP Code 2.1 ("obviously identifiable") also fails — CAP Code covers UK marketing communications generally, not only consumer-facing ones, so the B2B audience doesn't soften this.     | CMA; CAP Code 2.1                                                                                |

**Overall verdict: FAIL.** A single failing layer fails the asset — this one fails four.

`[COUNSEL: whether the FTC Guides apply directly to a B2B audience is by-analogy only — the Guides never say "consumer-only," but the clearest textual hook (16 CFR 255.0 Example 13) reaches B2B deception through Section 5, not through Part 255 itself. Doesn't change the finding; changes which statute counsel would cite.]`

## Remediation (live asset, still earning impressions)

Default cure for a caption problem is "edit in place." **That's not available here** — the rule this asset fails is a per-format placement rule that puts the disclosure _inside the video_, and TikTok doesn't allow editing a video's audio/visuals after publish (caption/cover only). A caption edit cannot cure a missing on-screen/spoken disclosure, so this escalates one rung:

1. **Right now (minutes):** Edit the live caption so "#ad" is the very first thing, before any text that triggers "more." This doesn't fully cure the format-placement failure but stops the truncation failure immediately while step 2 is prepared.
   - Rewrite: `Ad — [rest of caption]`
2. **Re-publish a corrected version, then remove the original** (the format's own rule requires this): re-cut or re-record with:
   - On-screen text overlay in the first 1–3 seconds: `AD — paid partnership with Torvel`
   - A spoken line at the very start: _"This video is sponsored by Torvel — they paid me to talk about their product."_
   - Caption still opening with "Ad" per step 1.
   - Take this route over a bare takedown — it's equal on undisclosed-exposure removed but preserves the earned reach, per the ladder's own efficiency ranking.
3. **Don't rely on TikTok's native paid-partnership label alone**, even if the creator also enables it — FTC and CMA both say platform tools are "no guarantee," and it can vanish on screenshots/embeds/cross-posts.
4. `[COUNSEL: pausing this affiliate's commission until fixed is a legitimate ladder rung, but only if your affiliate program terms already contain a withholding clause — confirm before invoking it as leverage.]`

## Going forward

- This is a **paid** relationship (stronger material connection than gifted product) — no ambiguity that disclosure was owed.
- Since this is video/ephemeral-format content, the standing fix is a **pre-publication gate** on this affiliate's video content rather than after-the-fact monitoring — TikTok/Reels/Stories are the FTC's own named case for why post-hoc catches this too late.
- Feed the two compliant lines above into your affiliate wording bank so this doesn't recur with other creators.
