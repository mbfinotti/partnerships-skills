# Palo Verde Home — Affiliate Program: Prohibited Tactics Policy (Draft)

*Draft policy language for insertion into the master Affiliate Program Agreement / Program Policies addendum. Two carve-outs below correspond to the Slipstream cashback-extension relationship and the coupon-site network. Flag for outside counsel before publishing: the clickstream-data clauses touch unsettled CIPA/wiretap case law and CCPA "sale/share" analysis — this is policy drafting, not a legal opinion.*

---

## Section A — Cashback & Browser-Extension Partners

*(Applies to Slipstream and any future cashback/deal-extension partner. Written to let the relationship continue, not to end it — the point is to bound what data comes in and how commission gets earned.)*

**A.1 — Scope of tracking data accepted**
Company will ingest and retain, from any cashback/extension partner, only the following event types, tied to a specific, user-initiated interaction with the extension on Company's domain or checkout flow: (a) extension activation timestamp, (b) referring click ID, (c) cart contents and order value at time of purchase, (d) SKU-level order data. Company will not ingest, and the partner may not transmit, browsing activity, search queries, or page views occurring on any domain other than Company's own properties, nor any browsing history not directly tied to a completed or attempted Company purchase. "Full clickstream" feeds must be filtered to this scope before they reach Company; unfiltered feeds are to be rejected by the tracking vendor at ingestion, not sorted after the fact.

**A.2 — No passive or forced attribution**
The extension may fire a tracking/attribution event only when the shopper affirmatively opens or activates the extension during that session (e.g., clicks "apply savings" or equivalent). No attribution event may fire from background page loads, auto-injection at checkout, iframe/pixel activation without a corresponding user action, or activation on pages the shopper did not open. Company reserves the right to audit event logs against session recordings or server-side event data at any time on 5 business days' notice.

**A.3 — Attribution priority (anti-cannibalization)**
Where a shopper's session shows a qualifying click from a non-cashback channel (paid search, content affiliate, email, direct) within the applicable cookie window, that channel's click takes attribution priority over a cashback-extension activation that occurs later in the same session, unless the extension activation is the only qualifying click present. This prevents the extension from overwriting credit earned by whoever actually drove the purchase decision.

**A.4 — Consumer disclosure**
Partner must disclose, before or at the moment any offer/cashback amount is shown, that (a) use of the extension may generate a commission for the operator, and (b) purchase data will be shared with the retailer for attribution purposes. Disclosure must meet FTC Endorsement Guide standards and the data-use disclosures required by the extension's browser-store listing (Chrome Web Store User Data Policy or equivalent). Non-compliant disclosure is grounds for suspension pending fix.

**A.5 — Data handling, retention, and legal basis**
Partner represents that it has a valid legal basis (consent or applicable exemption) for any personal data shared with Company, and that sharing complies with CCPA/CPRA obligations applicable to a "third party" recipient, including honoring Global Privacy Control/opt-out-of-sale-or-share signals upstream of any data reaching Company. Company will not merge this data with data from unrelated retailers, will retain it only as long as needed for attribution, fraud review, and statutory recordkeeping, and will delete or de-identify it thereafter. A data processing addendum covering security, breach notice, and deletion-on-request must be executed before go-live and reviewed annually.

**A.6 — No unauthorized codes or coupon UI from the extension**
The extension may surface only codes that are live in Company's authorized-code feed (see Section B.2). It may not auto-generate, guess, or display a code Company did not issue, and may not represent that a discount was applied when none was.

**A.7 — Remedies**
A breach of A.1–A.6 that is not cured within 10 business days of written notice suspends commission accrual for affected traffic and, on a second occurrence within 12 months, terminates the partnership. Company may claw back commission on any order shown to have been attributed through a violation of A.2 or A.3.

---

## Section B — Coupon & Deal Site Network

*(Applies to all ~30 coupon/deal-site affiliates.)*

**B.1 — Authorized codes only**
Affiliate may publish only codes Company has explicitly issued to that affiliate, or codes distributed through Company's official live-code feed (see B.2). Publishing a code sourced from another retailer's page, a forum, a scrape, guesswork, or a code issued to a different affiliate is prohibited, regardless of whether the code happens to work.

**B.2 — Live-feed requirement, not manual listings**
Company (via its tracking vendor) will provide a machine-readable feed of currently valid codes with start/expiration timestamps. Affiliates must display codes by syncing to this feed — polling at least once every 24 hours — rather than hand-maintained listings. A code not present in the feed may not appear on the affiliate's site, cached page, browser notification, or app, including previously-valid codes left live past expiration.

**B.3 — No phantom or non-functional discounts**
Affiliate may not represent that a code grants a discount, free shipping, or other benefit it does not actually grant. A "reveal code" or "click to copy" interaction that fires a tracking click but applies no real discount at checkout is treated as a fake-code violation regardless of intent.

**B.4 — Expiration and accuracy hygiene**
Affiliate must remove or mark expired any code within 24 hours of the expiration timestamp in the feed. Indexed/cached pages showing dead codes (e.g., stale search-engine results) must be updated or noindexed by the affiliate; Company is not responsible for affiliate-side caching failures.

**B.5 — Audit and takedown**
Company may audit any affiliate's live coupon pages at any time without notice. Where an unauthorized, expired, or non-functional code is found, Company will issue written notice requiring takedown within 24 hours (48 hours for weekends/holidays). Failure to comply suspends the affiliate's account; a second violation within 12 months terminates the account.

**B.6 — Commission clawback**
Commission is void, and subject to clawback, on any order where the shopper landed via a page showing a code that violated B.1–B.3, regardless of whether the order otherwise would have qualified. This applies retroactively to the date the violating page went live, up to Company's standard chargeback window.

**B.7 — Trademark and paid-search carve-out**
Affiliate may not bid on Company's brand or product trademarks in paid search to promote a coupon page, whether or not the underlying code is authorized, except where separately licensed under a distinct trademark-bidding agreement.

---

**Open items for counsel / ops before finalizing:**
- A.5's CCPA "sale/share" characterization of the Slipstream data flow should get a specific look — receiving broad clickstream data from a partner can itself create obligations even if Palo Verde didn't collect it directly.
- A.1's "on Company's domain only" restriction needs confirmation from Slipstream's engineering side that their extension can actually scope its reporting that narrowly — if not, this becomes a go/no-go point for keeping the partner at current terms.
- B.2's feed requirement is the real fix for half the coupon sites — worth checking whether the tracking vendor can stand up this feed before the new terms go live, or whether there's a gap period to bridge.