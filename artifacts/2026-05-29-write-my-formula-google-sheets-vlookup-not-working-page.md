# Write My Formula Google Sheets VLOOKUP not working page - 2026-05-29

## Task
Ship one no-spend repair-intent page for Google Sheets `VLOOKUP` formulas that return `#N/A`, pull the wrong row, use approximate match unintentionally, search the wrong range, return the wrong column, or mismatch text and numeric lookup values.

## Result
- Live page: https://writemyformula.com/google-sheets-vlookup-not-working/
- Commit: `ea24267 Add Google Sheets VLOOKUP repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-vlookup-not-working/`

## Evidence
- Google Docs Editors Help documents `VLOOKUP(search_key, range, index, [is_sorted])`, first-column lookup behavior, exact-match `#N/A` when no match exists, approximate-match `is_sorted=TRUE`, wrong values when approximate-match data is not sorted ascending, and `#N/A` when the approximate-match key is smaller than the first-column minimum: https://support.google.com/docs/answer/3093318
- Current search evidence showed active repair demand around Google Sheets `VLOOKUP` `#N/A`, wrong returned values, omitted fourth argument / approximate match, unsorted lookup columns, wrong lookup range, wrong return index, and text-vs-number mismatches, including current troubleshooting pages and Reddit/Stack Overflow-style help threads.
- Luke reviewed copy direction. Final copy used the exact-match / sorted-range / first-column / return-index framing but avoided unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## What changed
- Added `google-sheets-vlookup-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-vlookup-not-working/index.html`.
- Linked the route from the homepage and regenerated all static SEO pages so their embedded route grid includes the new page.
- Added sitemap coverage and a focused content test.

## Verification
- `npm run build:seo && npm test` passed `69/69`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no forbidden claims on the changed public page/homepage.
- Local desktop/mobile Playwright screenshots and checks passed.
- Pushed `ea24267` to GitHub/Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-vlookup-not-working/`.
- Live desktop/mobile Playwright checks returned expected title, H1, canonical URL, `6` checkout links, required sorted-range and return-index copy, and `0` console errors.
- IndexNow submission for the new page, homepage, and sitemap did not complete: first call returned HTTP `503`; retries returned timeout/`502`/timeout. The page is live and sitemap-linked, so retrying IndexNow is a next-run optional freshness task, not a launch blocker.

## Gates and budget
- `config/OPEN_GATES.md` remains unchanged: `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` and `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`.
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.
- Current cash balance remains `$35.93`.
