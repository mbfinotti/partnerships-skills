Here's the compliance read on both assets, plus the newsletter question.

## Is there an FTC rule specific to email newsletters?

Yes, but it's not the rule you're expecting for the "in partnership" line — that part is governed by the same law as everything else you publish (the FTC Act §5 / Endorsement Guides, 16 CFR Part 255, plus the FTC's ".com Disclosures" guidance). There's no email-specific carve-out or relaxation for material-connection disclosures — "clear and conspicuous" applies the same way in an email as on a web page.

The rule that _is_ email-specific is the **CAN-SPAM Act**, enforced by the FTC, and it's a completely separate obligation from disclosure:

- **From/subject line must not be deceptive** — can't misrepresent sender identity or make the subject line misleading about content.
- **Must identify the message as an ad** if it's a commercial email (not required to say "AD" in the subject, but the body must make clear it's an advertisement).
- **Valid physical postal address** required in every commercial email.
- **Working opt-out mechanism**, honored within 10 business days, no fee, no extra personal info required.
- Penalties are per-email (~$53,088/email as of the last inflation adjustment), which is what makes it dangerous at 41k subscribers × weekly sends.

⚠️ Check your ESP footer includes a real postal address and one-click unsubscribe — this is unrelated to the "in partnership" issue below but is the actual "email-specific FTC rule" you asked about.

**UK complication**: FTC only covers US recipients. For your UK half, the US CAN-SPAM opt-out model doesn't apply — UK/EU email marketing runs on **PECR** (Privacy and Electronic Communications Regulations), which generally requires **prior opt-in consent**, not just an opt-out option, subject to a narrow "soft opt-in" exception for existing customers. If your 41k list was built US-style (opt-out, pre-checked boxes, purchased lists, etc.), your UK subscribers may not be validly consented under PECR regardless of what the sponsored block says. Separately, UK sponsorship disclosure itself is governed by the **CAP Code / ASA**, not the FTC — same "must be obvious before engagement" principle, but they favor explicit labels like "Ad" or "Advertisement Feature" over softer language.

## Asset 1 — Tent page banner

❌ **Not sufficient as currently placed.** A single grey disclosure banner above the intro, with the first affiliate buy button ~1,200 words later, fails the FTC's "clear and conspicuous" standard in practice, for one specific reason: **proximity to the claim, not just presence on the page**.

The FTC's .com Disclosures guidance and its enforcement pattern (see actions against Sunday Riley, Teami, and multiple influencer cases) treat a disclosure as inadequate if a reader can plausibly encounter the affiliate link/recommendation without having seen the disclosure first. On a "Top 9" listicle, that's a realistic scenario multiple ways:

- Reader arrives via Google search landing on a jump-link/anchor straight to "#3 Best 2-Person Tent," skipping the top banner entirely.
- Reader uses a "Jump to reviews" table of contents (common on listicles).
- Reader scrolls fast past 1,200 words of intro and simply doesn't register a banner they saw 30+ seconds and several screens earlier — the FTC's guidance explicitly discounts disclosures that are separated from the claim by "scrolling."

**Fix**: repeat a short disclosure (even one line: "This post contains affiliate links — we may earn a commission.") immediately above the product list, not just at the very top. Ideally also inline near each buy button or price block, since each one is a separate affiliate claim. Keep the top banner too — it doesn't hurt, it's just not sufficient alone.

## Asset 2 — Newsletter sponsored block

❌ **Two separate problems, not one.**

1. **Wording**: "in partnership" is on the FTC's list of ambiguous terms it has specifically flagged as likely _not_ understood by average consumers as meaning "this is a paid ad." The 2023 Endorsement Guides FAQ update calls out "partner," "ambassador," and similar relationship language as insufficient on their own — readers can read "partnership" as an editorial collaboration, not a paid placement. Use unambiguous terms: **"Sponsored," "Advertisement,"** or **"Paid partnership."**

2. **Placement**: putting the disclosure _underneath_ the sponsored block means readers who only skim the block itself (very common in email — most readers don't scroll to a small italic line below an image/CTA) see the pitch before, or without ever seeing, the disclosure. FTC guidance is explicit that disclosure must come **before or immediately adjacent to, and at least as prominent as**, the claim it modifies — not trailing below it in smaller/italic type, which also reads as intentionally de-emphasized (a pattern the FTC has treated as an aggravating factor, not a neutral styling choice).

**Fix**: move a clearly-worded label ("Sponsored" or "Advertisement") to sit directly above/inside the block, at a font size and style comparable to surrounding text — not smaller, not italic-only.

## Bottom line

Both assets currently rely on disclosure that's _technically present somewhere on the page/email_ but not _proximate and unambiguous_ at the point of the actual claim — which is the exact failure pattern the FTC has brought enforcement actions over. Neither is a "rewrite everything" fix: it's adding one clear line in the right spot on each.
