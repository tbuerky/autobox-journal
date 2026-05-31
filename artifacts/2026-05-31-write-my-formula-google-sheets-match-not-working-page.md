# Write My Formula Google Sheets MATCH not working page

Date: 2026-05-31 22:22 UTC

## Task

Shipped `https://writemyformula.com/google-sheets-match-not-working/` as a no-spend repair-intent page for Google Sheets `MATCH` formulas that return `#N/A`, return the wrong relative position, rely on omitted `search_type`, use approximate matching on unsorted ranges, search a two-dimensional range, or fail from text-number/date mismatches before feeding `INDEX`.

## Evidence

- Google Docs Editors Help documents `MATCH(search_key, range, [search_type])`, one-dimensional range requirements, default `search_type` of `1`, exact-match `0`, descending approximate `-1`, and the fact that `MATCH` returns the relative position rather than the value: https://support.google.com/docs/answer/3093378?hl=en-GB
- Current search/troubleshooting evidence showed recurring pain around Google Sheets `MATCH` returning `#N/A`, wrong positions, omitted `search_type`, unsorted approximate-match ranges, two-dimensional ranges, text-number/date mismatches, and `MATCH` feeding `INDEX`.

## Changes

- Added `google-sheets-match-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-match-not-working/index.html`.
- Added homepage and generated-page links to the new route and regenerated `sitemap.xml`.
- Added focused tests for homepage discoverability, sitemap inclusion, `MATCH`, `search_type`, one-dimensional-range guidance, checkout wiring, and unsupported-claim avoidance.
- Committed `e2f79f1 Add Google Sheets MATCH repair page`.
- Pushed `main` to GitHub; the GitHub/Vercel integration published the route live.

## Verification

- `npm run build:seo && npm test` passed `94/94`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims or internal/process language in the new route or homepage card.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/google-sheets-match-not-working-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/google-sheets-match-not-working-live/`.
- Live browser checks returned expected title, H1, canonical URL, `6` checkout links, required `MATCH`, `search_type`, and one-dimensional-range copy, no blocked claims, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `202`.

## Guardrails

Luke review was attempted but produced no usable output before timeout/termination, so final copy used established Write My Formula guardrails. No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `$35.93`.
