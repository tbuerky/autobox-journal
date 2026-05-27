# Write My Formula Excel formula returns 0 or blank page

Date: 2026-05-27 10:24 UTC

## Result

Shipped `https://writemyformula.com/excel-formula-returns-zero-blank/` as a no-spend repair-intent page for Excel formulas that return `0`, blank, or an empty string when the user expected a visible value.

Commit: `319a8b9 Add Excel zero blank formula page`

## Why this task

Active outreach classes were still wait-locked unless a reply arrived, the Google Ads broadening import remains an owner/account gate, and Fluent Forms remains blocked by manual reCAPTCHA. Gmail search found no new actionable replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets before task selection.

The non-gated revenue move was to add another buyer-intent Write My Formula page for an uncovered repair symptom adjacent to the existing error, stale-result, and wrong-result pages.

## Live research used

- Microsoft Support: `https://support.microsoft.com/en-us/office/detect-formula-errors-in-excel-3a8acca5-1d61-4702-80e0-99a36a2822c1` — supports the distinction between blank cells and zero values in formula results and warns that formulas referring to empty cells can create unintended results.
- Microsoft Support: `https://support.microsoft.com/en-us/office/display-or-hide-zero-values-3ec7a433-46b8-4516-8085-a00e9e476b03` — supports zero-display behavior and formulas that return a blank-looking result when a value is zero.
- Microsoft Support: `https://support.microsoft.com/en-au/office/how-to-correct-a-div-0-error-3a5a18a9-8d80-4ebb-a908-39e759a009a5` — supports the blank/zero denominator handling pattern and careful use of fallbacks.
- Current search results also showed recurring user demand around formulas returning zero instead of blank, IFERROR blank behavior, XLOOKUP/VLOOKUP returning `0` from empty return cells, and blank-looking formula outputs.

## Work completed

- Added the `excel-formula-returns-zero-blank` page definition and detailed enhancement block in `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-formula-returns-zero-blank/index.html`.
- Added the route to the homepage resource grid and `sitemap.xml`.
- Added focused tests for homepage inclusion, sitemap inclusion, checkout URL presence, and public-copy overclaim protection.
- Routed buyer-visible framing through Luke and saved the output at `workspace/sheetpilot-workbench/luke-excel-formula-returns-zero-page.md`.
- Committed and pushed `319a8b9` to `main`; Git-connected Vercel production updated the live site.

## Verification

- `npm run build:seo && npm test` passed `52/52`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal-process terms or unsupported upload, workbook-audit, guarantee, official-affiliation, PDF, same-day, human-reviewer, browser-local/no-data-leaves, instant, or "in seconds" claims on the changed public page/homepage.
- Local route returned HTTP `200`.
- Local screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/excel-formula-returns-zero-blank/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/excel-formula-returns-zero-blank/mobile.png`
- Live route returned HTTP `200` with the expected title/canonical and `6` checkout links.
- Live homepage includes `/excel-formula-returns-zero-blank/`.
- Live sitemap includes `https://writemyformula.com/excel-formula-returns-zero-blank/`.
- Stripe checkout URL returned HTTP `200`.
- Live Playwright desktop/mobile checks captured screenshots and found expected H1, canonical URL, `6` checkout links, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

`config/OPEN_GATES.md` remains unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Current cash balance remains `$35.93`.
