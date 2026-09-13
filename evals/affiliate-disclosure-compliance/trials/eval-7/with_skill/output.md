This is a compliance review against published regulator rules, not legal advice. Counsel owns the legal call; this review finds what counsel and regulators would find. Keep every `[COUNSEL]` marker below until counsel resolves it.

## Assumptions used (no live interview was run for this single-shot request)

I'm treating this as: **US audience** (nothing in the brief indicates UK/EU reach — `[COUNSEL: confirm audience geography; if any material UK/EU/DE/FR/IT viewership exists, this needs a second pass against CAP/CMA/UCPD overlays]`), **short-form video**, **TikTok**, **affiliate-commission-only relationship** (referral payout on funded accounts = a material connection regardless of structure), **B2C**, **already live** (2 days, 90k views, actively converting) → this is remediation, not pre-publication. Personal finance is a **regulated vertical**, which under this skill's own logic promotes the highest-value response regardless of effort — that shapes everything below.

`[COUNSEL: personal finance apps with funded-account referral payouts may carry disclosure or promotion obligations beyond FTC Part 255/465 — e.g. state money-transmission or consumer-finance rules. This skill covers FTC endorsement/testimonial law only; escalate the product-specific regulatory question separately.]`

---

## Asset review

**Asset**: TikTok short-form video, ~40 sec | Brandon Teele | affiliate-commission-only | US (assumed) | B2C | **live, 2 days, 90k views**

| Requirement                               | Verdict                                                                                                                                                                                                  | Evidence                                                                                                                                | Rule                                                                                                    | Fix                                                       |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Disclosure present                        | **FAIL**                                                                                                                                                                                                 | No label anywhere — not on-screen, not spoken, not in caption                                                                           | Referral commission on funded accounts is a material connection; the duty triggers regardless of format | Add disclosure per fix below                              |
| Wording unambiguous                       | **FAIL**                                                                                                                                                                                                 | N/A — nothing to evaluate, there is no wording                                                                                          | 16 CFR 255.0(f)                                                                                         | "#ad" / "paid partnership with [Yieldmark]"               |
| Placement and prominence                  | **FAIL**                                                                                                                                                                                                 | Nothing visible, nothing audible                                                                                                        | 16 CFR 255.0(f)                                                                                         | On-screen overlay + spoken line, start of video           |
| Per-format requirement (short-form video) | **FAIL**                                                                                                                                                                                                 | Disclosure must be in-video: on-screen _and_ spoken, before the endorsement. Caption-only would still fail this row even if present     | format-placement-rules: short-form video                                                                | Cannot be cured by a caption edit — see Remediation below |
| Truncation / portability                  | **FAIL**                                                                                                                                                                                                 | Caption ("finally an app that doesn't gatekeep") carries zero disclosure to begin with, so nothing survives a cut, embed, or screenshot | FTC "more"-cut guidance                                                                                 | Moot until in-video disclosure exists                     |
| Financial claim                           | `[COUNSEL: "doesn't gatekeep" implied against a funded-account financial product reads close to an approval/eligibility claim. Flag for substantiation review — separate from the disclosure question.]` | —                                                                                                                                       | FTC Section 5                                                                                           | Review before any re-publish                              |

**Verdict: FAIL — full-stack failure, not a single-layer miss.** There is no disclosure to fix in place; the asset needs to be replaced, not edited.

---

## Remediation — what actually cures this (do this, separately from the HR decision)

The default cheapest rung, editing the disclosure into the live asset, is **not available here**: the format rule (`format-placement-rules.md`) requires the disclosure to live _inside_ the video — on-screen and spoken — and a caption edit cannot manufacture that. Per this skill's own rule, that escalates the cure one rung:

1. **Today**: Take the original video down, or restrict it, so the fully undisclosed version stops earning impressions. It's currently the highest-exposure live violation you have — treat it first.
2. **This week**: If you want to preserve the reach, have Brandon (or Yieldmark, directly) re-publish a corrected version with an on-screen overlay ("AD — paid partnership with Yieldmark") appearing in the opening seconds, plus a spoken line ("this video is sponsored — I earn a commission if you sign up through my link"), before any product endorsement. Re-publish-and-remove-original and takedown are rated equal on value (both fully remove the non-compliant version from the audience); re-publish just keeps the earned reach, which is the only reason it's worth the extra hour.
3. Do **not** rely on caption edits, hashtags, or the bio as a substitute — all three are explicit fail patterns per `disclosure-wording.md`.

