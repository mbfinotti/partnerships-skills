This is a compliance review against published regulator rules, not legal advice. Counsel owns the legal call; this review finds what counsel and regulators would find.

## Short answer to your question

**No — do not assume B2B exempts either program.** That assumption doesn't hold, for three separate reasons:

- **Germany is not ambiguous at all.** UWG §5a(4) protects consumers *and* "other market participants" — Germany's rule reaches B2B audiences on its own terms. Your German customer chunk gets zero benefit of the doubt here.
- **For the US, the Guides (16 CFR Part 255) never say "consumer-only."** The FTC's own Example 13 under §255.0 treats deception aimed at "potential clients, purchasers, investors, partners, or employees" as within Section 5's deception theory. Applying Part 255 to B2B is by-analogy, not textually certain — `[COUNSEL: definitive B2B-scope opinion for Part 255 application to Ledgerwise's programs]` — but "by analogy, well-supported" is very different from "doesn't apply."
- **The instrument that actually bites hardest here is Part 465 (the Reviews Rule)**, not the Guides — §255.2 aggregate-rating theory, §465.5 insider reviews, §465.7 suppression. Nothing in Part 465 carves out business buyers, and it draws direct civil penalties without a prior Notice, unlike Guides-only violations.

So: B2B changes *how* the case gets argued (Section 5 / by-analogy for the softer Guides provisions), not *whether* either program is in scope. Both programs have live problems below, independent of the B2B question.

No specific post, screenshot, or review URL was supplied, so this reviews the two program *patterns* as described. Checks that need a rendered asset are marked "not assessable" — get me one live LinkedIn post and one live G2/Capterra review page and I'll re-run the full six-layer check against the actual rendering.

---

## 1. Employee advocacy program (LinkedIn)

**Format**: static social post | **Platform**: LinkedIn | **Relationship**: employee/insider + program incentive ($200 voucher, monthly top-3) | **Jurisdictions**: US, Germany | **Audience**: B2B | **Status**: live, ongoing

| Requirement | Verdict | Evidence | Rule | Fix |
|---|---|---|---|---|
| Disclosure present | **FAIL** | Only signal described is the LinkedIn headline naming the employer | 16 CFR 255.5: listing the employer on a profile page is not enough — disclosure belongs in the post itself | Add an in-post opener (below) |
| Wording | **FAIL** (nothing to grade — see above) | No in-post language exists | disclosure-wording.md B2B bank | "I work at Ledgerwise" |
| Placement/prominence | **FAIL** | Headline/profile-only is the exact "likely missed" pattern | 16 CFR 255.0(f); Common Failure Modes: "Disclosure in bio or profile only" | Move into the post's visible text |
| Truncation/portability | **FAIL** | A profile field never travels with a reshare, screenshot, or feed preview | 16 CFR 255.0(f) cross-cutting factor | Same fix — put it in the post, not the profile |
| US overlay — employee duty scaling | **FAIL** | A monthly leaderboard with a cash-value prize is active encouragement, not a passive policy | §255.5: "an employer that actively encourages reviews becomes responsible for monitoring them" | Stand up monitoring (below) |
| Germany overlay | **FAIL** | Employee receives a $200 voucher on top of employment — a second, independent material connection | UWG §5a(4); consideration from a third party is presumed, poster bears the burden of showing otherwise | Same in-post line covers it; `[COUNSEL: confirm no additional "Werbung"-style wording is needed given the voucher sits on top of employment — BGH's paid/unpaid distinction was drawn without a leaderboard prize in the fact pattern]` |

**Verdict: FAIL** — program-wide, since the pattern ("headline only") applies to everyone per your description.

**Rewritten opener** (paste-ready, B2B variant per disclosure-wording.md):
> "I work at Ledgerwise. [rest of post]"

If you want the incentive itself named too (belt-and-suspenders, not strictly required since employment alone triggers §255.5): *"I work at Ledgerwise, and I'm posting as part of our team's advocacy program."*

