## What's actually happening

This is almost certainly **attribution hijacking via a browser extension or ad-injection software**, not a real referral. It's an extremely common pattern with client-side pixel tracking, and it fits every symptom you listed:

- **"We've never seen them send traffic"** — because they don't send traffic. The affiliate's tracking script fires _on your checkout page itself_, not on a landing page the customer visited on DealBurrow's site.
- **"Customers found us organically through search"** — the customer's browser has a coupon/cashback extension installed (Honey, Capital One Shopping, PayPal Honey, RetailMeNot Genie, Piggy, various "deal finder" toolbars — or a less reputable clone). When the customer lands on your checkout or product page, the extension silently injects an iframe or fires a request to the affiliate network that writes DealBurrow's affiliate cookie, overwriting whatever attribution (or lack of it) existed before.
- **Client-side pixel tracking is exactly what's exploitable here** — if your model is "last cookie present at time of purchase gets the commission," anything that can write a cookie in that customer's browser can claim the sale. No click, no visit, no referral needed.

This is usually called **cookie stuffing** or **extension-based attribution fraud** in affiliate-marketing fraud literature — one of the most common exploits of last-click, cookie-based attribution.

## Step 1: Confirm it, don't assume it

1. **Pull DealBurrow's click logs from your affiliate network** (impact.com, PartnerStack, CJ, Everflow, whatever you use) for the flagged orders. Look at:
   - Click timestamp vs. order timestamp — genuine referral clicks happen minutes to days before purchase; stuffed cookies often land seconds before checkout, or exactly at checkout page load.
   - IP address / user agent on the click record — missing, generic, or datacenter IPs are a red flag; a real click has a normal residential IP and full browser UA.
   - Landing page URL the click supposedly hit — ask the network or DealBurrow directly which page on your site the click landed on. If they can't produce one, that's your answer.

2. **Reproduce it yourself.** Install a few popular shopping extensions in a clean browser profile, search your brand name on Google, click the organic result, go through checkout, and open DevTools → Network tab filtered on your affiliate network's tracking domain. Watch for a request firing with DealBurrow's ID that you never initiated by visiting their site.

3. **Check your own session recordings/analytics** (if you have Hotjar/FullStory/GA) for a sample of the disputed orders — confirm the entry channel really was organic search, with no visit to any external deal site in the session.

## Step 2: Stop the bleeding on payouts

- **Hold, don't pay, DealBurrow's pending commissions** while you investigate — every affiliate network's terms allow this for suspected fraud.
- **Check your clawback/validation window.** If you've already paid some of these, you're within your rights to claw them back if fraud is confirmed — check the program's stated clawback period.
- **Ask DealBurrow directly for proof**: "Show us the landing page and traffic source for order #X." A legitimate affiliate can answer immediately. A cookie-stuffer will stall, get vague, or disappear.
- **Check their approved promotional methods** in your program terms. Most affiliate agreements explicitly restrict or ban browser extensions/toolbars, or require disclosure and approval for that channel. If DealBurrow never disclosed operating an extension, that alone is a terms violation you can act on without even proving stuffing.

## Step 3: Fix the tracking so this can't keep happening

The root cause is that a **client-side pixel with pure "last cookie wins" logic trusts any cookie present at conversion**, regardless of whether a real click preceded it. Fixes, roughly in order of effort:

1. **Move to click-ID-based attribution instead of pure cookie presence.** Require a valid `click_id`/`sub_id` that your own system (or the network) issued at an actual outbound click, and validate it server-side at conversion — don't just check "is an affiliate cookie present."
2. **Add attribution priority rules**: if the session's first-touch channel was organic/direct (visible in your own first-party analytics) and no affiliate click was logged _before_ that first-party session started, override/ignore any affiliate cookie that shows up later in the same session. Many networks (Impact, Everflow) support "coupon/extension exclusion" or "channel priority" rules for exactly this — turn them on.
3. **Ask your affiliate network if they offer extension/cookie-stuffing detection.** Impact.com, Everflow, and Trackier all have fraud modules that specifically flag "last-click override," "zero-duration sessions," and known extension signatures — worth turning on if you're not already using it.
4. **Consider first-click or time-decay attribution instead of last-click** for at least a probationary period — it structurally weakens the value of late cookie injection.
5. **Server-side conversion validation**: fire the conversion event from your backend (order confirmation), not purely client-side, and cross-check the referring click record before crediting — this closes the door on pixel-only manipulation.

## Step 4: Decide DealBurrow's fate

Once you have even 5–10 confirmed cases with no landing-page evidence and no real click, that's enough to:

- Suspend them from the program immediately.
- Claw back paid commissions within your window.
- Terminate for terms violation (undisclosed traffic source / no bona fide referral) rather than needing to "prove" malicious intent — absence of a real click is enough on its own.

If you want, tell me which affiliate network you're on (impact.com, PartnerStack, CJ, Everflow, etc.) and I can give you the exact report/filter to pull the click evidence and the specific anti-fraud setting to enable.
