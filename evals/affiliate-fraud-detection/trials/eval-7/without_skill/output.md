## Verdict: Green-light the matching logic. Don't green-light the timeline or the fingerprinting piece as scoped.

### What's solid

- **Email/phone cross-reference between affiliate accounts and customer accounts** — standard, effective, catches most real self-referral rings (same person referring themselves, family members sharing an email pattern, disposable-email clusters).
- **Billing name/address overlap** with affiliate identity — good corroborating signal.
- Combine these into a **score, not a binary flag**. Self-referral fraud is rarely provable from one signal alone.

### What's weak or risky as described

- **Billing address vs. click IP** — noisy. VPNs, mobile networks, shared family Wi-Fi, and people simply ordering to a different address than they browse from will produce false positives. Treat as a weak signal, never a standalone trigger.
- **Device fingerprinting** — this is the part to slow down on, not speed up.
  - Under GDPR/ePrivacy (CNIL guidance since 2020), device fingerprinting is treated like a cookie: it generally requires **consent**, not just "legitimate interest." A narrow fraud-prevention exemption exists but is fact-specific and needs a documented justification — not something to wing in three weeks.
  - IP addresses and fingerprints are personal data. Cross-referencing them with billing/identity data to auto-suspend commissions is processing that a regulator or a disputing affiliate can challenge.
  - **This needs a DPIA (or at minimum a documented legal-basis assessment) before it goes live**, not after.

### Why three weeks is the wrong number

Three weeks is plausible for a scoring script. It is not enough for:
- False-positive review workflow and an appeal path for flagged affiliates.
- Legal basis / DPIA sign-off on the fingerprinting piece.
- Deciding what a "flag" actually does — auto-clawback, payout hold, or human review. Auto-clawback on a heuristic score is how you end up in a commercial dispute with an affiliate over wrongfully withheld earnings.
- Audit trail (why was this account flagged) — you'll need this the first time someone contests it.

### Recommended path

1. **Week 1–3**: build and ship the email/phone/billing cross-reference matcher as a scoring signal feeding a manual review queue. No auto-clawback yet.
2. **In parallel**: get 30 minutes with counsel (or your DPO if you have one) specifically on the fingerprinting + IP-matching piece. Don't build it until that's answered.
3. **Only after the matcher has run a few weeks and you've tuned false-positive rate**: consider wiring flags to automated payout holds (not permanent clawback) with a stated appeal process.
4. Skip device fingerprinting for v1 entirely — it adds marginal detection lift over what email/phone/billing overlap already catches, at disproportionate legal cost. Revisit only if the simpler signals prove insufficient.

**Bottom line**: the engineer's instinct on data matching is right and cheap to ship safely. His instinct on fingerprinting + a 3-week live deadline is the part that turns a fraud-prevention project into a legal-exposure project. Decouple the two.