**Remediation** (live, compounding — this isn't a one-off):
- Default rung: **edit in place** for already-published posts — it's a caption-only fix, no video/audio element to re-record. Have staff add the opener line or a first comment; a comment counts only if it's the first thing seen, not buried under replies.
- Getting the rule to ~200 staff: default to the **wording bank** (adapt the line above, ship it in one message to the whole roster) rather than live training — a roster this size and this dispersed won't attend a session.
- Monitoring going forward: **risk-weighted spot-check**, weighted toward the monthly leaderboard's top 3 — they're your highest earners of the incentive and the highest-value check per the Ranked Choices logic. Full-roster review isn't warranted for static text posts; promote it only if the same person fails twice after the wording ships.

---

## 2. Incentivized review program ($50 gift card, ~180 reviews, 4.1→4.6 over 8 months)

**Format**: incentivized customer review | **Platform**: third-party software review sites (not named — treat generically) | **Relationship**: gift-for-review | **Jurisdictions**: US, Germany | **Audience**: B2B | **Status**: live, ongoing

| Requirement | Verdict | Evidence | Rule | Fix |
|---|---|---|---|---|
| Per-review incentive disclosure | **PASS** (per-review level) | Every reviewer ticked the platform's "I received an incentive" checkbox | 16 CFR 255.2 | None needed at this layer |
| Wording/rendering of that checkbox | **Not assessable** — no screenshot/URL supplied | — | disclosure-wording.md | Pull one live review page and confirm the rendered label reads unambiguously (not a vague icon-only badge) |
| Truncation/portability | **FAIL (likely)** | Star ratings and review quotes get reused off-platform in trust badges, the website, sales decks, one-pagers | Common Failure Modes: "Platform's native label relied on alone... labels can vanish in embeds and screenshots" | Any reproduction of a star rating or quoted review outside the platform must carry the incentive context too, not just the raw score |
| **Aggregate-rating disclosure** | **FAIL** | Displayed average moved 4.1 → 4.6 over 8 months while ~180 incentivized reviews were collected — a material, on-its-face inflation | 16 CFR 255.2 aggregate-rating trap: "even when every incentivized review discloses, the practice can still deceive if those reviews materially raise the displayed average" | Add a clear, conspicuous note next to the displayed score itself (not buried in an FAQ): e.g. "X of our reviews were submitted by customers who received a $50 gift card, which may affect this average." Do this on every surface the 4.6 figure appears — the review platform's own page if it allows it, and anywhere Ledgerwise repeats "4.6 stars" in marketing. |
| Germany overlay | **FAIL** | Same incentive, same UWG reach to "other market participants" | UWG §5a(4) | Same fixes apply without a B2B discount |
| Review suppression check | `[COUNSEL: confirm negative incentivized reviews weren't filtered or excluded from what's displayed]` | Not stated either way | 16 CFR 465.7 — direct civil-penalty exposure, no prior Notice required | If any incentivized reviewer's negative review was withheld or not published, that's a separate, more severe finding than the disclosure gap above |

**Verdict: FAIL** — driven by the aggregate-rating gap, which is the real exposure here and sits on the more dangerous side of the ledger: `us-ftc-standard.md` weights this under the Guides/Section-5 track today, but it converts into Part-465 territory (direct penalties, no Notice needed) the moment suppression or selective collection is added to the picture — hence the `[COUNSEL]` item above is the one thing worth resolving fastest.

**Remediation** (live, ongoing, single most consequential fix):
- This can't be cured with a caption edit — the violation lives in the *aggregate number*, not in any one review. Treat it as its own asset: add the disclosure adjacent to the score everywhere it's displayed, prioritized by where it's earning the most impressions right now (your own site's "4.6 stars" badge likely outranks the review platform's own page for this).
- Get the incentivized-vs-organic split and the correlation between incentive volume and the rating trend from each platform before finalizing wording — `[COUNSEL: quantify materiality precisely; 180 reviews and a 0.5-star, 8-month move is enough to flag now, but counsel will want the denominator]`.
- Ask each review platform directly how it handles the aggregate-disclosure requirement for incentivized programs — some do this natively (e.g., a "reviews collected via incentive program" filter/footnote). If none do, that gap is yours to fill, not theirs.

---

## What this doesn't cover

- No specific asset was reviewed line-by-line — this is a program-pattern review. Pull one live LinkedIn post and one live review-platform page and re-run this for a binding per-asset verdict.
- Program-terms language (making disclosure a contractual condition of the $200 voucher / $50 gift card) and partner-onboarding rollout of the wording bank are out of this skill's scope — see `affiliate-program-terms` and `affiliate-onboarding-sequence`.
- Only US and Germany were checked because those are the jurisdictions you named. If UK, France, or Italy carry material customer share, say so and I'll add those overlays — don't assume they transfer from the above.

**Repeat: this is a compliance review against published rules, not legal advice.** Keep every `[COUNSEL]` marker attached to its finding until counsel resolves it — don't let it drop off in a summary.