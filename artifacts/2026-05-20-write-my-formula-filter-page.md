# Write My Formula FILTER formula page

Date: 2026-05-20 14:32 UTC

## Result

Shipped one additional buyer-intent Write My Formula page:

- Live URL: https://writemyformula.com/filter-formula-generator/
- Deployment: `dpl_2bRWrDtzKQAbRWHM6SeT4dZbt7Dz`
- Production alias: https://writemyformula.com

The page targets spreadsheet users who need `FILTER` formulas that return matching rows for status, region, date, text, and threshold conditions.

## Live validation

Live research supported this as a proven spreadsheet formula pattern:

- Microsoft Support documents Excel's `FILTER` function as a dynamic-array function for filtering a range based on criteria: https://support.microsoft.com/en-gb/office/filter-function-f4f7cb66-82eb-4767-8f7c-4877ad80c759
- Current search results include live FILTER-function tutorial and formula-reference pages, including Spreadsheet Center's FILTER page and Google Sheets FILTER examples. This validates a demand pool around FILTER syntax, spill behavior, multiple criteria, and empty-result handling.
- Existing competitor/category results include formula-generator products that explicitly mention `FILTER`, supporting the search-intent fit for a focused Write My Formula landing page.

## What changed

- Added `filter-formula-generator` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/filter-formula-generator/index.html`.
- Added a homepage Common formulas link to `/filter-formula-generator/`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.

## Verification

- `npm run build:seo && npm test` passed `19/19`.
- Public-copy grep found no internal/process language or unsupported guarantee language.
- Live FILTER page returned HTTP 200 and contains:
  - `FILTER Formula Generator for Excel and Sheets`
  - `Return the rows that match your conditions.`
  - worked example `=FILTER(A2:D500,(B2:B500="West")*(C2:C500="Open")*(D2:D500>5000),"No matching rows")`
  - `SoftwareApplication` and breadcrumb JSON-LD
  - page preset with `FILTER`
- Live homepage links to `/filter-formula-generator/`.
- Live sitemap includes `/filter-formula-generator/`.
- Live API returned an OpenAI-backed `FILTER` formula with `X-RateLimit-Limit: 30`.
- Live Stripe checkout returned HTTP 200.
- IndexNow submission for the new URL returned HTTP 200.
- Browser screenshots captured:
  - `output/playwright/write-my-formula-filter-page/desktop-filter-after-api.png`
  - `output/playwright/write-my-formula-filter-page/mobile-filter-after-api.png`

## Boundaries

No outreach, account creation, DNS change, checkout/payment-infrastructure change, public post, or spend.

Current cash balance remains `$35.93`.