**Freezing commission and terminating Brandon do not, by themselves, cure any of this.** The video stays live, undisclosed, and converting regardless of what happens to his account. If you terminate without also pulling or fixing the video, "the undisclosed asset live[s] on; the exposure outlives the relationship" — you'll have removed the partner and kept the FTC-facing problem.

---

## On freezing his commission today

This is the exact case this skill flags by name: **"withholding without [a program-terms clause] is a contract dispute, not a remediation."** You've confirmed the T&Cs have nothing on withholding. That means freezing his commission today isn't a compliance action — it's you unilaterally not paying someone under a contract that doesn't currently permit it. That's a real business decision you're entitled to make, but:

`[COUNSEL: confirm whether freezing already-accrued commission absent a withholding clause exposes Yieldmark to a breach-of-contract or (depending on state) wage/commission-timing claim from Brandon. This is a contract-law question, not a disclosure-compliance one — outside what this review can clear.]`

Two separate things are true at once: the _content_ clearly fails FTC disclosure standards (good record for you), and _withholding pay over it today_ isn't yet backed by anything you can point to in the agreement he signed. If you want to act today, the defensible path is pairing the takedown request with a hold pending investigation you can articulate under the general terms (breach of platform guidelines, misrepresentation, etc. — whatever is actually in your current T&Cs), rather than framing it as a withholding-clause action that doesn't exist yet.

## On terminating this week

Fine as a business call, but pair it with the takedown/re-publish above — termination alone leaves the 90k-view undisclosed video exactly where it is.

---

## Draft T&C clause — commission withholding & termination for disclosure non-compliance

Scope note: drafting program-terms language is technically the sibling skill's job (`affiliate-program-terms`), not this content-review skill's — I'm giving you a working draft since you asked, but route it through that skill or counsel before it goes live in your T&Cs.

> **Disclosure Compliance; Withholding and Termination.**
> Partner's continued eligibility to earn and receive referral commissions under this Agreement is conditioned on Partner's compliance, for every piece of Content promoting the Company's products or services, with applicable advertising and endorsement disclosure laws, including the FTC's Endorsement Guides (16 CFR Part 255) and Guides on the Use of Testimonials (16 CFR Part 465), and any platform-specific disclosure requirements.
>
> If the Company reasonably determines that Content does not clearly and conspicuously disclose Partner's material connection to the Company, the Company may, at its discretion:
> (a) request that Partner correct or remove the non-compliant Content within a specified period;
> (b) withhold, place on hold, or suspend payment of any commission attributable to the non-compliant Content, or to Partner's account generally, until the Content is corrected or removed;
> (c) claw back commissions already paid that are directly attributable to the non-compliant Content; and
> (d) suspend or terminate Partner's participation in the program, with or without withholding under (b) or (c).
>
> These remedies are cumulative, not exclusive, and are independent of any other rights the Company has under this Agreement or applicable law. This clause applies prospectively from its effective date and does not itself authorize action on Content published, or commissions earned, before that date.

`[COUNSEL: the last sentence is deliberate — a clause added today shouldn't be represented as already having authorized withholding on Brandon's pre-existing commissions. If you want the new clause to reach his account, that's a retroactivity/consideration question counsel needs to sign off on, not something this draft can resolve.]`

---

## What this incident should change going forward

- **Monitoring**: personal finance is a regulated vertical — per this skill's own re-ranking rule, that promotes full-roster or pre-publication review above the usual risk-weighted spot-check default, at least until the roster's disclosure hygiene is proven out.
- **Getting the rules to partners**: ship Brandon's corrected line as the seed of an approved wording bank (`references/disclosure-wording.md` has ready-to-paste lines for video) so every partner gets the same phrasing instead of improvising.
- **Get the withholding clause finalized** before you need it again — today's gap is exactly what turned a clean compliance case into a mixed compliance/contract situation.
