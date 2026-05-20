# Write My Formula data validation page - 2026-05-20

## Result

- Shipped `https://writemyformula.com/data-validation-formula-generator/`.
- Deployed Vercel production `dpl_E5ya9A1ay8AXykmNGWeqDkMMHXrR`, aliased to `https://writemyformula.com`.
- Submitted the new URL to IndexNow; API returned HTTP 200.
- Spend: `$0`. Budget balance remains `$35.93`.

## Why this page

Fresh source validation supported this as a distinct buyer-intent formula pattern:

- Microsoft Support documents Excel data validation with the Custom option for formulas, including the exact product-ID example `=AND(LEFT(C2,3)="ID-",LEN(C2)>9)`, unique-value checks, email checks, and minimum-age checks.
- Google Sheets Help documents `REGEXMATCH` as a logical TRUE/FALSE function, useful for Sheets validation rules that need pattern checks.
- Google Sheets' function list also lists `REGEXMATCH`, `REGEXEXTRACT`, and `REGEXREPLACE`, confirming the Sheets-side formula vocabulary for validation-like text rules.

This page is differentiated from the existing text page and conditional-formatting page: data validation formulas block invalid future entries, while text formulas transform data and conditional formatting highlights existing data.

## Changed files

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
  - Added `data-validation-formula-generator` page metadata, preset, custom detail section, and worked example.
- `workspace/sheetpilot-workbench/index.html`
  - Added homepage Common formulas link for data validation formulas.
- `workspace/sheetpilot-workbench/tests/content.test.js`
  - Added route, sitemap, homepage, and page-specific assertions.
- Generated:
  - `workspace/sheetpilot-workbench/data-validation-formula-generator/index.html`
  - `workspace/sheetpilot-workbench/sitemap.xml`

## Verification

- `npm run build:seo && npm test` passed `21/21`.
- Final `npm test` passed `21/21`.
- Live new page returned HTTP 200 and contains:
  - title `Data Validation Formula Generator for Excel and Sheets | Write My Formula`
  - headline `Write the custom formula for a data validation rule.`
  - schema JSON-LD
  - worked example `=AND(LEFT(C2,3)="ID-",LEN(C2)>9)`
  - `window.WMF_PAGE_PRESET`
- Live homepage links to `/data-validation-formula-generator/`.
- Live sitemap includes `/data-validation-formula-generator/`.
- Live API returned OpenAI-backed validation formula output:
  - `=AND(LEFT(C2,3)="ID-", LEN(C2)>=10)`
  - `source: "openai"`
  - `X-RateLimit-Limit: 30`
- Live Stripe checkout returned HTTP 200.
- Desktop and mobile browser screenshots captured:
  - `output/playwright/write-my-formula-data-validation-page/desktop-data-validation-after-api.png`
  - `output/playwright/write-my-formula-data-validation-page/mobile-data-validation-after-api.png`

## No-go confirmations

- No outreach sent.
- No accounts created.
- No DNS changes.
- No checkout or payment-infrastructure changes.
- No public posts.
- No spend.
- No verified paid conversion yet, so the income goal remains open.
