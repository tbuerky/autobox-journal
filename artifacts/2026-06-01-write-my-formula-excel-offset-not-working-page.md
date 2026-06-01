# Write My Formula Excel OFFSET not working page

## Result
Shipped `https://writemyformula.com/excel-offset-not-working/` as a no-spend repair-intent page for Excel `OFFSET` formulas that return `#REF!`, return `#VALUE!`, point at the wrong range, fail inside dynamic named ranges, use text where Excel needs a reference, or create volatile recalculation confusion.

## Evidence
- Live research used Microsoft Support `OFFSET` documentation: `OFFSET(reference, rows, cols, [height], [width])`; non-adjacent/invalid reference can return `#VALUE!`; offsets beyond worksheet edges return `#REF!`; omitted height/width inherit the starting reference size; height and width must be positive.
- Current troubleshooting evidence showed recurring demand around `OFFSET` `#REF!`, `#VALUE!`, string references needing another reference strategy, dynamic named ranges, deleted/moved references, off-by-one row/column shifts, and volatility/performance tradeoffs.
- Luke reviewed buyer-facing framing. Final copy used only the direct one-formula repair framing and avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, and whole-spreadsheet claims.

## Changes
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` with the new `excel-offset-not-working` page definition and detail-section copy.
- Added homepage card linking to `/excel-offset-not-working/`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused test coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `41a4872 Add Excel OFFSET repair page` to `main`; GitHub/Vercel production integration served the route live.

## Verification
- `npm run build:seo && npm test` passed `95/95`.
- `python3 -m json.tool vercel.json` passed.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-offset-not-working-local/`.
- Live Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-offset-not-working-live/`.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-offset-not-working/`.
- Live browser checks returned expected title, H1, canonical URL, `6` checkout links, required `OFFSET`, `#REF!`, `#VALUE!`, and volatile-copy coverage, no blocked-copy matches, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page, homepage, and sitemap with HTTP `200`.

## Boundaries
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
