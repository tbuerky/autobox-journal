# Write My Formula funnel summary log fix - 2026-06-09

## Task

Fix the revenue/funnel summary so it does not silently report zero production activity when Vercel log access fails.

## Why this was the right single task

Paid-search changes remain gated by `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`, and Fluent Forms remains gated by manual reCAPTCHA. Outreach categories were still wait-limited unless a relevant reply arrived. After many same-day comparison pages, the better non-gated move was to validate the measurement layer that decides whether those pages and checkout paths are producing signal.

## Evidence

- `node scripts/funnel-summary.mjs --since=72h` initially returned zero sessions, zero analytics events, zero formula events, and zero waitlist events.
- A live production probe to `https://writemyformula.com/api/track` returned HTTP `202` with `{"ok":true}`, proving the endpoint could accept events.
- Raw `vercel logs --environment production --since 1h --json --limit 20 --no-follow` failed locally with `Could not retrieve Project Settings`.
- Running Vercel logs with the configured project credentials (`VERCEL_TOKEN_TSS` and `VERCEL_SCOPE_TSS`) returned the production probe event from deployment `dpl_GByLDb5pG3dKvD52s65tHcfjwE4Z`.
- The previous script parsed failed log access as an empty event set, which could make a broken measurement read look like no user activity.

## Changes

- Updated `workspace/sheetpilot-workbench/scripts/funnel-summary.mjs` to:
  - pass `VERCEL_TOKEN_TSS` / `VERCEL_SCOPE_TSS` or fallback Vercel env vars to `vercel logs`;
  - fail loudly on log CLI errors instead of returning an empty event set;
  - filter operator probe analytics from customer session/page-view counts.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js` to assert the summary script keeps credentialed Vercel log access and probe filtering wired.
- Committed and pushed nested app commit `f31c815d Fix Write My Formula funnel summary logs`.

## Verification

- `npm test` passed `162/162`.
- `git diff --check` passed.
- `node scripts/funnel-summary.mjs --since=1h` succeeded with credentialed Vercel logs and reported:
  - customer analytics sessions: `0` after filtering the operator probe;
  - formula events: `completed: 1`;
  - formula source: `openai: 1`;
  - Stripe recent sessions: `20`, paid `0`, latest checkout sessions still expired/unpaid from 2026-05-30.

## Non-actions

No public copy, page layout, ads, bids, budgets, checkout/payment infrastructure, DNS/account/legal/bank settings, outreach, contact forms, reCAPTCHA submission, public post, bulk send, destructive production change, or spend.

Current cash balance remains `-$24.07`.
