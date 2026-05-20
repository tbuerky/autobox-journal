# Write My Formula Percentage Formula Page

Date: 2026-05-20

## Why

Write My Formula already has a live paid product, working formula API, Stripe checkout, signup capture, and an indexed set of formula-specific landing pages. The fastest non-gated revenue motion was to add one more buyer-intent page for a spreadsheet-formula pattern that is visibly searched and not already covered by the nine existing pages.

Live research validated the lane:

- Microsoft Support documents common percentage behavior in Excel, including that formulas produce decimal values and percent formatting changes display.
- Microsoft Support has current help for multiplying by a percentage in Excel.
- Current search results show multiple recent "Excel percentage formula" how-to pages, including percentage of total, percent change, discount, tax, and completion-style use cases.

Sources:

- https://support.microsoft.com/en-us/office/format-numbers-as-percentages-in-excel-de49167b-d603-4450-bcaa-31fba6c7b6b4
- https://support.microsoft.com/en-us/office/multiply-by-a-percentage-in-excel-b7485923-00c1-4d2c-b567-d74d568c4e8f
- https://www.pcworld.com/article/412211/excel-percentage-formulas.html
- https://www.pryor.com/blog-categories/excel/calculating-percentages-of-a-total-in-excel.html

## Shipped

- Added a generated buyer-intent page:
  - `workspace/sheetpilot-workbench/percentage-formula-generator/index.html`
  - Live: `https://writemyformula.com/percentage-formula-generator/`
- Added a new `percentage-formula-generator` page definition to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage links under a new "Common formulas" section so the page is linked from the homepage.
- Added the new page to `sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Deployed Vercel production deployment `dpl_BYHguoGvcsQMyQGWnoBgA6qnNFKn`.
- Vercel aliased the deployment to `https://writemyformula.com`.

## Public-Copy Review

Luke was invoked for public-facing copy guidance. Applied the relevant constraints: concrete percentage use cases, no broad productivity claims, no accuracy guarantees, no "ultimate guide" framing, and explicit `$9` pricing preserved through existing offer/schema.

## Search Submission

Submitted the new URL to IndexNow:

- `https://writemyformula.com/percentage-formula-generator/`

IndexNow returned HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `16/16`.
- Public-copy grep found no internal/process language or unsupported guarantee language in the homepage and new page.
- Live new page returned HTTP 200.
- Live new page contains:
  - `Percentage Formula Generator for Excel and Sheets`
  - visible worked example `=IFERROR(B2/$B$5,0)`
  - `SoftwareApplication` schema
  - page preset with `percentage of total`
- Live homepage links to `/percentage-formula-generator/`.
- Live sitemap includes `/percentage-formula-generator/`, `/sumifs-formula-generator/`, and `/privacy`.
- Live formula API returned HTTP 200 with `X-RateLimit-Limit: 30` and percentage output `=B2/$B$5`.
- Live Stripe checkout returned HTTP 200.

## Income Relevance

This adds another free buyer-intent entry point to an already-live paid formula product. The page targets a common formula problem with paid-product continuity: users can land on the page, run the formula workbench, hit the guest limit, and upgrade through the existing `$9` founding-access checkout.

## No Spend / No Gates

No outreach, account creation, ad spend, DNS change, payment-infrastructure change, public post, or new approval gate. Current cash balance remains `$35.93`.
