## The 87% number isn't wrong, it's just measuring the wrong thing

First, a small correction: 120/140 = **85.7%**, not 87% (worth fixing before it's on a slide).

But the bigger issue: that number is your **approval rate on applications received**, not a performance metric. It tells you how permissive your screening is. You could hit 100% by rubber-stamping everyone, or 20% by being pickier — neither says anything about whether the program is working. It's a vanity metric because:

- It ignores 500 of your 640 prospects (78%) who never applied at all.
- It says nothing about what those 120 approved affiliates actually _did_ — sent traffic, converted a sale, generated revenue.
- Your affiliate platform dashboard only exposes approvals and payouts, which silently drops the entire top of the funnel (outreach → application) and blurs the difference between "approved" and "producing."

## The full funnel you actually have

| Stage                  | Count      | Conversion from previous | Conversion from start |
| ---------------------- | ---------- | ------------------------ | --------------------- |
| Contacted              | 640        | —                        | 100%                  |
| Applied                | 140        | 21.9%                    | 21.9%                 |
| Approved               | 120        | 85.7%                    | 18.75%                |
| **Active / producing** | ❓ unknown | ❓                       | ❓                    |
| **Generated ≥1 sale**  | ❓ unknown | ❓                       | ❓                    |

The honest headline isn't "87% approval rate" — it's "**18.75% of contacted prospects became approved affiliates**," and even that stops at approval, before any of them have proven they can drive a sale.

The application rate (21.9%) is arguably the more interesting number to scrutinize: it's the stage where your outreach message, targeting, and offer actually get tested. A low number there is either a targeting problem (wrong prospects) or a pitch problem (wrong offer/message) — worth knowing separately from approval quality.

## What's missing entirely: outcomes

Approvals are an input metric — they measure your recruiting funnel, not the affiliate program's output. What's absent from the dashboard and from the slide:

- **Activation rate**: of the 120 approved, how many made at least one referral/sale within, say, 90 days of approval? This is usually the ugliest number in any affiliate program — a large share of "approved" affiliates never send a single click.
- **Revenue generated** and **payouts made** per cohort — you said the dashboard _does_ give you payouts, so pull it, just tie it to the cohort, not just aggregate totals.
- **Net contribution**: revenue generated minus payouts minus outreach labor cost. This is the number that actually belongs on a quarterly review slide to leadership.
- **Time-to-first-sale**: from approval to first commission-earning action — tells you if the program ramps fast or if affiliates go dormant.
- **Concentration**: what % of revenue comes from your top 10-20 affiliates? Affiliate programs are almost always power-law distributed; if 5 people drive 80% of revenue, "120 approved" is a misleading denominator for everything.
- **Cost per approved affiliate** and **cost per producing affiliate**: 640 outreach touches cost time/tooling — divide that cost by 120 approvals, then again by however many actually produced. The second number is usually much more sobering.

## What to put on the slide instead

Replace the single 87% stat with a funnel + one outcome number:

> "640 contacted → 140 applied (21.9%) → 120 approved (85.7% of applicants) → **N active, generating $X in revenue / $Y net after payouts**."

If you don't have the activation/revenue numbers yet for last quarter, say so explicitly rather than filling the gap with the approval rate — "we don't yet track post-approval performance; fixing that this quarter" is a more credible slide than a polished-looking number that measures nothing.

## How to track this going forward

The root cause is that you're relying on the affiliate platform's dashboard as your source of truth, but it only instruments the stages _it_ owns (application → approval → payout). Outreach and activation live outside it. You need your own lightweight funnel table alongside the platform.

**Data model** (a Postgres table is plenty at this volume):

```sql
CREATE TABLE affiliate_prospects (
    id              BIGSERIAL PRIMARY KEY,
    contacted_at    TIMESTAMPTZ NOT NULL,
    source          TEXT NOT NULL,          -- outreach channel/list
    applied_at      TIMESTAMPTZ,            -- NULL if never applied
    approved_at     TIMESTAMPTZ,            -- NULL if rejected/pending
    rejected_at     TIMESTAMPTZ,
    platform_ref    TEXT,                   -- affiliate ID on the platform, to join payouts back
    first_sale_at   TIMESTAMPTZ,            -- pull from platform's conversion/payout events
    status          TEXT NOT NULL DEFAULT 'contacted',
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

Then join `platform_ref` against whatever the platform exposes for conversions/payouts (API export, if the platform has one) to backfill `first_sale_at` and lifetime revenue per affiliate.

**Cadence**:

1. Log every outreach contact the day it happens (not batched at quarter-end) — a spreadsheet row is fine if a DB is overkill for now, but it must exist somewhere you control, since the platform will never show you the 500 who never applied.
2. Each quarter, report **two things**, not one: the new cohort's funnel (contacted → applied → approved) and the **maturing performance of prior quarters' cohorts** (activation rate, revenue), since this quarter's approved affiliates haven't had time to prove themselves yet.
3. Track cohort-by-cohort, not just point-in-time totals — an affiliate approved in month 3 of the quarter hasn't had the same runway as one approved in month 1, so blending them into one "quarter" number understates a young cohort and overstates nothing meaningful.

The one-sentence version: **stop reporting the ratio your tool hands you for free, and start reporting the ratio that reflects whether the program made money** — contacted → applied → approved → active → revenue, with the last two numbers being the ones that matter and the ones currently missing.
