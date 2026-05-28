# Write My Formula Google Sheets IMPORTRANGE not working page - 2026-05-28

## Task
Ship one no-spend repair-intent page for Google Sheets `IMPORTRANGE` formulas that fail with `#REF!`, `Allow access` prompts, source permission issues, oversized imports, slow refreshes, or volatile source-formula problems.

## Result
- Live page: https://writemyformula.com/google-sheets-importrange-not-working/
- Commit: `9be4656 Add Google Sheets IMPORTRANGE repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-importrange-not-working/`

## Evidence
- Google Docs Editors Help documents `IMPORTRANGE(spreadsheet_url, range_string)`, quoted URL/range requirements, the first-use `Allow access` grant, non-owner source access requirements, the 600-user share-limit implication, the external-data/performance model, a 10 MB received-data cap per request, hourly refresh behavior while open, throttling from churn, and restrictions around `NOW`, `RAND`, and `RANDBETWEEN`: https://support.google.com/docs/answer/3093340
- Current troubleshooting evidence showed visible demand around `IMPORTRANGE` `#REF!`, internal error, `Result too large`, slow import, and source-access problems, including Stack Overflow and Reddit results.
- Luke reviewed the buyer-facing direction and recommended symptom-led framing. Final copy used the symptom router but softened unsupported "tell you exactly" / "so it works" claims and avoided upload, workbook-audit, official-affiliation, guarantee, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## What changed
- Added `google-sheets-importrange-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-importrange-not-working/index.html`.
- Linked the route from the homepage and regenerated all static SEO pages so their embedded route grid includes the new page.
- Added sitemap coverage and focused content tests.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `67/67`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no forbidden claims on the changed public page/homepage; matches in test/generator files were negative assertions or existing comparison copy.
- Local Firefox screenshots captured for desktop and mobile; local static-server console noise was expected `501` POST handling from the simple file server.
- Pushed `main` to GitHub/Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-importrange-not-working/`.
- Live Firefox desktop/mobile checks returned expected title, H1, canonical, `6` checkout links, required `Allow access`, result-size, and volatile-function copy, with `0` console/page issues.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Gates and budget
- `config/OPEN_GATES.md` remains unchanged: `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` and `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`.
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.
- Current cash balance remains `$35.93`.
