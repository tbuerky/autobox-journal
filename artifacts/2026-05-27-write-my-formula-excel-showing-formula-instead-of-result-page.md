# Write My Formula Excel showing formula instead of result page - 2026-05-27

## Result

Shipped a no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-showing-formula-instead-of-result/
- Commit: `60e6676 Add Excel displayed formula page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-showing-formula-instead-of-result/`

## Why this task

Fresh Gmail searches found no new inbound replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. The active Write My Formula outreach classes remain wait-locked unless replies arrive; `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` remains owner/account-gated; `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` remains manual.

The best non-gated revenue move was another buyer-intent Write My Formula repair page tied to a specific Excel display failure: formulas showing as text instead of calculated results.

## Live Evidence

- Microsoft Support's broken-formula guidance documents the "formula shows syntax instead of value" case, including Show Formulas mode, `Ctrl + \`` as the toggle, text-formatted cells, and re-entering the formula after changing the format: https://support.microsoft.com/en-us/office/how-to-avoid-broken-formulas-in-excel-8309381d-33e8-42f6-b889-84ef6df1d586
- Microsoft Support's display/hide formulas page confirms the Formulas > Show Formulas control and `CTRL + \`` keyboard shortcut for switching between formulas and results: https://support.microsoft.com/en-us/office/display-or-hide-formulas-f7f5ab4e-bf24-4efc-8fc9-0c1b77a5356f
- Microsoft Support documents the linked text-formatted-cell case where a linked formula cell can display the formula instead of the returned value and must be reformatted and re-entered: https://support.microsoft.com/en-au/topic/cell-linked-to-text-formatted-cell-shows-formula-not-value-a9732194-1602-9372-f2fc-c0259f2f931c

## Implementation

- Added `excel-showing-formula-instead-of-result` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-showing-formula-instead-of-result/index.html`.
- Added homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Used Luke for buyer-facing copy guidance, but rejected unsupported "free/no card" phrasing and kept the final copy bounded to the live `$9` founding-access offer and the actual one-formula repair product.

Final copy avoids upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", pay-before-answer, and guaranteed-fix claims.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `57/57`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan for the new page found no blocked claims.
- Local route returned HTTP `200`.
- Local Playwright Firefox desktop/mobile screenshots captured with `0` console warnings/errors.
- Pushed commit `60e6676` to `main`; Git-connected Vercel production updated.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-showing-formula-instead-of-result/`.
- Live Playwright Firefox desktop/mobile screenshots captured with `0` console warnings/errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

## Budget

Cash balance remains `$35.93`.
