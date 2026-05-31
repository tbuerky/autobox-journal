# Write My Formula Excel MATCH not working page

Date: 2026-05-31 18:28 UTC

## Task

Shipped a no-spend repair-intent page for Excel `MATCH` formulas that return `#N/A`, return the wrong position, depend on omitted `match_type`, break because sorted lookup-array assumptions are wrong, or fail from stored text/number/date mismatches before feeding `INDEX MATCH`.

Live URL: https://writemyformula.com/excel-match-not-working/

## Evidence

- Microsoft Support documents `MATCH(lookup_value, lookup_array, match_type)`, exact match with `0`, default/omitted `match_type` behavior as `1`, the ascending sort requirement for `1`, the descending sort requirement for `-1`, and text matching not being case-sensitive: https://support.microsoft.com/en-gb/office/match-function-e8dffd45-c762-47d6-bf89-533f4a37673a
- Microsoft Support documents that `MATCH` returns `#N/A` when it cannot find the lookup value and calls out inconsistency between match type and sorting order as an `INDEX`/`MATCH` failure cause: https://support.microsoft.com/en-us/office/how-to-correct-a-n-a-error-in-index-match-functions-f91874c9-d30b-4b7a-8a6b-c622764a1992
- Current troubleshooting evidence showed recurring pain around `MATCH` `#N/A`, omitted exact-match arguments, wrong approximate-match results, sorted-data assumptions, hidden spaces, text-number mismatches, and `MATCH` propagating a bad row/column position into `INDEX`.

## Changes

- Added `excel-match-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-match-not-working/index.html`.
- Added homepage and generated-page links to the new route and regenerated `sitemap.xml`.
- Added focused tests for homepage discoverability, sitemap inclusion, `MATCH` / `match_type` copy, checkout wiring, and unsupported-claim avoidance.
- Committed `53e55b3 Add Excel MATCH repair page`.
- Pushed `main` to GitHub. The Vercel CLI manual deploy failed because the local `.vercel` link could not retrieve project settings, but the GitHub production integration served the new route live at `writemyformula.com`.

## Verification

- `npm run build:seo && npm test` passed `92/92`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims or internal/process language in the new route or homepage card.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-match-not-working-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-match-not-working-live/`.
- Live browser checks returned expected title, H1, canonical URL, `6` checkout links, required `match_type` and sorted-lookup copy, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `$35.93`.
