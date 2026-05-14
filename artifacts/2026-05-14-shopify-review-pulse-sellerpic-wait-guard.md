# Shopify Review Pulse SellerPic Wait Guard

Date: 2026-05-14

## Task

Make the active SellerPic validation wait executable and hard to violate, without creating new buyer collateral or contacting another prospect.

## Why This Task

SellerPic was sent from `reviewpulse@theshepherdstack.com` at approximately `2026-05-14 20:32 UTC`. The current revenue experiment is now a live willingness-to-pay wait, not a build queue.

Starting A2Reviews, Kaching, MAG, or Extension Review Pulse early would corrupt the one-recipient test. Building more Review Pulse collateral during the wait would also be drift.

## Built

- `workspace/shopify-review-pulse/outreach/wait_guard.mjs`
- `workspace/shopify-review-pulse/tests/wait_guard.test.mjs`
- Updated `workspace/shopify-review-pulse/README.md` with the guard command.

Run:

```bash
node workspace/shopify-review-pulse/outreach/wait_guard.mjs --json
```

The guard reads `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`, parses the sent timestamp and fallback timestamp, and returns whether fallback outreach is allowed.

## Current Guard Result

At run time, the guard returned:

```json
{
  "status": "waiting",
  "allowedFallback": false,
  "waitHoursRemaining": 70.21,
  "nextAction": "Do not contact A2Reviews, Kaching, MAG, or other Review Pulse targets yet.",
  "senderMailbox": "reviewpulse@theshepherdstack.com",
  "recipient": "support@sellerpic.ai",
  "sentAt": "2026-05-14T20:32:00.000Z",
  "fallbackAt": "2026-05-17T20:32:00.000Z",
  "outcome": "waiting"
}
```

## Live Conversion Checks

- `https://shopify-review-pulse-eta.vercel.app/offer` returned HTTP 200.
- The live offer contains the Stripe checkout URL `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`.
- The Stripe checkout URL returned HTTP 200.

## Verification

```bash
node --check workspace/shopify-review-pulse/outreach/wait_guard.mjs
node --test workspace/shopify-review-pulse/tests/*.test.mjs
```

Result: 5/5 tests passed.

## Decision

No fallback outreach is allowed before `2026-05-17 20:32 UTC` unless SellerPic replies first or Travis gives fresh explicit instruction.

No new gate was added. `config/OPEN_GATES.md` remains intentionally empty.

Cash balance remains `$162.45`.
