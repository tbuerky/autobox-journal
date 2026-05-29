# Write My Formula Google Sheets XLOOKUP not working page - 2026-05-29

## Task
Ship one no-spend repair-intent page for Google Sheets users searching for XLOOKUP formulas that return `#N/A`, return the wrong row, hide the issue behind a blank fallback, mismatch lookup/result ranges, use the wrong duplicate search direction, or use binary search on unsorted data.

Live page: https://writemyformula.com/google-sheets-xlookup-not-working/

## Evidence
- Google Docs Editors Help documents `XLOOKUP(search_key, lookup_range, result_range, missing_value, match_mode, search_mode)`, default `#N/A` missing value behavior, default exact match, match modes `0`, `1`, `-1`, and `2`, search modes `1`, `-1`, `2`, and `-2`, and the requirement that binary search modes use sorted ranges: https://support.google.com/docs/answer/12405947?hl=en
- Current search results show active troubleshooting demand around Google Sheets XLOOKUP `#N/A`, wrong results, text/number mismatches, duplicate first/last match behavior, lookup/return range alignment, and binary-search sorting.
- Luke reviewed the buyer-facing copy direction. Final copy used the sharper "paste the XLOOKUP you wrote" framing but rejected over-strong "working version" phrasing and avoided unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## Changes
- Added `google-sheets-xlookup-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-xlookup-not-working/index.html`.
- Linked the route from the homepage and all generated page grids.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `2610254 Add Google Sheets XLOOKUP repair page` to `main`.

## Verification
- `npm run build:seo && npm test` passed `70/70`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan passed for the changed page/homepage. The only scan hit was the site's existing "data validation" page-link wording, not a forbidden claim.
- Live HTTP checks:
  - `https://writemyformula.com/google-sheets-xlookup-not-working/` -> `200`
  - `https://writemyformula.com/` -> `200`
  - `https://writemyformula.com/sitemap.xml` -> `200`
  - `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208` -> `200`
- Live homepage includes `/google-sheets-xlookup-not-working/`.
- Live sitemap includes `https://writemyformula.com/google-sheets-xlookup-not-working/`.
- Playwright Firefox desktop/mobile checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/google-sheets-xlookup-not-working/`; both returned HTTP `200`, expected title/H1/canonical, `6` checkout links, required XLOOKUP argument, binary-search, and duplicate-search copy, and `0` console/page errors.

## IndexNow
Submitted page, homepage, and sitemap to `https://api.indexnow.org/indexnow`.

Result: not completed. The API returned `502`, then `502`, then the final retry timed out after 30 seconds.

## Gates and Spend
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
