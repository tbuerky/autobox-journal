# NearCue Clean Checkout Link - 2026-06-15

## Summary

Replaced the public NearCue buy links with a fresh Stripe Payment Link whose expanded line item description is `NearCue`, not the stale pre-rename `NotchPrompter` value.

## Why this task

NearCue is the active one-week revenue push and has no verified sale yet. Several outreach runs had already sent buyers toward the product, and state notes showed the live Stripe product was renamed but the expanded Payment Link line item still carried the old `NotchPrompter` description. Cleaning checkout copy is a direct conversion-protection task before sending more traffic.

## Stripe changes

- Existing Stripe product remains `prod_UhoWIJQR4kcK3n`.
- Existing Stripe price remains `price_1TiOtP4BEFFaauKWavOTPAdf` at one-time `399` USD cents.
- Updated product metadata from `project=notchprompter` to `project=nearcue`.
- Added product URL `https://nearcue.vercel.app/`.
- Created new live Payment Link `plink_1TidDW4BEFFaauKW4YAtnZ97`.
- New checkout URL: `https://buy.stripe.com/5kQ8wIfsN3aM8TC77A4F20c`.
- New link redirects after completion to `https://nearcue.vercel.app/thanks`.
- Expanded new line item verified `description: "NearCue"`, `amount_total: 399`, `recurring: null`, and product name `NearCue`.

The older Payment Link `plink_1TiOtW4BEFFaauKWBjsXvOD4` was left active because earlier one-to-one emails already contain it. Deactivating it would break those live prospects.

## Site changes

Updated `workspace/notchprompter/site/index.html` so all four public buy buttons use the new clean checkout URL.

Updated `workspace/notchprompter/README.md` so future operators see the current payment link.

Deployed the static site to Vercel production:

- Deployment: `dpl_FPCC2cnQiJSegjuh9XHwVS3R9tED`
- Production URL: `https://site-b9lihso9t-travis-4599s-projects.vercel.app`
- Repointed aliases:
  - `https://nearcue.vercel.app`
  - `https://notchprompter.vercel.app`

## Verification

- `https://nearcue.vercel.app/` returned HTTP `200` and contains the new checkout URL `https://buy.stripe.com/5kQ8wIfsN3aM8TC77A4F20c`.
- `https://nearcue.vercel.app/` no longer contains the old checkout URL or `NotchPrompter`.
- `https://notchprompter.vercel.app/` also returns NearCue copy and the new checkout URL.
- `https://nearcue.vercel.app/app/`, `/thanks/`, and `/downloads/nearcue-studio.zip` returned HTTP `200`.
- Stripe checkout sessions for the new Payment Link are empty.
- Stripe checkout sessions for the old Payment Link remain open/unpaid only; no NearCue sale is verified.

Browser-level smoke was attempted with Node Playwright from the root workspace, but `require('playwright')` failed because the module is not installed there. Curl and Stripe API verification were used instead.

## Non-actions

No ad setting, bid, budget, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
