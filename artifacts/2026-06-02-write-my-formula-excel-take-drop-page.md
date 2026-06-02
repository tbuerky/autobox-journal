# Write My Formula Excel TAKE / DROP Repair Page

## Task

Ship one no-spend buyer-intent repair page for Excel `TAKE` and `DROP` formulas, without changing ads, payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, public posts, bulk sends, destructive production settings, or spend.

## Evidence

- Microsoft Support documents `TAKE` as returning specified rows or columns from the start or end of an array; negative counts work from the end; `0` rows or columns returns `#CALC!`; an array that is too large returns `#NUM!`; and the function is supported in Microsoft 365, Excel for the web, and Excel 2024.
- Microsoft Support documents `DROP` as excluding specified rows or columns from the start or end of an array; negative counts work from the end; `0` rows or columns returns `#CALC!`; an array that is too large returns `#NUM!`; and the function is supported in Microsoft 365, Excel for the web, and Excel 2024.
- Current troubleshooting evidence showed users running into missing `TAKE` / `DROP` support (`#NAME?` / `_xlfn`), rollout/version confusion, formulas that pull or drop from the wrong end, `#SPILL!` blocked output, and nested `FILTER`, `SORT`, `CHOOSECOLS`, or `CHOOSEROWS` failures.

Sources:

- Microsoft `TAKE` function: `https://support.microsoft.com/en-us/office/take-function-25382ff1-5da1-4f78-ab43-f33bd2e4e003`
- Microsoft `DROP` function: `https://support.microsoft.com/en-us/office/drop-function-1cb4e151-9e17-4838-abe5-9ba48d8c6a34`
- Current indexed troubleshooting evidence included Microsoft Community Hub and Reddit examples around missing `TAKE` / `DROP` functions, Office version rollout confusion, and nested dynamic-array usage.

## Output

- Added `excel-take-drop-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-take-drop-not-working/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live desktop/mobile screenshots under ignored verification folders:
  - `workspace/sheetpilot-workbench/output/playwright/excel-take-drop-not-working-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-take-drop-not-working-live/`
- Committed and pushed `7ca6de3 Add Excel TAKE DROP repair page`.
- Live page: `https://writemyformula.com/excel-take-drop-not-working/`

## Verification

- `npm run build:seo && npm test` passed `108/108`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language in the new route or homepage card.
- Luke reviewed buyer-facing copy direction; final copy avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click/automatic-fix, pay-before-answer, PDF, same-day, whole-workbook, whole-spreadsheet, exact-cause, any-Excel-version, and unsupported traction claims.
- Local desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `TAKE` / `DROP` / `#CALC!` / `#NUM!` / `#SPILL!` / `Microsoft 365` / `Excel 2024` / positive-count / negative-count copy, homepage card text, sitemap inclusion, and no horizontal overflow. Local static-server `POST /api/*` `501` console noise was expected.
- Production route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required copy, homepage card text, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
