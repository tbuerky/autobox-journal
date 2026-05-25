# Write My Formula Excel Formulas Not Working Page

Date: 2026-05-25 06:25 UTC

## Result

Shipped a new buyer-intent repair page for Write My Formula:

- Live page: `https://writemyformula.com/excel-formulas-not-working/`
- Commit: `f5c2d08 Add Excel formulas not working page`
- Screenshot folder: `workspace/sheetpilot-workbench/output/playwright/excel-formulas-not-working/`

## Why This Task

The remaining Write My Formula Google Ads broadening import is owner/account-gated, and current one-to-one outreach wait windows have not cleared. This page moves the same active paid-search lane forward without spend by adding a landing surface for broader fix-intent searches around Excel formulas not working, not calculating, showing formula text, or breaking after imports.

## Live Evidence

Research used current public support/search evidence:

- Microsoft Support documents the same problem cluster: Show Formulas mode, cells formatted as text, manual calculation, missing equals sign, formula error values, missing parentheses/arguments, quoted text, and data-type problems. Source: https://support.microsoft.com/en-us/office/how-to-avoid-broken-formulas-in-excel-8309381d-33e8-42f6-b889-84ef6df1d586
- Microsoft Learn documents locale/list-separator formula errors and notes that the typed argument separator can differ from Excel/Windows regional settings. Source: https://learn.microsoft.com/en-us/troubleshoot/microsoft-365-apps/excel/formula-errors
- Ablebits has a long-running, currently active competitor/support article around Excel formulas not working, including calculation mode, Show Formulas, text-formatted formulas, and list-separator issues. Source: https://www.ablebits.com/office-addins-blog/excel-formulas-not-working/

## Work

- Added `excel-formulas-not-working` to the SEO page generator with page-specific metadata, preset, detail section, worked example, and copy checks.
- Regenerated the static SEO pages and sitemap.
- Added a homepage card for the new route.
- Added regression coverage for the new page, sitemap inclusion, homepage link, checkout href, and no-overclaim copy constraints.
- Committed and pushed to `main`, triggering Vercel production deployment through the connected GitHub repo.
- Submitted the new page, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `38/38`.
- Public-copy scan passed for internal/process/gate/approval/guarantee/upload/refund/Microsoft-partner language.
- Local route returned HTTP `200`; local Playwright snapshot/screenshot captured. The local static server produced expected 501s for API POSTs because it does not emulate Vercel functions.
- Live route returned HTTP `200` with the expected H1.
- Live homepage returned HTTP `200` and links `/excel-formulas-not-working/`.
- Live sitemap returned HTTP `200` and includes `https://writemyformula.com/excel-formulas-not-working/`.
- Live Stripe checkout returned HTTP `200`.
- Live Playwright snapshot/screenshot captured; browser console had `0` errors and `0` warnings after the Vercel page loaded.

## Gates and Budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred.

Open gate remains: `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`.

Current cash balance remains `$35.93`.
