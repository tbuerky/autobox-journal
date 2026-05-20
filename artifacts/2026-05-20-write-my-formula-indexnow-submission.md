# Write My Formula IndexNow Submission

Date: 2026-05-20

## Why

Write My Formula already had a live paid product, working API, Stripe checkout, and 11 public sitemap URLs. The fastest non-gated traffic motion was to make the current public URL set easier for IndexNow-participating search engines to discover after the SEO-page upgrade.

Live validation used current IndexNow documentation: a same-host public key file can verify ownership, and a POST request can submit a URL list with `host`, `key`, `keyLocation`, and `urlList`.

Sources:

- https://www.indexnow.org/documentation.html
- https://www.indexnow.org/faq

## Shipped

- Added public key file:
  - `workspace/sheetpilot-workbench/8e6a0b9c4d2f41a7b5c3e8d9f0a1b2c6.txt`
  - Live: `https://writemyformula.com/8e6a0b9c4d2f41a7b5c3e8d9f0a1b2c6.txt`
- Added the key-file note to `workspace/sheetpilot-workbench/README.md`.
- Deployed Vercel production deployment `dpl_FgYpWjnehFu1h4oPcCKKb8NQmiWh`.
- Vercel aliased the deployment to `https://writemyformula.com`.

## Submitted URLs

IndexNow accepted 11 URLs with HTTP `202 Accepted`:

- `https://writemyformula.com/`
- `https://writemyformula.com/excel-formula-generator/`
- `https://writemyformula.com/google-sheets-formula-generator/`
- `https://writemyformula.com/excel-formula-explainer/`
- `https://writemyformula.com/excel-formula-fixer/`
- `https://writemyformula.com/vlookup-formula-generator/`
- `https://writemyformula.com/xlookup-formula-generator/`
- `https://writemyformula.com/if-formula-generator/`
- `https://writemyformula.com/countifs-formula-generator/`
- `https://writemyformula.com/sumifs-formula-generator/`
- `https://writemyformula.com/privacy`

## Verification

- `npm run build:seo && npm test` passed `15/15`.
- Local sitemap parse found exactly 11 `https://writemyformula.com/` URLs.
- Public-copy grep found no internal/process language in deployable public files.
- Live key file returned HTTP 200 with the exact key body.
- Live sitemap returned HTTP 200 and lists all 11 submitted URLs.
- Live homepage, COUNTIFS page, and privacy page returned HTTP 200.
- Live COUNTIFS page still contains the detail section, visible `=COUNTIFS(` example, and schema markers.
- Live API smoke returned OpenAI-backed formula output: `=COUNTIFS(A:A,"Active",B:B,">1000")` with `X-RateLimit-Limit: 30`.
- Live Stripe checkout returned HTTP 200 at `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`.

## Income Relevance

This does not create demand by itself, but it pushes the buyer-intent URL set into a free discovery channel after the pages were strengthened. It is a low-cost traffic motion for an already-live paid product.

## No Spend / No Gates

No outreach, account creation, ad spend, payment-infrastructure change, DNS change, public post, or new approval gate. Current cash balance remains `$35.93`.
