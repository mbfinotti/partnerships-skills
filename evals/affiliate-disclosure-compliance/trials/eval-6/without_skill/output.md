This is a compliance program in name only, and the gap between what it does and what an FTC investigation would actually check is wide enough to drive an enforcement action through. Here's where it breaks.

## 1. "#ad" text-scanning doesn't work on video/audio, which is 100% of your program

Your own framing: the overwhelming majority of content is YouTube reviews and podcast ad reads, where disclosure is spoken or shown on screen. A crawler that greps for the string "#ad":

- **Cannot read audio.** A podcast host saying "this episode is sponsored by Crestpine" produces no text your crawler will ever see unless someone transcribes it. Most podcast platforms don't expose transcripts to crawlers, and even where they do, disclosure language varies infinitely ("this segment brought to you by," "my friends at Crestpine hooked me up," "use code X") — you can't regex your way to "was this adequately and clearly disclosed."
- **Cannot read on-screen text in video.** A lower-third graphic that says "Ad" for 3 seconds during a 20-minute review is invisible to a description-field scanner. You'd need frame-by-frame OCR or manual spot-checks, not a hashtag grep.
- **YouTube descriptions are the one place "#ad" might live** — but the FTC has been explicit for years that a hashtag buried in a description below the fold, or requiring a "show more" click, is **not adequate disclosure**. It has to be clear and conspicuous *in the ad itself* — meaning in the video, spoken or on-screen, not just in metadata. So even a crawler that works perfectly is checking for something that doesn't satisfy the actual legal standard.

Net effect: your crawler will scan the one part of the content (description text) that matters least, miss the parts that matter most (spoken/on-screen disclosure), and give you a false sense of coverage. It will also generate false negatives constantly — flagging affiliates who *did* disclose on-screen or verbally but didn't also tag a hashtag — which burns your 6 hours/month on noise instead of signal.

## 2. Attestations don't create disclosure, they create a paper trail that you knew and did nothing

The FTC's actual test in enforcement (see the CSGO lotto case, Machinima, Teami, Sunday Riley, the 2023 Endorsement Guides update) is not "did the advertiser have a policy" — it's whether the **advertiser took reasonable steps to monitor and enforce** compliance. A signed quarterly attestation saying "I disclose properly" that is never checked against actual output is close to the textbook example of what doesn't satisfy that standard. If anything, it can make things worse for you: it's documentary proof you were told disclosure might be an issue, asked people to self-certify, and then did no verification — which reads as knowing indifference rather than good-faith diligence. A regulator or plaintiff's attorney will use the attestation file against you, not for you.

## 3. You're treating the network's "own disclosure terms and scan" as compliance coverage without knowing what it actually catches

You mentioned the network runs some kind of scan on their side, but you don't seem to know what it does or does not check. Before building anything, you need to answer:

- Does their scan cover video/audio content or just text like yours would?
- What's their actual flag rate and false-negative rate?
- Do they share results with you, or is it a black box you're trusting on faith?
- Critically: **the network's disclosure terms are a contract between you and the network, not a shield against FTC liability.** The FTC holds the advertiser (you) responsible for affiliate disclosure regardless of what the network's terms say or what the network scans for. If the network's scan misses something, that's still your exposure, not theirs, unless your contract with them specifically indemnifies you — and even then, the FTC doesn't care about your indemnification agreement, it cares whether *you* took reasonable steps.

## 4. No feedback loop, no escalation, no remediation

A crawler that "flags" something without a defined next step isn't a program, it's a log file. What happens when something is flagged — does anyone read the flags? Is there a threshold for warning vs. suspension vs. termination? Repeat offenders currently have zero consequence baked into this design because nothing downstream of "flag" exists. The FTC explicitly looks at whether you have a **cut-off mechanism for repeat violators** — without one, "we scan for it" is meaningless.

## 5. No sampling of actual video/audio content at all

Given the format mismatch in #1, you have zero mechanism — automated or manual — that actually looks at or listens to a single second of the content your affiliates produce. A program that never once samples the real medium being used isn't a diminished compliance program, it's not a compliance program for this business.

## 6. Quarterly cadence doesn't match content velocity

An affiliate can post daily. A non-compliant video posted on day one of a quarter sits live, earning commission and misleading consumers, for up to three months before the next attestation cycle even asks the question again — and attestation isn't detection anyway, see #2.

## What this actually needs (sized to your 6 hours/month, not a rebuild)

1. **Replace "does #ad appear" with a monthly random-sample manual review** — pull a random 10–15 videos/episodes across your 400 affiliates each month (not the same people every time), actually watch/listen to the first 30–60 seconds and skim for a disclosure. That's the one thing nothing in your current plan does. At ~2–3 min per sample, 15 samples is well under an hour.
2. **Keep the attestation, but make it a checklist, not a promise** — have affiliates confirm *specific, checkable* things ("I state 'this is a paid partnership' within the first 30 seconds of video content" / "I include verbal disclosure before any spoken ad read"), and cross-reference a subset of attestors against your sample review each quarter. Mismatch = escalation.
3. **Get the network's scan methodology in writing** — ask them directly what it covers, and don't assume it fills the video/audio gap. If it only checks text metadata, you have zero automated coverage where it counts and should say so plainly rather than relying on it.
4. **Define a three-strike escalation path now**, even if it's five bullet points: flag → warning + resource on compliant disclosure language → second flag = commission hold → third = termination. Without this, "flagging" is theater.
5. **Keep a record of what you reviewed and when** — this is the actual artifact that matters if you're ever investigated: evidence of an ongoing, reasonable monitoring effort, not a folder of unread signatures.

This is still doable in roughly the time budget you have — the fix isn't "review everything," it's "review a real random sample of the real medium, on a cadence shorter than a quarter, with actual consequences," instead of pattern-matching a hashtag that mostly doesn't exist in your content and collecting signatures nobody checks.