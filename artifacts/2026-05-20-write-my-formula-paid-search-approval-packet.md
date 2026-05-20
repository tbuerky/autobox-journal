# Write My Formula paid-search approval packet

Date: 2026-05-20 16:19 UTC

## Decision

Recommend one tiny Google Search test for Write My Formula because the product is live and paid-ready, but the last 24-hour funnel summary shows no real traffic.

Approval line:

`APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15`

## Current evidence

`npm run analytics:summary -- --since=24h` returned:

- `sessions`: `0`
- `analyticsEvents`: `{}`
- `formulaEvents`: `{}`
- `waitlistEvents`: `{}`
- `paidSuccessPageViews`: `0`
- Stripe Payment Link sessions: `1` total recent session, `0` paid, `1` open/unpaid
- Latest Stripe session: `cs_live_a1ZEGcSYIZ8VAPdTWoDwzZrDNZ9tVl0RjFXlpoNuuqv3YRJ7RUDUQrc4YA`, open/unpaid, `$9.00`, created `2026-05-20T15:33:38.000Z`

Interpretation: the revenue surface is technically ready, but it has not had enough buyer-intent visits to test willingness to pay.

## Live market check

- SheetGPT is an active paid Excel/Google Sheets formula product claiming `90,000+` formulas generated, an `$8/mo` plan, and a formula-generator paywall pattern: https://sheetgpt.pro/
- ExcelGPT presents the same broad category as an AI Excel assistant and formula generator, with visible claims of `50,000+` users and `4.8/5` reviews: https://excelgpt.app/
- Google's Keyword Planner guidance says advertisers can add candidate keywords to a plan, set daily budget, bid maximum, and location, then review forecasted clicks, impressions, and conversion estimates before launch: https://business.google.com/us/resources/articles/using-google-ads-keyword-planner/
- Google Ads supports setting an average daily budget that can be changed at any time: https://support.google.com/google-ads/answer/2375420
- Google Ads bid-strategy docs say Maximize Clicks can use a campaign-level maximum CPC bid, while Manual CPC lets the advertiser manage maximum CPC bids directly: https://support.google.com/google-ads/answer/2472725

This category has visible commercial competition. A capped Search test is a cleaner validation step than adding a 20th SEO page before any user signal exists.

## Test spec

Prepared file: `workspace/sheetpilot-workbench/ads/google-search-test.md`

- Budget cap: `$15`
- Stop condition: stop after `$15` spend or `30` clicks, whichever happens first
- Landing page: `https://writemyformula.com/?utm_source=google_ads&utm_campaign=formula_generator_test`
- Keywords: exact or phrase match only
  - `excel formula generator`
  - `google sheets formula generator`
  - `fix excel formula`
  - `explain excel formula`
  - `xlookup formula generator`
- Negative keywords:
  - `free download`
  - `template`
  - `course`
  - `job`
  - `salary`
  - `pdf`
  - `certification`
  - `tutorial`

## Launch constraints after approval

- Use Search only, not Display, Performance Max, Demand Gen, or broad match.
- Use the existing first-party funnel summary before and after launch.
- Do not raise budget without a new approval.
- Continue only if there is at least one real checkout click, signup, or strong formula-use session before the cap is hit.
- Stop if spend reaches the cap with no checkout clicks and no meaningful formula usage.

## Options considered

- Add another SEO page: rejected for this run because 19 strengthened SEO entry pages are already live and the current signal problem is zero measured sessions.
- Manual outreach: rejected because the current instruction says not to send outreach or ask Travis to post on social.
- Wait: rejected because the product has no traffic signal to wait on yet.
- Tiny paid search: selected because it buys buyer-intent visits into a live $9 checkout with a hard, owner-approved cap.

## Gate raised

Added to `config/OPEN_GATES.md`:

`APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15`

No ads were launched, no account changes were made, no public post was made, and no money was spent.
