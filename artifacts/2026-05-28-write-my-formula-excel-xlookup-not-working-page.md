# Write My Formula Excel XLOOKUP not working page

Date: 2026-05-28 08:24 UTC

## Result

Shipped a new no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-xlookup-not-working/
- Commit: `6c5a20c Add Excel XLOOKUP repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-xlookup-not-working/`

The page targets broader "XLOOKUP not working" intent beyond the existing `xlookup-na-error` page: `#N/A`, wrong rows, blank-looking fallbacks, lookup/return array alignment, stored type mismatches, duplicate/search behavior, `match_mode`, `search_mode`, and Excel version support.

## Evidence

Live research checked:

- Microsoft Support XLOOKUP function documentation: https://support.microsoft.com/en-gb/office/xlookup-function-b7fd680e-6d10-43e6-84f9-88eae8bf5929
- Microsoft Q&A / Support confirmation that XLOOKUP is unavailable in Excel 2016 and Excel 2019: https://learn.microsoft.com/en-us/answers/questions/5182738/x-lookup-function-not-found-in-my-excel
- Current repair-demand evidence for "XLOOKUP not working" pages and forum/search results, including FormulaDesk's recent page: https://formuladesk.site/lookup/xlookup-not-working/

Microsoft's source supports the page's syntax and failure framing: XLOOKUP uses `lookup_value`, `lookup_array`, `return_array`, optional `if_not_found`, optional `match_mode`, and optional `search_mode`; a missing valid match without `if_not_found` returns `#N/A`; default match mode is exact; binary search modes require sorted arrays; and Excel 2016/2019 compatibility is a real issue. Third-party/search evidence showed active demand around hidden spaces, stored text/number mismatches, array-size mismatches, wrong results, fallback misuse, and unsupported versions.

## Implementation

- Added `excel-xlookup-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the generated static page under `workspace/sheetpilot-workbench/excel-xlookup-not-working/index.html`.
- Linked it from the homepage and therefore from the generated route grids.
- Regenerated `sitemap.xml`.
- Added regression tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Routed public-facing copy direction through Luke in `workspace/sheetpilot-workbench/luke-excel-xlookup-not-working-page.md`; used the repair-first framing, but softened unsupported "working one back" and INDEX/MATCH rewrite claims.

## Verification

- `npm run build:seo && npm test` passed `60/60`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", pay-before-answer, internal, experiment, or approval-gate language on the changed public page/homepage.
- Local desktop/mobile Playwright screenshots captured. Local browser check returned expected route title/H1/canonical/checkout links with only expected static-server `501` API POST noise.
- Pushed `6c5a20c` to GitHub `main`; Vercel production updated.
- Live route/home/sitemap/checkout checks returned HTTP `200`.
- Live homepage and sitemap include `/excel-xlookup-not-working/`.
- Live Playwright check returned expected title, H1, canonical URL, six checkout links, required binary-search copy, required worked example, and `0` console/page issues.
- Live desktop/mobile screenshots captured.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. The pre-existing uncommitted `workspace/sheetpilot-workbench/README.md` outreach-ledger changes were left untouched and uncommitted.

Budget remains `$35.93`.
