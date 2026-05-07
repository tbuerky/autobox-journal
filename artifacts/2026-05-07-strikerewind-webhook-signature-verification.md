# StrikeRewind — live Stripe webhook signature-verification audit

**Run:** 2026-05-07 run 6 (~16:18 UTC)
**Target:** `https://strikerewind-api.onrender.com/api/stripe/webhook`
**Why now:** TODO line 48 has been parked since the Render env-wipe incident: *"STRIPE_WEBHOOK_SECRET was created fresh (`we_1TT7tMAy6OYpygDjm6zXKzCq`, `whsec_3NyYLQfjTRo2Ag9ZjSFEV4prPtqXhE96`) and added. Verify webhook fires correctly on test checkout after Playwright suite confirms the UI is working."* The Playwright suite passed 29/29 in run 2 this morning, so the prerequisite is met. A real test-checkout requires either Stripe CLI on the box or a live customer card swipe (revenue-relevant; not autonomous). What IS bounded and autonomous is verifying the live endpoint enforces Stripe-signature validation — i.e., that a forged or unsigned webhook can NOT promote a fake `checkout.session.completed` event to "subscription paid". This is the security check that defends subscription revenue before any customer exists.

## Threat model

If the live webhook endpoint accepted unsigned events, anyone could POST a forged `checkout.session.completed` body to `https://strikerewind-api.onrender.com/api/stripe/webhook` and the backend would treat it as a paid subscription — promoting an arbitrary user to PRO/ULTRA tier without payment. This is the canonical Stripe-webhook security mistake.

## Code review (offline)

`backend/src/index.ts:76-77` mounts `express.raw({ type: 'application/json' })` only for `/api/stripe/webhook`, which preserves the raw body required for HMAC verification. `backend/src/index.ts:357-367` reads `req.headers['stripe-signature']` and delegates to `stripeService.handleWebhook(req.body, signature)`; on any throw, the catch block returns 400. `backend/src/services/stripeServiceDB.ts:113-126` calls `stripe.webhooks.constructEvent(payload, signature, webhookSecret)` — the Stripe SDK's standard signature-verification call, which throws on missing/invalid/expired signatures. The pattern matches Stripe's documented integration; nothing custom or hand-rolled in the verification path.

## Live probe results

Five `curl` probes against the production endpoint at 2026-05-07 16:18 UTC:

| # | Request | Expected | Actual | ✓ |
|---|---|---|---|---|
| 1 | POST, no `stripe-signature` header | 400 reject | HTTP 400 — `Webhook Error: Error: Webhook verification failed` | ✓ |
| 2 | POST, `stripe-signature: t=1714512000,v1=fakefakefake` | 400 reject | HTTP 400 — `Webhook Error: Error: Webhook verification failed` | ✓ |
| 3 | POST, malformed `stripe-signature: this-is-not-a-signature` | 400 reject | HTTP 400 — `Webhook Error: Error: Webhook verification failed` | ✓ |
| 4 | POST, empty body, bogus signature | 400 reject | HTTP 400 — `Webhook Error: Error: Webhook verification failed` | ✓ |
| 5 | GET on `/api/stripe/webhook` | 404 (POST-only route) | HTTP 404 — `Cannot GET /api/stripe/webhook` | ✓ |

All five behave correctly. The endpoint:

1. Will not accept any event without a valid signature.
2. Will not accept a forged signature.
3. Does not expose method-disclosure beyond Express's standard 404.
4. Does not leak the webhook secret in error responses (the body returns only `"Webhook verification failed"` — Stripe SDK's standard error message, no key material).

## What this does NOT verify

- That the webhook secret on Render matches the secret on the Stripe-side endpoint `we_1TT7tMAy6OYpygDjm6zXKzCq`. A real test-event from Stripe Dashboard ("Send test webhook") OR a sandbox `stripe trigger checkout.session.completed` would prove the round-trip. Either path requires the live `STRIPE_SECRET_KEY`, which is correctly NOT on this box.
- That the post-verification logic (`handleWebhook` → Supabase tier write) actually mutates the right row. That is exercised the moment Travis (or a real customer) completes a Stripe Checkout session.
- That rate-limiting on the endpoint behaves correctly under burst (the trust-proxy fix from run 5 unblocks per-IP enforcement, but the webhook endpoint may sit on its own limiter; left as a future bounded check rather than running 100+ probes that show in logs).

## Recommendations (no Travis approval required)

1. **Travis-when-convenient:** open Stripe Dashboard → Webhooks → endpoint `we_1TT7tMAy6OYpygDjm6zXKzCq` → "Send test webhook" → fire a `checkout.session.completed` payload → confirm the dashboard shows a 200 response and a Supabase row update lands. This is the round-trip proof. Reply `STRIPE WEBHOOK ROUND-TRIP: PASS` when done.
2. **No code change needed.** The endpoint behaves correctly. The verification path is the standard SDK call; no homegrown HMAC.

## Suggested post copy

> Run 6 today: bounded security probe on the live StrikeRewind Stripe webhook. Sent 5 forged/unsigned requests to https://strikerewind-api.onrender.com/api/stripe/webhook and confirmed all 4 POST variants return 400 "Webhook verification failed" plus GET returns 404. The endpoint won't accept any event without a valid Stripe signature — fake "checkout.session.completed" payloads can't promote a user to PRO. Real round-trip test still belongs to you (Stripe Dashboard → "Send test webhook" on we_1TT7tMAy6OYpygDjm6zXKzCq, ~30 sec). Two gates still on you: LAUNCH POSTURE (StrikeRewind copy) and ADS DECISION (PAF Search extend). Cash $162.45.
