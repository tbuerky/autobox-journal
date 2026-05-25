# Write My Formula Excel #NAME? error page - 2026-05-25

## Task
Ship one no-spend repair-intent page for Excel `#NAME?` formula errors on the live Write My Formula product.

## Output
- Live page: https://writemyformula.com/excel-name-error/
- Commit: `d6f7a33 Add Excel NAME error page`
- Deployment: `dpl_7uVuVENEzS27Y3Ukj1gXbYyoEMvX`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-name-error/`
- Luke copy review: `workspace/sheetpilot-workbench/luke-excel-name-error-page.md`

## Evidence
Live research checked Microsoft Support's current `#NAME?` guidance, which frames the error as a formula syntax issue commonly caused by misspelled function names, undefined names/named ranges, missing double quotes around text, missing colons in ranges, add-in-dependent functions, and unsupported/custom functions. Microsoft also warns against masking the error with `IFERROR` before resolving the underlying syntax.

Current search results also show active formula-fixer competition around Excel/Sheets formula generation and repair, so the page fits the existing Write My Formula wedge: one formula, one repair, in-browser, with the live `$9` founding-access checkout.

## Changes
- Added `excel-name-error` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-name-error/index.html`.
- Regenerated existing static SEO pages and `sitemap.xml`.
- Linked the new page from the homepage Common formulas section.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.

## Verification
- `npm run build:seo && npm test` passed `44/44`.
- Public-copy scan passed for the new page and homepage.
- Local route, homepage, and sitemap returned HTTP `200`.
- Local desktop and mobile screenshots captured.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage links `/excel-name-error/`.
- Live sitemap includes `https://writemyformula.com/excel-name-error/`.
- Live Playwright checks found the expected H1, valid checkout URL, homepage link, and `0` console errors on desktop and mobile.
- IndexNow accepted page/home/sitemap with HTTP `202`.

## Boundaries
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Final copy avoids file upload, workbook audit, guarantee, refund, PDF, same-day, human-reviewer, official-affiliation, unlimited-fix, and pay-before-answer claims.

## Budget
Spend: `$0`. Current cash balance remains `$35.93`.
