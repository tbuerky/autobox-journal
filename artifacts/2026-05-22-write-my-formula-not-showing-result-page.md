# Write My Formula formula-not-showing-result page

Date: 2026-05-22 18:22 UTC

## Result

Shipped one search-term-matched page for the live Write My Formula paid-search test:

- Live page: https://writemyformula.com/excel-formula-not-showing-result/
- Deployment: `dpl_FgPeh4FMakDdvTcbUWeqVMA8m7qx`
- Production alias: `https://writemyformula.com`
- Screenshots:
  - `output/playwright/write-my-formula-not-showing-result/local-desktop.png`
  - `output/playwright/write-my-formula-not-showing-result/local-mobile.png`
  - `output/playwright/write-my-formula-not-showing-result/live-desktop.png`
  - `output/playwright/write-my-formula-not-showing-result/live-mobile.png`

## Why this task

Fresh owner-provided Google Ads signal showed the live campaign `WMF - Formula Specific Search - $15 Test` has `9` impressions, `0` clicks, `$0.00` spend, and relevant visible search terms including `excel formula not showing result`, `formula for conditional formatting in excel`, and `google sheets conditional format custom formula`.

The highest-leverage no-spend task was to create a page that exactly matches the strongest visible fix-intent term and routes users into the existing formula-fixer workbench and `$9` checkout path.

## Live source evidence

Sources checked before page copy:

- Microsoft Support, Excel calculation settings: https://support.microsoft.com/en-us/office/change-formula-recalculation-iteration-or-precision-in-excel-73fc7dac-91cf-4d36-86e8-67124f6bcce4
- Microsoft Support, formula error checking: https://support.microsoft.com/en-us/office/detect-formula-errors-in-excel-3a8acca5-1d61-4702-80e0-99a36a2822c1
- Google Docs Editors Help, conditional formatting custom formulas: https://support.google.com/docs/answer/78413
- Google Sheets API conditional formatting rules: https://developers.google.com/workspace/sheets/api/guides/conditional-format

Relevant constraints from those sources:

- Excel calculation mode can be automatic or manual, and manual mode requires explicit recalculation.
- Excel formula errors can come from syntax, argument/data-type problems, text-formatted numbers, inconsistent references, omitted cells, and other common rules.
- Google Sheets conditional formatting custom formulas should evaluate to a condition used by a formatting rule; references and applied range matter.

## Work completed

- Added `excel-formula-not-showing-result` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Regenerated `workspace/sheetpilot-workbench/excel-formula-not-showing-result/index.html`.
- Linked the page from the homepage Common formulas grid.
- Added the URL to `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Routed public-copy direction through Luke; used the pain-first framing and avoided unsupported "always fix" or time-guarantee claims.
- Deployed production with the correct Vercel scope/token for the live `sheetpilot-workbench` project.
- Submitted the new page, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `29/29`.
- `python3 -m json.tool vercel.json` passed.
- Local route `/excel-formula-not-showing-result/` returned HTTP `200`.
- Local desktop/mobile browser screenshots were captured and checked for H1, fix-mode preset, and Stripe checkout href.
- Production route `/excel-formula-not-showing-result/` returned HTTP `200`.
- Production page contains the title, H1, calculation-mode/text-formatted-cell copy, fix-mode page preset, and live `$9` Stripe checkout URL.
- Production homepage links to the new page.
- Production sitemap includes the new page.
- Live Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile browser screenshots were captured.
- Public-copy scan found no internal process language, stale `$49`, stale `$15`, or approval-gate language in the changed public HTML.

## Gate reconciliation

Removed `APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15` from `config/OPEN_GATES.md` because the fresh owner message reports an active Google Ads campaign with current impressions, search terms, and spend state. The ad campaign exists; the launch decision is no longer pending.

## No-go actions

No new ads were launched, no campaign settings were changed, no budget or bids were changed, no outreach was sent, no payment infrastructure was created, no DNS/account/public post action occurred, and no money was spent.

Current cash balance remains `$35.93`.
