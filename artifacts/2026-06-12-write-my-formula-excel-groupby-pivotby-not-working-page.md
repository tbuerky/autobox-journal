# Write My Formula Excel GROUPBY / PIVOTBY not working page - 2026-06-12

## Task

Shipped `https://writemyformula.com/excel-groupby-pivotby-not-working/` as a no-spend repair-intent page for Excel users whose `GROUPBY` or `PIVOTBY` formula returns `#VALUE!`, `#CALC!`, `#SPILL!`, `#NAME?`, wrong headers, wrong totals, sort issues, filter-array shape problems, or the wrong summary grid.

## Why this task

Paid-search control and the Fluent Forms manual reCAPTCHA remain owner-gated, while outreach categories are cooling down until 2026-06-14 unless a relevant prospect replies. A focused repair page creates another buyer-intent sales surface without spend, outreach, ad changes, account changes, or owner identity risk.

## Evidence

- Microsoft GROUPBY support says GROUPBY creates a formula summary by grouping along one axis and aggregating values, with syntax `GROUPBY(row_fields, values, function, ...)`.
- Microsoft GROUPBY docs specify column-oriented `row_fields` and `values`, aggregator functions such as `SUM`, `PERCENTOF`, `AVERAGE`, and `COUNT`, and a `filter_array` whose length must match `row_fields`.
- Microsoft PIVOTBY support says PIVOTBY creates a formula summary by grouping row and column fields, is not directly related to PivotTable, and uses syntax `PIVOTBY(row_fields, col_fields, values, function, ...)`.
- Microsoft PIVOTBY docs specify column-oriented row/column fields and values, aggregator functions, field headers, row/column total depth, sort order, filter arrays, and `relative_to` behavior for two-argument aggregations.
- Search results showed active user confusion around GROUPBY/PIVOTBY availability, aggregator behavior, and PivotTable alternatives.

Sources:
- https://support.microsoft.com/en-US/Excel/groupby-function
- https://support.microsoft.com/en-US/Excel/pivotby-function
- https://support.microsoft.com/en-US/Excel/excel-functions-by-category

## Copy-risk review

Luke reviewed public-copy risk in `workspace/sheetpilot-workbench/luke-excel-groupby-pivotby-not-working.md`. Final copy avoids Google Sheets GROUPBY/PIVOTBY, upload/workbook-audit claims, spreadsheet diagnosis claims, guarantees, Microsoft affiliation/partner/recommendation claims, human-review/same-day/PDF claims, instant/one-click/automatic-fix claims, exact-cause claims, works-in-every-version claims, PivotTable-replacement claims, and fully-supported lambda claims.

## Output

- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage/shared generated page card.
- Generated `workspace/sheetpilot-workbench/excel-groupby-pivotby-not-working/index.html`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved local and live Playwright screenshots/summaries under:
  - `workspace/sheetpilot-workbench/output/playwright/excel-groupby-pivotby-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-groupby-pivotby-live/`
- Committed and pushed nested app commit `175b7014 Add Excel GROUPBY PIVOTBY repair page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `178/178`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Public-copy scan found no blocked claims in the new route or homepage.
- Local Chromium desktop/mobile/home checks passed with expected local static-server `POST 501` analytics/API noise only, no page errors, and no horizontal overflow.
- Production route returned HTTP `200` after Vercel deployment.
- Production homepage and sitemap include `/excel-groupby-pivotby-not-working/`.
- Actual Stripe checkout URL returned HTTP `200`.
- Live Chromium desktop/mobile/home checks returned expected title/H1/canonical, six checkout links, homepage link present, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Gates and budget

`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

`config/BUDGET.md` remains unchanged. Current cash balance remains `-$24.07`.
