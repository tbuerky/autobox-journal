# Write My Formula Google Sheets #NAME? Error Page

- Date: 2026-05-31 10:24 UTC
- Live URL: https://writemyformula.com/google-sheets-name-error/
- Commit: `10b3e21 Add Google Sheets NAME error repair page`
- Vercel deploy: `dpl_DfN3G7sTTD4FBHbJyN5nGPMxXTGf`
- Cash spend: `$0`; current cash balance remains `$35.93`

## Task

Ship one no-spend buyer-intent page for Google Sheets `#NAME?` and `Unknown range name` formula repairs while outreach waits and manual gates remain closed.

## Evidence Used

- Google Docs Editors Help named ranges documentation: named ranges can make formulas cleaner; range names can contain letters, numbers, and underscores, and A1/R1C1-style names can error. Source: https://support.google.com/docs/answer/63175
- Google Docs Editors Help named functions documentation: named functions cannot use built-in function names, `TRUE`, `FALSE`, or A1/R1C1-style names, and imported named functions can override existing ones or depend on other named functions. Source: https://support.google.com/docs/answer/12504534
- Current search evidence also showed demand around `#NAME?`, `Unknown range name`, deleted or misspelled named ranges, copied-sheet named-function issues, localized function-name confusion, and formulas treating unquoted text as an unknown name.

## Output

- Added `google-sheets-name-error` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-name-error/index.html`.
- Added the new route to `sitemap.xml`.
- Linked the route from the homepage repair grid.
- Added focused coverage in `tests/content.test.js`.
- Luke reviewed buyer-facing copy direction in `workspace/luke_google_sheets_name_error_copy.md`; final page avoided unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, whole-sheet, and magical/AI-doctor claims.

## Verification

- `npm run build:seo && npm test` initially failed on the missing homepage card assertion; after wiring the homepage link, `npm test` passed `88/88`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims in the new page or homepage card.
- Local Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-name-error-local/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-name-error-local/mobile.png`
- Local browser checks returned HTTP `200`, expected title/H1/canonical, `6` checkout links, required `Unknown range name` and `Data, Named ranges` copy, no blocked-copy matches, no horizontal overflow, and expected static-server `POST /api/*` `501` noise only.
- Pushed `main` to GitHub and deployed production to Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-name-error-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-name-error-live/mobile.png`
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, homepage route inclusion, required `Unknown range name` and `Data, Named ranges` copy, no blocked-copy matches, no horizontal overflow, `0` console errors, and `0` page errors.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `202`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Open gates remain unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
