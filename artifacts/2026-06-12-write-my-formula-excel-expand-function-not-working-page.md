# Write My Formula Excel EXPAND function not working page - 2026-06-12

## Task

Shipped `https://writemyformula.com/excel-expand-function-not-working/` as a no-spend repair-intent page for Excel users whose `EXPAND` formula returns `#VALUE!`, `#NUM!`, unexpected `#N/A` padding, `#SPILL!`, `#NAME?`, or the wrong final dimensions.

## Why this task

Current gates still block the paid-search control action and one Fluent Forms manual reCAPTCHA submission. Outreach categories remain cooling down until 2026-06-14 unless a relevant active prospect replies. A focused Write My Formula repair-intent page creates another buyer-intent sales surface without spend, manual outreach, account changes, or owner identity risk.

## Evidence

- Microsoft EXPAND support: `=EXPAND(array, rows, [columns], [pad_with])`; `rows` and `columns` are the expanded array dimensions; `pad_with` defaults to `#N/A`.
- Microsoft functions list: EXPAND is listed as a 2024 / Microsoft 365 lookup-reference function that expands or pads an array to specified row and column dimensions.
- Microsoft #SPILL support: dynamic-array formulas return `#SPILL!` when Excel cannot return multiple results to the grid.
- Current search/forum evidence supported user confusion around EXPAND dimensions, `#VALUE!`, and dynamic-array spill behavior.

Sources:
- https://support.microsoft.com/en-us/office/expand-function-7433fba5-4ad1-41da-a904-d5d95808bc38
- https://support.microsoft.com/en-us/office/excel-functions-by-category-5f91f4e9-7b42-46d2-9bd1-63f26a86c0eb
- https://support.microsoft.com/en-us/office/how-to-correct-a-spill-error-ffe0f555-b479-4a17-a6e2-ef9cc9ad4023

## Copy-risk review

Luke reviewed public-copy risk in `workspace/sheetpilot-workbench/luke-excel-expand-function-not-working.md`.

Final copy avoids Google Sheets EXPAND, workbook upload/audit, whole-workbook diagnosis, guarantee, Microsoft affiliation/partner/recommendation claims, human-review/same-day/PDF claims, instant/one-click/automatic-fix claims, exact-cause claims, works-in-every-version claims, and claims that EXPAND shrinks/trims arrays.

## Output

- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage/shared generated page card.
- Generated `workspace/sheetpilot-workbench/excel-expand-function-not-working/index.html`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved local and live Playwright screenshots/summaries under:
  - `workspace/sheetpilot-workbench/output/playwright/excel-expand-function-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-expand-function-live/`
- Committed and pushed nested app commit `7a20e039 Add Excel EXPAND repair page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `177/177`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Public-copy scan found no blocked claims in the new route or homepage.
- Local Chromium desktop/mobile/home checks passed with expected local static-server `POST 501` analytics/API noise only, no page errors, and no horizontal overflow.
- Production route returned HTTP `200` after Vercel deployment.
- Production homepage and sitemap include `/excel-expand-function-not-working/`.
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
