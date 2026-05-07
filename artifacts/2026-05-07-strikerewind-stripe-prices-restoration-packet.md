# StrikeRewind — Stripe price IDs missing on Render (subscription path silently broken)

**Date:** 2026-05-07 18:18 UTC
**Run:** 7 of 2026-05-07
**Author:** AutoBox autonomous run
**Owner action:** Travis, ~5 min in Stripe Dashboard (live mode)

## TL;DR

Every "Upgrade" button on `https://www.strikerewind.com/account` currently alerts
*"Price not configured. Please contact support."* No one can subscribe. Cause: Render
service `srv-d7r408favr4c73fb3670` is missing two env vars that survived the original
2026-05-02 setup but were not restored after the env-wipe incident:
`STRIPE_STANDARD_PRICE_ID`, `STRIPE_PRO_PRICE_ID`. Live Stripe keys (`sk_live_*` /
`pk_live_*`) and webhook secret (`whsec_*`) ARE set correctly. This is a
revenue-path regression on a property that the owner is otherwise asking to be
public-ready.

## Evidence

`GET https://strikerewind-api.onrender.com/api/stripe/prices` (HTTP 200) returned
`{}` at 2026-05-07 18:17 UTC. The endpoint code at `backend/src/index.ts:369-374`
reads `process.env.STRIPE_STANDARD_PRICE_ID` and `process.env.STRIPE_PRO_PRICE_ID`
into the response; both unset → response is `{}`.

`Account.tsx:82-86` reads `prices.standard`/`prices.pro`, falsy → shows
`alert('Price not configured. Please contact support.')` and `return`s before
calling `createCheckoutSession`. Subscription flow dead end.

Render env-vars audit (via Render API, key names only):

```
FRONTEND_URL
HUNT_USE_FIXTURES
NODE_ENV
PORT
STRIPE_PUBLISHABLE_KEY      ← pk_live_* (correct)
STRIPE_SECRET_KEY           ← sk_live_* (correct)
STRIPE_WEBHOOK_SECRET       ← whsec_*  (correct)
SUPABASE_SECRET_KEY
SUPABASE_URL
                            ← STRIPE_STANDARD_PRICE_ID missing
                            ← STRIPE_PRO_PRICE_ID      missing
```

## Why this regressed

The original 2026-05-02 packet
(`artifacts/2026-05-02-strikerewind-stripe-live-products-and-webhook-packet.md`)
raised `STRIPE LIVE CONFIGURED: STRIKEREWIND` to set all 5 missing vars. Travis
provided the price IDs, AutoBox plugged them in, gate cleared. Then an env-wipe
incident later nuked all 5 vars. `TODO.md:49` records that
`STRIPE_SECRET_KEY` + `STRIPE_PUBLISHABLE_KEY` were restored and a new
`STRIPE_WEBHOOK_SECRET` was created fresh — but the two price-ID env vars were
not restored, and nothing in the deploy pipeline reads them at boot, so the
break was silent. Today's run audited `/api/stripe/prices` and surfaced it.

## Tier model in production code

Confirmed today on `autobox/strikerewind-rename` HEAD (commit `533b875`):

| Tier name | Monthly price | Env var |
|---|---|---|
| FREE | $0 | (no Stripe product) |
| STANDARD | $9.99 | `STRIPE_STANDARD_PRICE_ID` |
| PRO | $29.99 | `STRIPE_PRO_PRICE_ID` |

This is `Account.tsx:18-50` and `stripeServiceDB.ts:261-268` — finalized in
commit `d070a8f` ("Tier model finalized to Free / Standard ($9.99) / Pro
($29.99)"), which superseded the earlier Free/Pro/Ultra exploration. No code
change needed.

## Action — single recommendation, single approval line

Travis-owned, in Stripe Dashboard with **live mode toggle ON** (top-right of
dashboard must read "Viewing live data"):

1. **Products** → check whether "Standard" ($9.99/mo) and "Pro" ($29.99/mo)
   recurring products already exist in live mode.
   - **If yes:** open each, copy the price ID (`price_*`).
   - **If no:** create both as monthly recurring products with those exact
     prices, copy the price IDs.
2. Reply on Discord in the format:

   ```
   STRIPE PRICES: STRIKEREWIND
   STANDARD=price_<value>
   PRO=price_<value>
   ```

That's it. No new webhook endpoint, no new keys — those are already live and
correct from the prior restoration.

## What happens immediately on reply

1. AutoBox PUTs `STRIPE_STANDARD_PRICE_ID` and `STRIPE_PRO_PRICE_ID` to Render
   service `srv-d7r408favr4c73fb3670` via Render API.
2. Triggers redeploy (typical ~3 min).
3. Verifies `GET /api/stripe/prices` now returns
   `{"standard":"price_…","pro":"price_…"}`.
4. Hits the Account page in headless Playwright, asserts the upgrade button
   handlers no longer trip the "Price not configured" alert (without clicking
   through to live Stripe).
5. Extends the live smoke harness with a permanent regression assertion:
   `/api/stripe/prices` must return non-empty `standard` and `pro` fields
   on every future smoke run, so a future env-wipe does not regress silently.
6. Posts confirmation to Discord and updates TODO/HANDOFF/RUNLOG.

## Cost

$0. No new spend. The Render starter ($7/mo) is the only recurring cost on this
property and is already pre-approved.

## Blast radius if not addressed

While the marketing freeze is in place and traffic is ~zero, this is non-urgent.
But: the open `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` gate, when it
resolves to `EARLY ACCESS` or `TIGHTEN COPY`, will surface the live site to first
visitors. If the upgrade button alerts "Price not configured" on day one, that's
a credibility hit on the very first conversion attempt. Fixing this now is
strictly easier than fixing it after a launch post lands.

## Approval line

```
APPROVED: STRIPE PRICES: STRIKEREWIND
STANDARD=price_<value>
PRO=price_<value>
```

(Or "DECLINED" / "HOLD UNTIL POLYGON" — both are valid; the gate stays open
until decided.)
