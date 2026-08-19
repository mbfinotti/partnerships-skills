This is a compliance review against published regulator rules, not legal advice. Counsel owns the legal call; this review finds what counsel and regulators would find. Keep every `[COUNSEL]` marker below until counsel resolves it.

**Verdict: FAIL AS A MONITORING PROGRAM, with `[COUNSEL]` ITEMS.** Not because a crawler and an attestation are worthless — they're two legitimate rungs — but because together they cover almost none of the actual content, and the plan skips the one duty (searching what partners are actually saying) that neither rung discharges.

## Why the crawler doesn't do what you think it does

Per `format-placement-rules.md`, short-form and long-form video require disclosure **in the video** — on-screen and spoken — and explicitly say "description-only fails." Podcasts require an **audible** disclosure matching the ad read's own prominence (16 CFR 255.0(f)). Your stated majority — YouTube reviews and podcast ad reads with spoken/on-screen disclosure — is exactly the content a text scan for `#ad` cannot see, because there's no reliable text layer to scan (video descriptions and show notes are not the disclosure; the video/audio is).

Concretely, the crawler produces both kinds of wrong answer:

- **False passes**: a video description carries `#ad` (habit, or copy-pasted boilerplate) while the video itself never mentions or shows it. Per the six-layer check, that's still a FAIL — description-only never satisfies the per-format rule — but your crawler marks it clean.
- **False failures**: an affiliate does the disclosure correctly — spoken at the top of the video, verbal repeat mid-podcast — but never writes `#ad` in the text field. Your crawler flags a compliant creator as non-compliant, and literal-string matching also misses every other accepted label (`disclosure-wording.md` passes "Ad," "advertising," "sponsored by [brand]," "paid partnership with [brand]," "publicité" for a French audience) unless you also match those.
- **Even where it works**, presence of the right word is one of six gates (Presence, Wording, Placement/prominence, Per-format, Truncation/portability, Jurisdiction overlays). A single fail on any layer fails the asset — a `#ad` hit tells you nothing about placement, prominence, or whether it survived a cross-post or embed.

So the crawler, as scoped, is close to a scan of the wrong surface for the wrong majority of your content. That's not a tuning problem — it's deletable as a standalone control here: this skill's own default is to delete the automated label scan precisely when disclosures are spoken or on-screen, which is your stated case.

Where a scan *is* worth keeping: run it (cheaply, same tooling) against auto-generated YouTube transcripts and podcast show notes, searching for cue words ("sponsored," "paid," "ad," "partnership," brand name near "pays/paid") rather than the literal `#ad` string alone. That widens recall on the audio layer at near-zero marginal cost — but treat every hit as a lead for a human to verify placement and prominence, never as a pass/fail verdict on its own.

## Why the attestation isn't monitoring

"Never let self-attestation stand as the monitoring itself. A partner who misunderstood the rule attests in good faith and still fails; the FTC asks for a search of what partners are saying, not a collection of their promises." That's the exact failure mode here: a quarterly signature tells you what a partner believes, not what's on their channel. It satisfies none of the FTC's own four-step monitoring checklist beyond step 1 (guide) — it does nothing for step 3 (periodically search) or step 4 (act on what's found), and 16 CFR 255.1(d) frames monitoring and remediation as duties, not alternatives to each other.

Three specific holes in the attestation as designed:

1. **No wording is shipped with it.** An affiliate attesting "yes, I disclose" while tagging `#ambassador` or saying "thanks to Crestpine" is answering honestly and still failing — those are on the rejected list. Attaching your accepted-label bank to the attestation form (adapted from `disclosure-wording.md`, one line per format: video overlay, spoken read, podcast verbal repeat) is a same-effort addition with real value.
2. **Quarterly is slow relative to publishing cadence.** 400 affiliates posting continuously means months of undisclosed content can run between signatures with zero visibility.
3. **It's only enforceable if your program terms already back consequences for a false attestation** (commission hold, termination). `[COUNSEL: confirm the program terms carry a clause backing withholding or termination on a disclosure failure before this attestation has teeth — drafting that clause is affiliate-program-terms' job, not this skill's]`.

