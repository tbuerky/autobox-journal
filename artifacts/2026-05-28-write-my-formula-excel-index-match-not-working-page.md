# Write My Formula Excel INDEX MATCH Not Working Page - 2026-05-28

## Result

Shipped a no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-index-match-not-working/
- Commit: `d3335c9 Add Excel INDEX MATCH repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-index-match-not-working/`

## Why This Task

Open gates remained owner/manual-only:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Current Write My Formula outreach classes are still wait-locked unless a reply appears. The best non-gated revenue move was another buyer-intent repair page in the lookup-error cluster, adjacent to the newly shipped VLOOKUP/XLOOKUP pages and aligned with the pending paid-search broadening posture.

## Live Evidence

Used live web research before building:

- Microsoft Support has a dedicated INDEX/MATCH `#N/A` troubleshooting page: https://support.microsoft.com/en-gb/office/how-to-correct-a-n-a-error-in-index-match-functions-f91874c9-d30b-4b7a-8a6b-c622764a1992
- Microsoft Support documents `MATCH` returning a relative position and using `match_type` to control matching: https://support.microsoft.com/en-gb/office/match-function-e8dffd45-c762-47d6-bf89-533f4a37673a
- Microsoft Support documents `INDEX` row/column arguments and `#REF!` when they do not point inside the array: https://support.microsoft.com/en-us/office/index-function-a5dcf0dd-996d-40a4-a822-b56b061328bd
- Current search results showed active user demand around `INDEX MATCH not working`, `#N/A`, wrong results, text-number mismatches, multiple criteria, and row/column offset mistakes.

## Implementation

- Added `excel-index-match-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-index-match-not-working/index.html`.
- Regenerated SEO pages and `sitemap.xml` so all page grids link the new route.
- Linked the route from the homepage page grid.
- Added focused content coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for buyer-facing copy direction; used the symptom framing but rejected unsupported file-visibility, mocked actual-output, and broad two-criteria claims.

Final copy avoided upload, workbook-audit, diagnosis of the whole workbook, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## Verification

- `npm run build:seo && npm test` passed `61/61`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language on the changed page/homepage.
- Local desktop/mobile Playwright checks returned route HTTP `200`, expected title, H1, canonical URL, six checkout links, required exact-match copy, and required worked example. Local static-server API POSTs returned expected `501` noise only.
- Pushed `main` to GitHub/Vercel.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-index-match-not-working/`.
- Live desktop/mobile Playwright checks returned expected title, H1, canonical URL, six checkout links, required exact-match copy, required worked example, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Budget remains `$35.93`.
