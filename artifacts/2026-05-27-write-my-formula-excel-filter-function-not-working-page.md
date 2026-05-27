# Write My Formula Excel FILTER function not working page - 2026-05-27

## Result

Shipped a no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-filter-function-not-working/
- Commit: `a9a535d Add Excel FILTER repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-filter-function-not-working/`

## Why this task

Fresh Gmail search found no new inbound replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. The active Write My Formula outreach classes remain wait-locked unless replies arrive; `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` remains owner/account-gated; `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` remains manual.

The best non-gated revenue move was another buyer-intent Write My Formula repair page tied to a known Excel formula failure cluster.

## Live Evidence

- Microsoft Support documents `FILTER(array, include, [if_empty])`, with `include` as a Boolean array matching the array height or width, the optional `if_empty` fallback, spill behavior, empty-result `#CALC!`, include-argument errors, linked-workbook `#REF!` behavior when source workbooks close, and AND/OR criteria examples using `*` and `+`: https://support.microsoft.com/en-gb/office/filter-function-f4f7cb66-82eb-4767-8f7c-4877ad80c759
- Microsoft Q&A has a current user question for `filter formula not working - excel` around a `#CALC! empty array` FILTER failure despite expected matching data, confirming live repair demand: https://learn.microsoft.com/en-us/answers/questions/e3cdde16-b898-4885-991d-7f4fd2c9f950/filter-formula-not-working-excel

## Implementation

- Added `excel-filter-function-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-filter-function-not-working/index.html`.
- Added homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Used Luke for buyer-facing copy guidance, then kept final copy bounded to one-formula repair and avoided unsupported "guaranteed working" language.

Final copy avoids upload, workbook-audit, guarantee, official-affiliation, PDF, same-day, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## Verification

- `npm run build:seo && npm test` initially found one too-strict test assertion; after correction, `npm test` passed `56/56`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan for the new page found no blocked claims.
- Local Playwright Firefox desktop/mobile screenshots captured with `0` console warnings/errors.
- Pushed commit `a9a535d` to `main`; Git-connected Vercel production updated.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-filter-function-not-working/`.
- Live Playwright Firefox desktop/mobile screenshots captured with `0` console warnings/errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

## Budget

Cash balance remains `$35.93`.
