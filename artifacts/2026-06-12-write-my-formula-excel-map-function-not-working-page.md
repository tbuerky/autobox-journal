# Write My Formula Excel MAP Function Not Working Page - 2026-06-12

## Outcome
Shipped `https://writemyformula.com/excel-map-function-not-working/` as a no-spend repair-intent page for Excel users whose `MAP` formula returns `#VALUE!` / Incorrect Parameters, `#CALC!`, `#SPILL!`, `#NAME?`, a wrong transformed array, or a LAMBDA parameter mismatch.

## Why this task
Current owner direction prioritized active business motions with minimal human involvement. The paid-search control action remains owner-gated, Fluent Forms remains blocked by manual reCAPTCHA, and Write My Formula outreach categories remain on cooldown until 2026-06-14 unless a relevant prospect replies. A new buyer-intent repair page creates another public sales surface without spend.

## Evidence
- Microsoft’s current MAP support page says MAP maps each value in arrays to a new value using a LAMBDA, requires the LAMBDA as the last argument, and returns `#VALUE!` / Incorrect Parameters for invalid LAMBDA functions or incorrect parameter counts.
- Microsoft’s current LAMBDA support page confirms related `#VALUE!`, `#NUM!`, and `#CALC!` behavior for parameter count, recursion, and uncalled LAMBDA patterns.
- Current search/forum evidence shows users encountering MAP `#VALUE!`, nested-array / `#CALC!`, localization/version, and LAMBDA helper confusion.
- Luke reviewed copy-risk and flagged the main risk as implying whole-workbook diagnosis; final copy stays scoped to one pasted visible formula.

## Changed
- Added `excel-map-function-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/excel-map-function-not-working/index.html`.
- Regenerated generated static pages and `sitemap.xml`.
- Added focused coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved local Playwright screenshots under `workspace/sheetpilot-workbench/output/playwright/excel-map-function-not-working-local/` and `workspace/sheetpilot-workbench/output/playwright/excel-map-function-not-working-live/`.
- Committed and pushed nested app commit `a8b1c114 Add Excel MAP repair page`.

## Public copy boundaries
Final copy avoids Google Sheets MAP claims, upload/workbook-audit claims, guarantees, Microsoft affiliation/partner language, human-review/same-day/PDF claims, instant/one-click/automatic-fix claims, exact-cause claims, whole-workbook/spreadsheet claims, handles-any-size claims, works-in-every-version claims, and payment-before-answer claims.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `176/176`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Local desktop/mobile Chromium checks passed with expected static-server `POST 501` analytics/API noise only, no page errors, no horizontal overflow, correct title/H1/canonical, six checkout links, expected MAP copy, and no banned copy.
- Production route, homepage, sitemap, and live Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks passed with `0` console messages, `0` page errors, no horizontal overflow, correct title/H1/canonical, six checkout links, expected MAP copy, and homepage card present.
- IndexNow accepted route/home/sitemap submission with HTTP `200`.

## Gates and budget
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`. Open gates remain unchanged.
