# Write My Formula Excel CHOOSECOLS / CHOOSEROWS Repair Page

## Task

Ship one no-spend buyer-intent repair page for Excel `CHOOSECOLS` and `CHOOSEROWS` formulas, without changing ads, payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, public posts, bulk sends, destructive production settings, or spend.

## Evidence

- Microsoft Support documents `CHOOSECOLS` as returning specified columns from an array and says Excel returns `#VALUE!` when any `col_num` absolute value is `0` or exceeds the number of columns in the array.
- Microsoft Support documents `CHOOSEROWS` with the same row-position constraint: `#VALUE!` when any `row_num` absolute value is `0` or exceeds the number of rows in the array.
- Current troubleshooting evidence showed demand around `CHOOSECOLS` and `CHOOSEROWS` returning `#VALUE!`, `#NAME?`, wrong selected columns or rows, structured references used where positional numbers are required, blocked spill output, and errors propagated from nested `FILTER`, `INDEX`, or `SORT` formulas.

Sources:

- Microsoft `CHOOSECOLS` function: `https://support.microsoft.com/en-us/office/choosecols-function-bf117976-2722-4466-9b9a-1c01ed9aebff`
- Microsoft `CHOOSEROWS` function: `https://support.microsoft.com/en-gb/office/chooserows-function-51ace882-9bab-4a44-9625-7274ef7507a3`
- Current indexed troubleshooting evidence included ExcelForum and Reddit examples around `FILTER` + `CHOOSECOLS`, structured-reference `#VALUE!` cases, `CHOOSEROWS` not appearing in unsupported versions, and nested dynamic-array failures.

## Output

- Added `excel-choosecols-chooserows-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-choosecols-chooserows-not-working/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live desktop/mobile screenshots under ignored verification folders:
  - `workspace/sheetpilot-workbench/output/playwright/excel-choosecols-chooserows-not-working-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-choosecols-chooserows-not-working-live/`
- Committed and pushed `d9160ee Add Excel CHOOSECOLS CHOOSEROWS repair page`.
- Live page: `https://writemyformula.com/excel-choosecols-chooserows-not-working/`

## Verification

- `npm run build:seo && npm test` passed `107/107`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language in the new route or homepage card.
- Luke reviewed buyer-facing copy direction; final copy avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click/automatic-fix, pay-before-answer, PDF, same-day, whole-workbook, whole-spreadsheet, exact-cause, any-Excel-version, and unsupported traction claims.
- Local desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `CHOOSECOLS` / `CHOOSEROWS` / `#VALUE!` / `Microsoft 365` / `Excel 2024` / `array argument` copy, homepage card text, sitemap inclusion, Stripe checkout HTTP `200`, and no horizontal overflow. Local static-server `POST /api/*` `501` console noise was expected.
- Production route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required copy, homepage card text, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
