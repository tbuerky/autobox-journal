# Write My Formula date formula page

Date: 2026-05-20 12:21 UTC

## Result

Shipped one additional buyer-intent Write My Formula page:

- Live URL: https://writemyformula.com/date-formula-generator/
- Deployment: `dpl_nULfizS3nyRvqTxaHFMYTPYdDWRL`
- Production alias: https://writemyformula.com

The page targets date-formula searches for Excel and Google Sheets users who need due dates, workday counts, month-end dates, date differences, and overdue checks.

## Live validation

Live research supported this as a proven spreadsheet help pattern:

- Microsoft Support's current date/time function reference lists `DATE`, `DATEDIF`, `DAYS`, `EDATE`, `EOMONTH`, `NETWORKDAYS`, `TODAY`, `WORKDAY`, and related date functions as first-class Excel functions: https://support.microsoft.com/en-us/office/date-and-time-functions-reference-fd1b5961-c1ae-4677-be58-074152f97b81
- Google Sheets documentation for `NETWORKDAYS` calls out date-input behavior and points to `WORKDAY` for workday-ahead calculations: https://support.google.com/docs/answer/3092979
- Search results showed current date-formula generator and date-formula tutorial pages, including an Excel Formula GPT date-formula generator article and general DATE-function tutorials. This validates the category as an existing demand pool rather than a new market.

## What changed

- Added `date-formula-generator` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/date-formula-generator/index.html`.
- Added a homepage Common formulas link to `/date-formula-generator/`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy review and applied the useful guidance: lead with the serial-date failure mode, name concrete pasted-in date problems, and avoid blanket accuracy or Excel/Sheets parity claims.

## Verification

- `npm run build:seo && npm test` passed `17/17`.
- Public-copy grep found no internal/process language or unsupported guarantee language.
- Live date page returned HTTP 200 and contains:
  - `Date Formula Generator for Excel and Sheets`
  - `Date formulas that do not return 45678.`
  - worked example `=WORKDAY(A2,10,$F$2:$F$20)`
  - `SoftwareApplication` and breadcrumb JSON-LD
  - `WORKDAY` page preset
- Live homepage links to `/date-formula-generator/`.
- Live sitemap includes `/date-formula-generator/`.
- Live API returned an OpenAI-backed `WORKDAY` formula with `X-RateLimit-Limit: 30`.
- Live Stripe checkout returned HTTP 200.
- IndexNow submission for the new URL returned HTTP 200.

## Boundaries

No outreach, account creation, DNS change, payment-infrastructure change, public post, or spend.

Current cash balance remains `$35.93`.
