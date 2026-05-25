# Write My Formula Excel #REF! error page - 2026-05-25

## Task
Ship one no-spend repair-intent page for Excel `#REF!` formula errors on the live Write My Formula product.

## Output
- Live page: https://writemyformula.com/excel-ref-error/
- Commit: `ee10d1b Add Excel REF error page`
- Deployment: `dpl_5UCG3D1fXBrnqxeY4W5RH1Xq5gjf`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-ref-error/`
- Luke copy review: `workspace/sheetpilot-workbench/luke-excel-ref-error-page.md`

## Evidence
Live research checked Microsoft Support's current `#REF!` guidance, which frames the error as a formula pointing to an invalid cell reference, commonly after referenced rows or columns are deleted. Microsoft's broken-formula guidance also lists `#REF!` among common Excel formula errors. Current search results show ongoing troubleshooting demand around fixing `#REF!` after deleted rows, moved cells, lookup/reference arguments, and copied formulas.

Sources:
- https://support.microsoft.com/en-gb/office/how-to-correct-a-ref-error-822c8e46-e610-4d02-bf29-ec4b8c5ff4be
- https://support.microsoft.com/en-us/office/how-to-avoid-broken-formulas-in-excel-8309381d-33e8-42f6-b889-84ef6df1d586
- https://excelchamps.com/formulas/ref-error/

## Changes
- Added `excel-ref-error` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-ref-error/index.html`.
- Regenerated existing static SEO pages and `sitemap.xml`.
- Linked the new page from the homepage Common formulas section.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.

## Verification
- `npm run build:seo && npm test` passed `45/45`.
- Public-copy scan passed for the new page and homepage.
- Local route, homepage, and sitemap returned HTTP `200`.
- Local desktop and mobile Playwright screenshots captured with `0` console errors.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage links `/excel-ref-error/`.
- Live sitemap includes `https://writemyformula.com/excel-ref-error/`.
- Live desktop and mobile Playwright screenshots captured with `0` console errors.
- Vercel deployment `dpl_5UCG3D1fXBrnqxeY4W5RH1Xq5gjf` is `Ready` and aliased to `https://writemyformula.com`.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Boundaries
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or new cash spend occurred. Browser verification may have exercised the live formula UI, but no new purchase or cash budget change occurred. Final copy avoids file upload, workbook audit, guarantee, refund, PDF, same-day, human-reviewer, official-affiliation, unlimited-fix, and pay-before-answer claims.

## Budget
Cash spend: `$0`. Current cash balance remains `$35.93`.
