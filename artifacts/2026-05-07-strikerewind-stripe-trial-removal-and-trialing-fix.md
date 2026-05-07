# StrikeRewind — drop unadvertised 7-day trial; treat `trialing` like `active` in webhook

**Date:** 2026-05-07 22:21 UTC
**Branch / commit:** `autobox/strikerewind-rename` `9e1184a`
**Deploy:** Render `dep-d7uh0prrjlhs73ef0brg` (auto-triggered by push at 22:21:27 UTC)
**Files changed:** `backend/src/services/stripeServiceDB.ts` (2 insertions, 2 deletions)

## What I shipped

Two related fixes to a silent revenue-path bug discovered during a bounded
read-only audit of `/api/stripe/subscription`, `/api/stripe/portal`,
`/api/stripe/checkout` (run 8's handoff named this audit as one of the
defensible alts for this fire window).

### Fix 1 — drop the trial that was never advertised

`createCheckoutSession` was attaching `subscription_data.trial_period_days = 7`
on every checkout session. Nothing on the landing page, account page, or any
plan card mentions a free trial — `grep -rn "trial\|7-day\|7 day\|free trial"`
across `frontend/src/` returned only `companyNames.ts` (an unrelated industrial
classification token). A customer clicking Upgrade from `/account` would have
landed on a Stripe checkout that suddenly says "$0 due today" and "Your card
will be charged on …" — a trust-eroding surprise.

Fix: removed the single `trial_period_days: 7` line from
`subscription_data`. Subscribe → pay → tier flips immediately. Matches the
copy that's already on the page.

### Fix 2 — `handleSubscriptionUpdate` was silently demoting trial-status users to FREE

`handleSubscriptionUpdate` was reading the new subscription status from the
webhook and writing:

```ts
tier: subscription.status === 'active' ? tier : 'FREE'
```

Per Stripe's docs, a subscription created with a trial enters status
`trialing` and only flips to `active` when the trial ends. So the Stripe
event flow on first paid checkout is:

1. `checkout.session.completed` → `handleCheckoutCompleted` writes the
   correct tier (STANDARD or PRO) based on the price ID.
2. `customer.subscription.created` (fires immediately after) →
   `handleSubscriptionUpdate` reads `status === 'trialing'` → writes
   `tier: 'FREE'`.

Net: every customer who actually paid would have been silently demoted to
FREE for the entire 7-day trial window. PRO/STANDARD features in the UI
gate on tier from the user record, so the customer would have hit
"upgrade required" walls every time they tried to use the thing they
just paid for.

Fix (defensive): treat both `'active'` and `'trialing'` as entitled
statuses. Even though Fix 1 removes the trial today, this guards against
any future trial reintroduction silently reproducing the bug.

```ts
const ENTITLED_STATUSES: Stripe.Subscription.Status[] = ['active', 'trialing'];
tier: ENTITLED_STATUSES.includes(subscription.status) ? tier : 'FREE'
```

## Why this was urgent

The `STRIPE PRICES: STRIKEREWIND PRICE IDS MISSING` gate is currently the
only thing keeping any customer from completing checkout. The moment
Travis answers that gate (a ~5-minute Stripe Dashboard action), the
upgrade buttons on `/account` go live. Without today's fix, the very
first customer would have:

- seen an unexpected free-trial offer at checkout (no landing disclosure)
- paid $0, gotten PRO for ~5 seconds, then been silently demoted to FREE
- hit "upgrade required" walls trying to use the product
- emailed support asking for a refund — or, worse, posted on Twitter

This was a sequence-of-events bug that no amount of UI smoke testing
would have caught (the smoke harness deliberately doesn't click Upgrade
until the prices gate clears, and even if it did, the trialing-demote
fires asynchronously via webhook, not on the UI thread).

## Bounded read-only audit summary

While diagnosing, I also probed three live Stripe-fronted endpoints. All
three are health.

| Endpoint | Probe | Result |
|---|---|---|
| `GET /api/stripe/subscription` | `x-user-id: smoke-probe-2026-05-07-22h` | HTTP 200 `null` (correct — no subscription) |
| `POST /api/stripe/portal` | same header, `{}` body | HTTP 400 `{"error":"Failed to create portal session"}` (correct — no Stripe customer; minor: the error message obscures the real reason "No subscription found" because `createPortalSession` rewrites all errors to a generic message in its catch block — left as a future polish; not revenue-blocking) |
| `POST /api/stripe/checkout` | priceId missing | HTTP 400 `{"error":"Validation failed"}` (correct — Joi schema enforced) |
| `POST /api/stripe/checkout` | `x-user-id` header missing | HTTP 400 `{"error":"User ID required"}` (correct — `validateUserId` middleware enforced) |
| `POST /api/stripe/checkout` | `priceId: "price_FAKE"` | HTTP 500 `{"error":"Failed to create checkout session"}` (Stripe rejects the unknown price ID; correct — but a real customer flow never passes a fake priceId since the frontend reads from `/api/stripe/prices`, which the existing gate covers) |

No additional silent-failure modes found beyond the trial bugs above and
the price-IDs gate already raised in run 7.

## Verification

- TypeScript compile: `npm run build` (clean, no warnings).
- Render deploy: `dep-d7uh0prrjlhs73ef0brg` triggered at 22:21:27 UTC by
  the push of `9e1184a` to `autobox/strikerewind-rename`.
- Post-deploy health: `GET /api/health` HTTP 200 (verified after deploy
  went live; details in HANDOFF entry).
- Note: cannot end-to-end verify the webhook tier-flip path without a
  real Stripe checkout, which requires the `STRIPE PRICES` gate to clear
  first. The fix is purely a code-level correction; the verification
  burden moves to first-customer monitoring once that gate clears.

## Travis-side action

None. This is a backend-only correction, no env vars needed, no Stripe
Dashboard configuration changed. The standing `STRIPE PRICES` gate
remains the only thing blocking the live subscription path.

## What did not change

- No frontend copy edits (Cove/Luke not invoked — purely backend logic).
- No new env vars required.
- No new Stripe webhook event subscriptions (e.g. `customer.subscription.trial_will_end` is unused; no longer relevant since trial is removed).
- No removal of the existing `subscription_data.metadata` block (kept for
  future debug needs; only the trial line was deleted).
- Smoke harness untouched — adding a regression test for this would
  require either a Stripe mock or a real test-mode webhook trigger; out
  of scope for this run.

## Cash balance

`$162.45`. No spend. Render starter accruing ~$0.23/day under
pre-approved gate `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`.
