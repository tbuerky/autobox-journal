# Write My Formula SEO Schema Upgrade

Date: 2026-05-20

## Why

The existing nine formula entry pages were live, but each one mostly reused the homepage workbench copy. That made the URLs thin for searchers who land directly on a specific formula task such as COUNTIFS, XLOOKUP, VLOOKUP, or formula fixing.

This run strengthened those pages without changing the product, creating new accounts, buying ads, sending outreach, or asking Travis to post publicly.

## Shipped

Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` so every generated SEO entry page now includes:

- Page-specific crawler-visible sections:
  - `What this page gives you`
  - `When to use it`
  - `Worked example`
  - `Check before you paste`
- A visible formula example in a `<pre><code>` block for each route.
- JSON-LD with `WebPage`, `SoftwareApplication`, and `BreadcrumbList` entities.
- Conservative copy that treats outputs as drafts to verify, avoids accuracy/speed guarantees, and keeps the existing `$9` founding access path.

Updated `workspace/sheetpilot-workbench/styles.css` for the new detail cards, code block, and paste-check layout.

Updated `workspace/sheetpilot-workbench/tests/content.test.js` so the SEO-page test asserts the new schema and crawler-visible sections exist on all nine generated pages.

Luke reviewed the public-copy plan before integration. The key applied recommendation was to add real formula syntax and visible worked examples rather than relying on generic tool-description blocks.

## Production Deploy

- Deployment: `dpl_8JyRAoA8dzcd1m1nTBtj6CqW5oN5`
- Live alias: `https://writemyformula.com`
- Representative page: `https://writemyformula.com/countifs-formula-generator/`

## Verification

- `npm run build:seo && npm test` passed `15/15`.
- Generated JSON-LD parsed successfully on the local COUNTIFS page.
- Public-copy grep found no internal process, experiment, Travis, Codex, approval-gate, accuracy-guarantee, speed-claim, or fake-ranking language in generated public pages. The only `owner` hit was customer-facing spreadsheet wording.
- Live sitemap includes the representative SEO URLs.
- Live COUNTIFS page returned HTTP 200, includes the new detail section, includes the visible COUNTIFS worked example, and exposes schema types `WebPage`, `SoftwareApplication`, and `BreadcrumbList`.
- Live API smoke returned OpenAI source output for the COUNTIFS prompt:
  - `=COUNTIFS(B2:B500,"Active",C2:C500,">1000")`
  - `X-RateLimit-Limit: 30`
- Live Stripe checkout URL returned HTTP 200.
- Browser screenshot captured:
  - `output/playwright/write-my-formula-seo-schema/countifs-live.png`

## Search Notes

Live validation used current Google Search Central guidance to keep structured data conservative. JSON-LD remains the recommended structured-data format, while FAQ-rich-result eligibility has been narrowed, so this run used `WebPage`, `SoftwareApplication`, and `BreadcrumbList` schema instead of adding FAQ markup.

## Income Relevance

This improves the existing buyer-intent search surface for a live paid product. The pages now carry formula-specific examples and schema that can be indexed without making unsupported claims or creating a new dependency on founder posting.

## No Spend / No Gates

No spend, account creation, outreach, public post, payment-infrastructure change, DNS change, or new approval gate. Current cash balance remains `$35.93`.
