# Write My Formula conditional formatting page refresh

Date: 2026-05-22 20:22 UTC

## Result

Refreshed the live conditional-formatting landing page to better match the visible paid-search terms:

- Live page: https://writemyformula.com/conditional-formatting-formula-generator/
- Deployment: `dpl_Abis2uxsE6dnLzhgNxqCzmqPZTU7`
- Production alias: `https://writemyformula.com`
- Screenshots:
  - `output/playwright/write-my-formula-conditional-formatting/local-desktop.png`
  - `output/playwright/write-my-formula-conditional-formatting/local-mobile.png`
  - `output/playwright/write-my-formula-conditional-formatting/live-desktop.png`
  - `output/playwright/write-my-formula-conditional-formatting/live-mobile.png`

## Why this task

Fresh owner-provided Google Ads signal showed relevant visible search terms including `formula for conditional formatting in excel` and `google sheets conditional format custom formula`. The site already had `/conditional-formatting-formula-generator/`, so the highest-leverage no-spend move was to sharpen that existing page instead of adding a duplicate URL.

## Live source evidence

- Microsoft Support, conditional formatting formulas: https://support.microsoft.com/en-us/office/use-conditional-formatting-to-highlight-information-fed60dfa-1d3f-4e13-9ecb-f1951ff89d7f
- Google Docs Editors Help, conditional formatting custom formulas: https://support.google.com/docs/answer/78413
- Microsoft Support, relative/absolute references: https://support.microsoft.com/en-gb/office/switch-between-relative-absolute-and-mixed-references-dfec08cd-ae65-4f56-839e-5f0d8d0baca9

Relevant constraints applied:

- Conditional formatting formulas should evaluate to TRUE/FALSE.
- Relative, absolute, and mixed references matter because rules are evaluated across an applied range.
- Google Sheets custom formulas can use same-sheet references directly; cross-sheet references require `INDIRECT`.

## Work completed

- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` for the conditional-formatting page title-adjacent copy, lede, intent, checks, usage guidance, and worked example read.
- Updated the homepage Common formulas card to mention Excel and Google Sheets custom formulas directly.
- Regenerated `workspace/sheetpilot-workbench/conditional-formatting-formula-generator/index.html`.
- Added focused content assertions in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Routed the public-copy direction through Luke, then corrected/grounded the copy against Microsoft and Google documentation.
- Deployed production and submitted the refreshed page, homepage, and sitemap to IndexNow.

## Verification

- `npm run build:seo && npm test` passed `29/29`.
- `python3 -m json.tool vercel.json` passed.
- Local desktop/mobile browser screenshots were captured and checked for the new H1, `INDIRECT` guidance, and Stripe checkout href.
- Production route `/conditional-formatting-formula-generator/` returned HTTP `200`.
- Production page contains the new rule-dialog H1, Google Sheets `INDIRECT` guidance, applied-range copy, and live `$9` Stripe checkout URL.
- Production homepage links to the refreshed page with the updated card copy.
- Production sitemap includes the page.
- Live Stripe checkout URL returned HTTP `200`.
- IndexNow accepted the refreshed page/home/sitemap set with HTTP `200`.
- Live desktop/mobile browser screenshots were captured.
- Public-copy scan found no internal process language, stale `$49`, stale `$15`, approval-gate language, or guarantee language in the changed public HTML.

## No-go actions

No ad settings were changed, no budgets or bids were changed, no outreach was sent, no payment infrastructure was created, no DNS/account/public post action occurred, and no money was spent.

Current cash balance remains `$35.93`.
