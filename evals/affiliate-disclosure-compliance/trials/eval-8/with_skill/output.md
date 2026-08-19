This is a compliance review against published regulator rules, not legal advice. Counsel owns the legal call; this review finds what counsel and regulators would find.

Scope: both assets are reviewed from your text description only (no screenshot/URL/HTML supplied), so visual factors (grey banner's contrast, exact italic font size) are marked "not assessable" rather than guessed. Jurisdictions checked: US + UK only, since that's your stated audience — no EU/DE/FR/IT overlay applies.

---

## Asset 1 — "Top 9 Ultralight Tents 2026" page

**Format**: affiliate roundup/comparison page | **Relationship**: affiliate-commission | **Audience**: US + UK, B2C (assumed — flag if wrong) | **Status**: live | **Artefact**: text description only

| Requirement | Verdict | Evidence | Rule | Fix |
|---|---|---|---|---|
| Disclosure present | ✅ PASS | Grey banner at top of page | Material-connection duty | — |
| Wording unambiguous | ✅ PASS | "This page contains affiliate links" plainly names the commercial relationship | Matches the accepted blog-header pattern | — |
| Visual prominence (contrast/size) | ⚠️ NOT ASSESSABLE | "Grey banner" described, not rendered | 16 CFR 255.0(f) visual factors | Verify contrast ratio against background; grey-on-white risks reading as low-priority boilerplate |
| Per-format placement (roundup) | ❌ FAIL | Banner sits ~1,200 words above the 9 product/buy-button blocks | FTC: reader must see the disclosure and the affiliate link **at the same time**; CMA: no scrolling required | Add a short line adjacent to each of the 9 buy buttons, e.g. "(affiliate link — we may earn a commission)" |
| Truncation/portability | ✅ PASS / N/A | Static webpage, no caption-cut risk | — | If the page is ever syndicated/cached/AMP'd, confirm the banner survives |
| UK overlay (CAP 2.1 / CMA) | ❌ FAIL | Same separation issue applies under the "readers shouldn't have to scroll or hunt" standard | CAP Code 2.1; CMA guidance | Same fix as above covers both markets |

**Verdict: FAIL** — wording and top-of-page placement are fine on their own; the failure is that the *only* disclosure lives 1,200 words away from every link a reader could actually click. That's the exact "roundup disclosure separated from the links" failure mode FTC and CMA both call out by name.

**Fix (paste-ready, repeat under each of the 9 blocks):**
> Ad — we may earn a commission if you buy through this link.

Keep the top banner too; it doesn't hurt, it just isn't sufficient alone.

**Remediation** (page is live and still earning organic/search impressions, so this is the priority asset): **edit in place** — add the adjacent line to each block. Minutes of work, no republish or takedown needed, since the fix is additive text, not a structural rewrite.

---

## Asset 2 — Thursday newsletter sponsored block

**Format**: newsletter/email | **Relationship**: paid sponsorship (brand deal, not affiliate) | **Audience**: US + UK ~50/50, 41k subscribers, B2C (assumed) | **Status**: live (weekly recurring — treat as compounding, not one-off) | **Artefact**: text description only

**Direct answer to your question: no.** There is no FTC rule specific to email/newsletters. The Endorsement Guides don't have a newsletter-specific provision. What applies is the same general clear-and-conspicuous standard as everything else (16 CFR 255.0(f)), read as: disclose adjacent to the sponsored block, **before** the reader acts on it, visually separated from editorial content. The UK has no email-specific rule either — CAP Code 2.1's general "obviously identifiable as marketing" standard governs instead.

| Requirement | Verdict | Evidence | Rule | Fix |
|---|---|---|---|---|
| Disclosure present | ✅ PASS | "in partnership" line exists | Material-connection duty | — |
| Wording unambiguous | ❌ FAIL | "in partnership" reads like the rejected vague-"partner" pattern — it signals a relationship without saying *paid* or *ad* | Same family as "#collab"/"#ambassador"/vague "partner" (fails to state the commercial nature); not on CMA's accepted label list (ad/advert/advertising) | Replace with "Sponsored — [Brand] paid for this placement." |
| Placement/prominence | ❌ FAIL | Disclosure sits **under** the sponsored block, i.e. after it | General standard requires disclosure before the reader engages with the block, not after | Move the line to the top of the block |
| Visual weight (small italic) | ⚠️ NOT ASSESSABLE, flagged | Small italic risks blending with normal editorial italics rather than standing apart | 255.0(f): must be "difficult to miss" and not contradicted/diminished by surrounding style | Set in normal body weight/size, ideally boxed or shaded against the block |
| Truncation/portability | ⚠️ NOT ASSESSABLE | Not stated whether disclosure is inside the same visual container as the block, or a separate line that could be clipped/dropped on forward, screenshot, or Gmail's clipping of long HTML emails | General portability principle | Merge disclosure and block into one visual unit so they can't be separated |
| UK overlay (CAP 2.1 / CMA) | ❌ FAIL | "in partnership" isn't on CMA's accepted list and doesn't make the ad "obviously identifiable" | CAP Code 2.1; CMA guidance | Same fix as above covers both markets |

**Verdict: FAIL** on both wording and placement.

**Fix (paste-ready, placed at the top of the block, before any CTA):**
> Sponsored — [Brand] paid for this placement.

**Remediation — this needs two different moves, not one:**
- **The issue already sent**: you can't edit a delivered email. If your ESP/platform hosts a web/archive version of the issue, correct that copy (equivalent to "re-publish corrected"). Otherwise there's nothing to cure retroactively on that specific send — 16 CFR 255.1(d) frames remediation as preventing *recurrence*, not un-sending.
- **Going forward, every Thursday**: since this is a recurring weekly slot, treat it as a compounding problem, not a one-off. Bake the corrected line and top-of-block placement into your sponsored-block template now, before next Thursday's send, so it's not a manual catch each week.

`[COUNSEL: if prior weekly issues used the same "in partnership" wording, that's a recurring pattern across multiple sends to a 41k list — worth a scoping call on whether that history needs disclosure to anyone beyond fixing forward.]`

---

## Priority across both

1. **Tent page first** — it's evergreen and still earning impressions/clicks every day the fix is delayed.
2. **Newsletter template second** — fix before next Thursday's send; the current issue's exposure is already largely locked in.

## Wording bank for future use (adapt once, reuse)

- Roundup/affiliate blocks: **"Ad — we may earn a commission if you buy through this link."** (place next to every link/button, not just at the top of the page)
- Sponsored newsletter blocks: **"Sponsored — [Brand] paid for this placement."** (top of the block, before any CTA, visually separated from editorial)

Keep both `[COUNSEL]` markers above until someone with authority to make the call clears them.