## The network doesn't cover this for you by default

Delegating to the network doesn't shift your liability — you remain responsible for what your affiliates do on your behalf, and the FTC's guidance says to require regular compliance reports from an intermediary, not assume silent coverage. Two things to actually verify rather than assume:

- What does the network's scan check — text only, or does it also touch video/audio? Given the same technical constraints above, "some kind of scan" run by a network is very likely also a text/label scan, meaning it has the identical blind spot on your majority content.
- Pull their compliance reports on a fixed cadence and read the network's own disclosure terms against `disclosure-wording.md` and `format-placement-rules.md` — a network standard built for a different vertical/format mix may not require in-video disclosure at all.

`[COUNSEL: if the network's terms conflict with or fall short of FTC/CAP standards for your audience's jurisdictions, confirm whether relying on them is defensible]`.

## What's entirely missing: a cure step

Nothing in the plan says what happens when a violation is actually found — by the network, a spot-check, or a partner's own admission. Curing is mandatory, not optional; per the remediation ladder, the default cheap move is a message asking for an edit-in-place, escalating only if the format's own rule puts the disclosure inside the content (a video with no spoken/on-screen disclosure can't be fixed by a caption edit — only a re-publish reaches it). A program that finds violations and has no defined next step is arguably worse for enforcement optics than no program: it shows you were aware and didn't act, which cuts against the good-faith reading of 255.1(d) rather than for it.

## Re-ranked plan for your actual constraints (solo, 6h/month, 400 affiliates, network already in place, spoken/on-screen majority)

Re-ranking rules from `SKILL.md` that apply directly: a centrally-enforcing network moves rungs up; a roster too large to review asset-by-asset moves sampling/automation up and full-roster down; disclosures that are spoken/on-screen delete the text-label scan as a standalone control.

1. **Risk-weighted spot check as the actual monitoring** (the thing the crawler and attestation together were supposed to be but aren't). Budget ~15–20 assets/month at ~20 min each inside your 6h — prioritize newest partners, top earners by commission, anyone previously flagged, and any gifted-only relationships (a free product is a material connection with the same disclosure duty, easy to forget it applies). This is the only rung that actually looks at placement, prominence, and the spoken/on-screen layer your content lives on.
2. **Self-attestation kept, but demoted to paper trail underneath the spot check**, not the program itself — bundled with the accepted-wording bank so a good-faith partner has the right lines in hand, and tied to a program-terms consequence if you have one `[COUNSEL]`.
3. **Text/transcript scan kept, but narrowed and demoted** to a cheap lead-generator (transcripts, show notes, landing pages, any blog/roundup content in the roster) feeding the spot check — never treated as a pass/fail signal on its own, and never claimed as coverage for video/audio.
4. **Network compliance reports pulled on a fixed cadence** (monthly or quarterly), with their scan methodology actually reviewed once against the format-placement table — don't inherit their definition of "compliant" untested.
5. **A predefined, tiny remediation ladder**: corrected-line DM first (minutes), escalate only per the format's own requirement, payment hold only if the terms already back it `[COUNSEL]`.

Track: first-pass rate (below 80% sustained = fix onboarding, not just assets), time-to-remediation (request the fix within 24h of a finding), and roster coverage (% of the 400 with at least one asset actually reviewed per period — an unreviewed partner is unmonitored risk under 255.1(d)).

## Open items before you ship this

- `[COUNSEL]` Jurisdictions: is the affiliate audience US-only, or does reach extend to UK/EU/France/Germany/Italy? That changes the wording bank and adds overlay rules (French "publicité," Italian Digital Chart, Germany's payment presumption) not covered by a `#ad` check at all.
- `[COUNSEL]` Any gifted-product-only or insider/employee affiliates in the 400? Those carry the same duty and, if any post reads as a "review," Part 465 (§465.5 insider reviews) carries direct civil-penalty exposure — higher severity than a Guides-only miss, and an attestation alone is a weak defense there.
- Confirm program terms actually back a withholding/termination consequence for attestation false statements — if not, that's `affiliate-program-terms`' job, not something to assume into place.