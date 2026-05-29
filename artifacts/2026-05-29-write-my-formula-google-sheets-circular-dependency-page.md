# Write My Formula Google Sheets circular dependency page - 2026-05-29

## Task
Shipped `https://writemyformula.com/google-sheets-circular-dependency/` as a no-spend repair-intent page for Google Sheets formulas that show "Circular dependency detected" because of direct self-references, self-including ranges, helper-cell loops, or misuse of iterative calculation.

## Why this task
Current Write My Formula outreach waits still constrained manual selling: training/resource until `2026-06-01 10:20 UTC`, consulting/support-service until `2026-06-01 16:20 UTC`, add-in vendor until `2026-05-30 22:20 UTC`, and marketplace/app-template while the Someka link-exchange wait is active. The Google Ads broadening import remains owner/account-gated and the Fluent Forms contact path remains blocked by manual reCAPTCHA. The best non-gated revenue move was another buyer-intent repair page tied to the existing `$9` Write My Formula checkout.

## Live research used
- Google support: "Set a spreadsheet's location & calculation settings" documents calculation settings, including iterative calculation as the setting that controls how many times a formula with a circular reference can occur: https://support.google.com/docs/answer/58515
- Google support: "Learn how to improve Sheets performance" documents that Sheets evaluates formulas and dependent cells after edits, supporting the dependency-chain framing: https://support.google.com/docs/answer/11468464
- Google Sheets API docs: `IterativeCalculationSettings` describes max iterations and convergence threshold for circular-dependency resolution: https://developers.google.com/resources/api-libraries/documentation/sheets/v4/csharp/latest/classGoogle_1_1Apis_1_1Sheets_1_1v4_1_1Data_1_1IterativeCalculationSettings.html
- Current troubleshooting-demand evidence showed active pages and discussions around "Circular dependency detected," self-referencing ranges, indirect loops, and the risk of enabling iterative calculation when the loop is accidental.

## Output
- Added `google-sheets-circular-dependency` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-circular-dependency/index.html`.
- Linked the route from the homepage page grid and regenerated existing SEO pages plus `sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Ran Luke review and stored it at `workspace/sheetpilot-workbench/luke-google-sheets-circular-dependency-page.md`.
- Committed and pushed `5f4a654 Add Google Sheets circular dependency page`.

## Verification
- `npm run build:seo && npm test` passed `75/75`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no upload, workbook-audit, guarantee, official-affiliation, same-day/PDF, human-reviewer, data-never-leaves, instant, one-click, automatic, or pay-before-answer claims in the changed public page/homepage.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/google-sheets-circular-dependency/`.
- Live Chromium desktop/mobile checks returned HTTP `200`, expected title, expected H1, canonical URL, `6` checkout links, and `0` console/page errors. Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-circular-dependency/desktop.png` and `workspace/sheetpilot-workbench/output/playwright/google-sheets-circular-dependency/mobile.png`.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and budget
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Open gates remain:
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Current cash balance remains `$35.93`.
