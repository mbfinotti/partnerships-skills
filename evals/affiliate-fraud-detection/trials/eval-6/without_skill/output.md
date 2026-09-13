This is a good instinct to push back on, because "we catch 100% of fraud" is a claim you cannot make and cannot prove — and saying it to your VP will hurt you later, not help you.

## Why "100% of fraud" is the wrong claim

- ⚠️ No confirmed incidents means no ground truth. Without labeled fraud/non-fraud cases, you cannot compute a true detection rate.
- 🎯 100% detection is also not a real goal for a rules-based system. Push false-positive tolerance to zero and you can trivially "catch everything" by flagging every affiliate — that's not a working control, it's a broken one.
- ❌ Absence of confirmed fraud historically could mean: no fraud happened, fraud happened and wasn't detected, or detection wasn't looked for. You cannot distinguish these without deliberately going and looking.

Reframe the message to your VP from "we catch 100%" to "here's how confident we are, and here's the evidence."

## What to tell your VP instead

**1. Coverage, not detection rate.** State what fraud patterns/typologies the ruleset covers (e.g., cookie stuffing, click flooding, incentivized traffic, self-referral, typosquatting, last-click hijacking) against a recognized taxonomy (IAB/TAG fraud categories, or your own risk register). Report this as "X of Y known typologies covered," not a percentage caught.

**2. Synthetic/adversarial testing.** Since there's no historical fraud, manufacture test cases:

- Write synthetic fraud scenarios per typology and confirm each rule fires on the ones it's meant to catch.
- Have someone (or a red-team exercise) try to construct traffic that evades every rule — this tells you where the gaps are, which is more useful than a "% caught" number.
- Backtest against your _legitimate_ historical traffic to measure the false-positive rate — this you _can_ measure with zero confirmed incidents, and it matters as much as detection.

**3. Benchmark against industry base rates.** Affiliate fraud incidence is well studied externally (industry reports cite ranges like 10-30% of affiliate traffic showing fraud signals in unmonitored programs). If your monitored traffic shows meaningfully lower flagged rates than industry base rates, or your flags concentrate in a few affiliates/patterns consistent with known fraud economics, that's evidence the rules are doing something real — not proof of 100%.

**4. Precision on what you do catch.** For every rule that fires, have a human review a sample and classify true positive vs. false positive. Report precision (e.g., "92% of flags upheld on manual review") — this is a real, defensible number, unlike a detection rate you can't compute.

**5. Leading + lagging indicators.** Track things you _can_ measure now (rule fire rates, flagged GMV, review turnaround, appeal/override rate) and commit to revisiting the false-negative question in 90 days once you have live data and — hopefully — your first confirmed cases to calibrate against.

## The actual message for your VP

> "We can't claim a detection rate with zero historical incidents to test against — that number would be fabricated either way. What we can show: coverage against N known fraud typologies, a synthetic test suite proving each rule fires as designed, a false-positive rate measured against real legitimate traffic, and precision on live flags reviewed by hand. We'll tighten the detection-rate estimate once we have real cases to calibrate against."

This is a stronger, more credible position than "100%" — it shows rigor, and it protects you the day a fraud case _does_ slip through despite the rules, because you never overclaimed.
