# Write My Formula conditional formatting formula page

Date: 2026-05-20 14:27 UTC

## Result

Shipped one additional buyer-intent Write My Formula page:

- Live URL: https://writemyformula.com/conditional-formatting-formula-generator/
- Deployment: `dpl_68Egm1qVhWFmfBsrNVUNfpi2PXkQ`
- Production alias: https://writemyformula.com
- Screenshot: `output/playwright/write-my-formula-conditional-formatting/live.png`

The page targets custom conditional-formatting formula searches for Excel and Google Sheets users who need row highlights, overdue-date rules, duplicate/missing-value checks, and status-based formatting.

## Live validation

Live research supported this as a proven spreadsheet-help pattern:

- Microsoft Support documents Excel conditional formatting formulas and says formula-based rules must return True or False. Source: https://support.microsoft.com/en-us/office/use-conditional-formatting-to-highlight-information-fed60dfa-1d3f-4e13-9ecb-f1951ff89d7f
- Google Sheets Help documents conditional formatting custom formulas and notes cross-sheet references require `INDIRECT`. Source: https://support.google.com/docs/answer/78413/use-conditional-formatting-rules-in-google-sheets-computer
- Current search results surface repeated conditional-formatting custom-formula help demand, including Microsoft/Google docs, tutorials, and recent user questions around formula references and row highlighting.

## What changed

- Added `conditional-formatting-formula-generator` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/conditional-formatting-formula-generator/index.html`.
- Added a homepage Common formulas link to `/conditional-formatting-formula-generator/`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy review and applied the useful guidance: made the H1 more transactional, softened unsupported "checks for" wording to "notes on", removed defensive "real spreadsheet work" phrasing, and replaced vague "high monthly limit" pricing copy with the configured `500 runs per month`.

## Verification

- `npm run build:seo && npm test` passed `18/18`.
- Public-copy grep found no internal/process language or unsupported guarantee language.
- Live conditional-formatting page returned HTTP 200 and contains:
  - `Conditional Formatting Formula Generator for Excel and Sheets`
  - `Get the formula for your conditional formatting rule.`
  - worked example `=AND($B2<TODAY(),$C2<>"Done")`
  - `SoftwareApplication` and breadcrumb JSON-LD
- Live homepage links to `/conditional-formatting-formula-generator/` and shows `500 runs per month`.
- Live sitemap includes `/conditional-formatting-formula-generator/`.
- Live API returned an OpenAI-backed conditional-formatting formula: `=AND($B2<TODAY(), $C2<>"Done")` with `X-RateLimit-Limit: 30`.
- Live Stripe checkout returned HTTP 200.
- IndexNow submission for the new URL returned HTTP 200.

## Boundaries

No outreach, account creation, DNS change, payment-infrastructure change, public post, or spend.

Current cash balance remains `$35.93`.
