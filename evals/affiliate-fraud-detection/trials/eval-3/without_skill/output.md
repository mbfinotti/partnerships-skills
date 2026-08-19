# Lead-fraud detection rules for the CPL program

50% no-answer is not automatically fraud — cold CPL leads commonly run 30-50% no-answer even from honest partners. Rule #0 before anything else:

**Rule 0 — Baseline against the other 42 partners.**
Pull the network-wide no-answer rate by partner, last 90 days, weighted by volume. If the two June partners sit within ~1 std dev of the network median, this is a sales/dial-cadence problem, not a partner problem. If they're outliers (2+ std dev worse), proceed below.

```sql
-- ClickHouse/Postgres, using postback + sales disposition data
SELECT
  partner_id,
  count(*) AS leads,
  countIf(disposition = 'no_answer') / count(*) AS no_answer_rate,
  countIf(disposition = 'connected') / count(*) AS connect_rate
FROM leads
WHERE created_at >= now() - INTERVAL 90 DAY
GROUP BY partner_id
ORDER BY no_answer_rate DESC;
```

If the two partners are outliers, run these detection layers.

## 1. Phone/PII validity rules (catches fake or dead contact info)

- **R1 — Invalid/disconnected number.** HLR lookup or a carrier-validation API (Twilio Lookup, Numverify) at ingest time. Reject/hold if `line_type = disconnected` or `line_status = invalid`.
- **R2 — VOIP/burner on a program expecting consumer mobile.** Flag `line_type = voip` at a rate materially above the network baseline for that partner.
- **R3 — Number age.** If the API returns port/activation recency and the number was ported/activated <7 days before lead submission, flag — common in synthetic-identity or recycled-SIM fraud.
- **R4 — Disposable email + no-answer correlation.** Cross-tab: leads with disposable/free-tier email domains (mailinator, guerrillamail, etc.) vs no-answer rate. A partner where disposable-email leads have a much higher no-answer rate than real-domain leads is laundering data.

## 2. Duplicate / recycled-data rules (catches resold or scraped lead lists)

- **R5 — Cross-partner duplicate PII.** Same phone, email, or name+address appearing under a different partner_id in the last 180 days. This is the single strongest signal for lead-list recycling.
```sql
SELECT phone_hash, count(distinct partner_id) AS partners, count(*) AS occurrences
FROM leads
WHERE created_at >= now() - INTERVAL 180 DAY
GROUP BY phone_hash
HAVING partners > 1
ORDER BY occurrences DESC;
```
- **R6 — Fuzzy near-duplicates within one partner.** Levenshtein distance ≤2 on name, or same last-4-digits phone with different area code, or sequential email handles (`john123`, `john124`). Sign of a bot generating variants of one seed identity.
- **R7 — Address reuse.** Same street address with different names, above a threshold (e.g. >3 leads/address/90 days) not explainable by an apartment building or business address.

## 3. Behavioral/timing rules (catches bots and click farms)

- **R8 — Bot-speed form fill.** `time_to_submit` (page load → submit) under ~3-5 seconds, consistently, for a multi-field form. Humans don't fill 8 fields in 3 seconds.
- **R9 — Click-to-conversion latency anomaly.** Time between ad click and postback fire is unnaturally constant (e.g. always 12-15s) rather than the wide human distribution you see elsewhere — indicates a scripted funnel, not a real user journey.
- **R10 — Off-daypart clustering.** Genuine consumer form-fills follow a human daypart curve (peaks daytime/evening, local timezone). Plot hour-of-day histogram per partner; a partner with a flat distribution or a 2-5am local-time spike is farm/bot traffic.
```sql
SELECT partner_id, toHour(created_at, timezone) AS local_hour, count(*)
FROM leads
GROUP BY partner_id, local_hour
ORDER BY partner_id, local_hour;
-- Compare shape (not just volume) against your top 5 trusted partners.
```
- **R11 — IP/device concentration.** >N leads from the same IP, /24 subnet, or device fingerprint within a rolling 24h window. Set N relative to expected unique-visitor traffic for that partner's stated channel.
- **R12 — Geo mismatch.** IP geolocation country/region vs phone area code vs claimed address disagree beyond a tolerance you'd expect from VPN/mobile carrier noise (e.g. >15% of a partner's leads show 3-way mismatch).

## 4. Consent/compliance rule (also protects you legally)

- **R13 — Missing consent receipt.** Every lead must carry a consent timestamp, the exact disclosure text shown, and the capturing IP. If a partner can't produce this on request, that's independently a reason to suspend the postback relationship — TCPA exposure aside, absence of a real consent event correlates strongly with data being harvested elsewhere and passed through.

## 5. Tie enforcement to the 90-day hold (this is where you actually claw back money)

Don't let the hold be passive — turn it into an active verification pipeline:

1. **Day 0-3:** auto-validate phone (R1-R3), auto-check duplicates (R5-R7). Fail → immediate hold, no payout accrual starts.
2. **Day 3-14:** require sales to log ≥3 dial attempts with disposition codes before a lead can be marked "worked." No dispositions logged by day 14 → flag for manual audit, don't silently let it ride to day 90.
3. **Day 30:** compute per-partner connect rate on the cohort. Below-baseline partner → move to manual review queue, hold further postback auto-pay (don't auto-approve new leads from that partner while the audit runs).
4. **Day 90 (release decision):** only leads with disposition = `connected` (or better) convert from held to paid. `no_answer` / `invalid_number` / `wrong_person` after 3+ documented attempts are charged back automatically — require the partner to prove otherwise, not the reverse.

## 6. Investigation checklist for the two June partners specifically

1. Export their raw lead records: IP, device fingerprint, timestamp, consent metadata, phone.
2. Bulk phone validation (R1-R3) — get the % invalid/VOIP/recently-ported.
3. Run duplicate/fuzzy match (R5-R7) within their leads and against the other 42 partners.
4. Run timing forensics (R8-R9) and daypart histogram (R10).
5. Personally sample-call 20-30 "no answer" leads yourselves — not through the sales queue — to confirm the number even reaches a real person and that they recall opting in.
6. If ≥2 of the above rules trigger at high confidence: suspend auto-pay on new postbacks from these partners, move their entire held (90-day) cohort to manual review, and enforce chargeback on anything failing R13 (no valid consent receipt).

If the sample calls in step 5 reach real people who deny ever requesting contact, that's a TCPA problem, not just a CPL-quality problem — worth flagging to whoever owns compliance before deciding whether to keep the relationship at all.