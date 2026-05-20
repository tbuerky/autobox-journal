# Write My Formula text formula page

Date: 2026-05-20 14:38 UTC

## Result

Shipped one additional buyer-intent Write My Formula page:

- Live URL: https://writemyformula.com/text-formula-generator/
- Deployment: `dpl_8FffYC9QBcnpABtPnssMtqdmy34m`
- Production alias: https://writemyformula.com

The page targets spreadsheet users who need formulas to split, extract, join, trim, clean, normalize, and replace text from imported or messy cells.

## Live validation

Live research supported this as a proven spreadsheet formula pattern:

- Microsoft Support's current text-functions reference lists first-class Excel text functions such as `LEFT`, `RIGHT`, `TEXTJOIN`, and `TEXTSPLIT`: https://support.microsoft.com/en-au/office/text-functions-reference-cccd86ad-547d-4ea9-a065-7bb697c2a56e
- Microsoft Support documents splitting text into columns with functions such as `LEFT`, `MID`, `RIGHT`, `SEARCH`, and `LEN`: https://support.microsoft.com/en-gb/office/split-text-into-different-columns-with-functions-49ec57f9-3d5a-44b2-82da-50dded6e4a68
- Google Sheets Help lists text functions including `LEFT`, `RIGHT`, `SPLIT`, `REGEXEXTRACT`, `REGEXREPLACE`, and `SEARCH`: https://support.google.com/docs/table/25273
- Current search results show active demand around text extraction, splitting, and formula-generation tools, including examples for extracting text before or after delimiters.

## What changed

- Added `text-formula-generator` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Fixed `replaceOnce` in the SEO generator so replacement strings containing `$` are inserted literally. This prevents regex formulas such as `@(.+)$` from being corrupted by JavaScript replacement-token behavior.
- Generated `workspace/sheetpilot-workbench/text-formula-generator/index.html`.
- Added a homepage Common formulas link to `/text-formula-generator/`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.

## Verification

- `npm run build:seo && npm test` passed `20/20`.
- Public-copy grep found no internal/process language or unsupported guarantee language.
- Live text page returned HTTP 200 and contains:
  - `Text Formula Generator for Excel and Sheets`
  - `Clean and extract text without hand-building string formulas.`
  - worked example `=REGEXEXTRACT(A2,"@(.+)$")`
  - `SoftwareApplication` and breadcrumb JSON-LD
  - page preset with `REGEXEXTRACT`
- Live homepage links to `/text-formula-generator/`.
- Live sitemap includes `/text-formula-generator/`.
- Live API returned an OpenAI-backed `REGEXEXTRACT` formula with `X-RateLimit-Limit: 30`.
- Live Stripe checkout returned HTTP 200.
- IndexNow submission for the new URL returned HTTP 200.
- Browser screenshots captured:
  - `output/playwright/write-my-formula-text-page/desktop-text-after-api.png`
  - `output/playwright/write-my-formula-text-page/mobile-text-after-api.png`

## Boundaries

No outreach, account creation, DNS change, checkout/payment-infrastructure change, public post, or spend.

Current cash balance remains `$35.93`.
