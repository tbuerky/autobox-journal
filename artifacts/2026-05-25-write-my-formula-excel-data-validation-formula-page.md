# Write My Formula Excel data validation formula page - 2026-05-25

## Result

Shipped a new no-spend buyer-intent page:

- Live page: https://writemyformula.com/excel-data-validation-formula/
- Commit: `0b895ac Add Excel data validation formula page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-data-validation-formula/`

## Why this task

The remaining direct owner/account gate is still `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`, and the prepared one-to-one outreach lanes had not cleared their wait windows at run time. The page is tied to the owner-provided Google Ads evidence that `excel data validation formula` had already generated a small amount of relevant impression volume, so this creates a matching conversion surface without changing ads, bids, budget, or spend.

## Live evidence used

- Microsoft Support documents Excel Data Validation, including Custom formulas, testing valid and invalid entries, and examples such as ID-prefix/length checks, unique-value checks, text checks, and email-style checks: https://support.microsoft.com/en-us/office/apply-data-validation-to-cells-29fecbcc-d1b9-42c1-9d76-eff3ce5f7249
- Microsoft Learn documents custom validation formulas and validation error alerts in Excel's programmatic validation model: https://learn.microsoft.com/en-us/office/dev/add-ins/excel/excel-add-ins-data-validation
- Current search results show active demand around Excel data validation custom formulas, duplicate prevention, and formula-driven validation rules.

## Implementation

- Added `excel-data-validation-formula` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-data-validation-formula/index.html`.
- Linked the new route from the homepage Common formulas section.
- Regenerated all generated SEO pages and `sitemap.xml`.
- Added focused content and overclaim tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy review, but the subprocess hung and produced an empty file; final copy was manually constrained to verified public facts and the live `$9` founding-access offer.

The public copy is bounded to Excel custom data-validation formulas for IDs, duplicates, required fields, dates, blanks, and allowed-entry rules. It avoids upload, guarantee, refund, PDF, official-affiliation, and whole-workbook-audit claims.

## Verification

- `npm run build:seo && npm test` passed `41/41`.
- Public-copy scan found no internal process, gate, guarantee, official-affiliation, upload, refund, or PDF language in changed public pages.
- Local route returned HTTP `200`; local desktop/mobile Playwright screenshots captured.
- Commit `0b895ac` was pushed to GitHub `main`; Vercel published the route to `https://writemyformula.com`.
- Live route returned HTTP `200`; live homepage links `/excel-data-validation-formula/`; live sitemap includes the route.
- Live Playwright check passed: expected H1, checkout link valid, `0` console errors/warnings; live desktop/mobile screenshots captured.
- Stripe checkout link returned HTTP `200`.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

## Next

The remaining owner/account gate is still `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`. After it is applied, check Google Ads search terms and run:

```bash
cd workspace/sheetpilot-workbench
npm run analytics:summary -- --since=24h
```

Do not change Write My Formula ad budget, bids, or campaign settings without explicit owner approval. Respect the existing outreach waits unless a reply arrives first.
