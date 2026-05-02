# StrikeRewind: Stripe live mode is missing products + webhook — recommendation packet

**Date:** 2026-05-02
**Surface:** strikerewind.com (live, deployed earlier today)
**Status:** revenue-blocked — every subscription path is broken on production right now

## What the smoke test found

Site is up. Backend is healthy (`/api/health` returns `{"status":"ok"}`). DEV_MODE is correctly `false` on Render so FREE-tier limits enforce. Live keys are wired (`sk_live_` on Render, `pk_live_` on Vercel).

But the live site cannot take a subscription. Two endpoints prove it:

1. `GET https://strikerewind-api.onrender.com/api/stripe/prices` returns `{}` — empty.
   - The frontend reads this in `Account.tsx:82` as `prices.standard` and `prices.pro`. Both `undefined` means clicking Upgrade alerts `Price not configured. Please contact support.` and bails.

2. `POST https://strikerewind-api.onrender.com/api/stripe/webhook` returns `400 Webhook Error: Error: Stripe webhook secret not configured`.
   - `stripeServiceDB.handleWebhook` (`stripeServiceDB.ts:113`) throws on missing `STRIPE_WEBHOOK_SECRET`. Even if a customer somehow paid, `checkout.session.completed` would not flow to the DB and their tier would not upgrade.

Render env vars currently set on `srv-d7r408favr4c73fb3670`: `NODE_ENV`, `PORT`, `SUPABASE_URL`, `SUPABASE_SECRET_KEY`, `FRONTEND_URL`, `STRIPE_SECRET_KEY`. **Missing:** `STRIPE_STANDARD_PRICE_ID`, `STRIPE_PRO_PRICE_ID`, `STRIPE_WEBHOOK_SECRET`.

I queried Stripe live mode directly with the `sk_live_` key from Render: `GET /v1/products?active=true` returns `{"data": []}` — **no live products exist**. The live keys are valid, but the product catalog wasn't migrated from test mode to live mode after the key swap this afternoon. The webhook endpoint also was never registered against the live API.

## Why this matters now

Travis just put a marketing freeze in place pending a full round of testing. Testing checkout right now would surface this on the first attempt. Better to fix it before testing so testing becomes useful signal instead of "yep, checkout doesn't work."

## Travis action — three steps in Stripe Dashboard

All three live in **Stripe Dashboard with the live-mode toggle ON** (top-left of the dashboard — easy to miss after testing in test mode).

### Step 1: Create the two live products

Products → Add product → for each:

| Name | Pricing model | Price | Billing period |
|---|---|---|---|
| Standard | Recurring | $9.99 | Monthly |
| Pro | Recurring | $29.99 | Monthly |

After creating each product, copy the **price ID** (looks like `price_1OabcXYZ...`) — that's what AutoBox needs to set on Render. The product ID (`prod_...`) is not what we need.

### Step 2: Create the webhook endpoint

Developers → Webhooks → Add endpoint:

- **Endpoint URL:** `https://strikerewind-api.onrender.com/api/stripe/webhook`
- **Events to send:** select these five only —
  - `checkout.session.completed`
  - `customer.subscription.created`
  - `customer.subscription.updated`
  - `customer.subscription.deleted`
  - `invoice.payment_failed`

After creation, click into the endpoint → reveal the **Signing secret** (looks like `whsec_...`). Copy that.

### Step 3: Reply with the three values

Reply on Discord (or paste in the interactive thread) in this format so AutoBox can autonomously plug them into Render:

```
STRIPE LIVE CONFIGURED:
STANDARD_PRICE_ID=price_...
PRO_PRICE_ID=price_...
WEBHOOK_SECRET=whsec_...
```

## What AutoBox does on receipt

One bounded autonomous run, no further approvals needed:

1. PUT three new env vars to `srv-d7r408favr4c73fb3670` via Render API
2. Trigger Render redeploy (env var changes don't auto-redeploy)
3. Verify `/api/stripe/prices` returns `{ "standard": "price_...", "pro": "price_..." }`
4. Verify webhook endpoint stops returning the "not configured" error (probe with a body lacking signature → expect signature-verification error, not config error)
5. Test webhook delivery end-to-end via Stripe Dashboard's "Send test webhook" → verify `subscription_events` row appears in Supabase
6. Update state files; close the gate

## Single approval line

**`STRIPE LIVE CONFIGURED: STRIKEREWIND`** (added to `OPEN_GATES.md`)

## Cost / risk

Zero AutoBox spend. Travis-side cost: ~5 minutes in Stripe Dashboard. Reversible cleanly — products and webhook can be archived/deleted at will, env vars can be removed from Render via API.
