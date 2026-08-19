# Why "100% caught" isn't a claim you can make — and what to tell your VP instead

## The claim itself is the first problem

A catch rate only means something paired with its false-positive rate. Every credible source in this space — published fraud-ops checklists, the academic literature — reports the two together; none reports catch rate alone. A rule set can trivially hit 100% catch by flagging everyone; the cost shows up entirely in the false-positive number. Promising your VP "100%" with no denominator attached is a number you cannot defend the first time someone asks "100% of what, measured how?"

There's also a harder ceiling: you can only ever measure catch rate against fraud you know about. Anything your rules and your manual review both miss is invisible to the metric by construction. No fraud-detection system — yours or a vendor's — gets to claim 100%, because "0 misses" and "misses I haven't found yet" are indistinguishable from inside the system. The honest framing for your VP is "here's our catch rate against everything we can verify," not "we catch everything."

## The real gap: you have no denominator at all yet

Normally you'd validate a rule set by backtesting against confirmed incidents — did the rules fire on the fraud you already know happened. You don't have that. That's not a reason to skip validation; it's a reason to say explicitly, in whatever you hand your VP, that there is no incident history to backtest against yet, and to build the validation plan around that gap rather than papering over it. Faking a backtest against zero incidents, or asserting a catch rate with nothing behind it, would be worse than saying "we don't know yet, here's how we'll know."

## What "proof" looks like with zero incident history

Four things, in the order to actually do them — none of them requires a confirmed incident to exist:

**1. Manual review of a sample — build your own ground truth.**
Pull a random sample of both flagged and unflagged partners (start with what you can review by hand; a formal 2-SD/scoring approach isn't worth building until your roster and flag volume justify it). Have someone review each one manually and label it fraud / not fraud using the evidence a dossier would need — cookie-drop reproduction, redirect-chain capture, CRM outcome data, referrer mismatches. This sample *is* your denominator. It's what lets you say "of everything we looked at, the rules caught X% and false-flagged Y%" instead of quoting a number with nothing under it.

**2. Prove each rule fires on the pattern it claims to catch — technical reproduction, not statistics.**
For every rule, deliberately reproduce the fraud pattern it targets and confirm the rule trips: visit the suspect property from a clean browser and check whether a cookie drops without a click; submit a test lead with the exact disposable-email / sub-3-second form-fill signature a rule targets and confirm it flags. This is a functional test of the rule logic itself, independent of whether real fraud has ever occurred — it tells you the rule works as designed, which is a different (and answerable) question from "how much real fraud is out there."

**3. Cross-check structurally, not just statistically.**
Compare what a click claims about itself (declared source, UA, geo) against an independently observed layer — server-side postbacks vs. client pixels, your CRM/order ledger vs. the platform's reported conversions. Mismatches here are a source of confirmed findings that don't depend on a prior "incident" ever having been logged as one.

**4. Set the real checkpoint now, don't leave it open-ended.**
Schedule the catch-rate / false-positive-rate check as a standing gate at your first quarterly review, run against the sampled flags you'll have accumulated by then. That's the point where you'll have an actual number to report — not today.

## Give your VP the pair, and the honest baseline

Report, from that sampled review, not from a headline figure:
- Flagged rate
- Confirmed-fraud rate (from the manual sample — this is your proxy ground truth until real incidents accumulate)
- False-positive rate from that same sample
- Reversed-commission share and recovered spend, in dollars

Calibration anchors, if she wants a number to compare against — labeled as anchors, not targets you're promising: published fraud-ops checklists converge around an 80%+ catch rate paired with a false-positive rate in the low single digits; the strongest published academic result for a comparable rule (a two-feature timing classifier) hit 93.3% accuracy with a 1.5% false-positive rate. Neither is an industry constant and neither is 100%.

## The point that reframes the whole conversation

Detection accuracy isn't the only thing protecting Northgate's money, and it's worth saying so explicitly — it's what makes "we can't prove 100%" a non-issue rather than a gap. A 30–90 day commission hold window, if you have one configured, is doing structural work independent of whether any individual rule fires correctly: the strongest independent evidence on this (Edelman & Brandi, *JMR* 2015) found that delaying affiliate payment two to four months eliminated over 70% of fraud without hurting profit — before any detection rule does anything. If that window isn't set yet, it's the single highest-leverage thing to fix before the rule set's accuracy matters much at all. Tell your VP: the hold window is the backstop, the rule set is what names who to act on and builds the evidence, and "100% detection" was never the right bar for either one — a defensible, honestly-measured catch rate paired with a low false-positive rate, backed by a hold window that limits the damage of whatever the rules miss, is what "good" actually looks like.