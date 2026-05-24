# Write My Formula Excel Formula Help Page - 2026-05-24

## Decision

Created and deployed a broad help-intent Write My Formula page for the pending Google Ads broadening traffic:

- Preview/live Vercel alias: `https://sheetpilot-workbench-three.vercel.app/excel-formula-help/`
- Intended canonical/customer URL: `https://writemyformula.com/excel-formula-help/`

The customer domain is not yet serving the new page because `writemyformula.com` is not accessible under the authenticated Vercel scope. I did not force a domain/account change.

## Why this task

The prior run created a Google Ads broadening import packet for `excel formula help`, `help with excel formula`, `write/create Excel formula`, and adjacent Sheets help-intent terms, but the import is owner-gated. This run created one no-spend landing page that can receive the broadened traffic once the campaign import and domain/project access are resolved.

Live research confirmed the broader formula-help category is active and commercial:

- Formulr, FormulaWiz, and HelpFormula all position around plain-English Excel/Google Sheets formula generation, explanation, or debugging.
- Microsoft documents Excel formulas/functions as reference-driven work where references, function choice, and compatibility matter.
- Google documents Sheets functions as a large function surface with platform-specific behavior.

Sources:

- `https://getformulr.app/`
- `https://formulawiz.vercel.app/`
- `https://helpformula.com/`
- `https://support.microsoft.com/en-us/office/overview-of-formulas-in-excel-ecfdc708-9162-49e8-b993-c311f47ca173`
- `https://support.microsoft.com/en-us/office/excel-functions-by-category-5f91f4e9-7b42-46d2-9bd1-63f26a86c0eb`
- `https://support.google.com/docs/table/25273?hl=en`

## Output

Updated:

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/excel-formula-help/index.html`
- `workspace/sheetpilot-workbench/.vercel/project.json`

Saved:

- `workspace/sheetpilot-workbench/luke-excel-formula-help-page.md`
- `workspace/sheetpilot-workbench/output/playwright/write-my-formula-excel-help/live-preview-desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/write-my-formula-excel-help/live-preview-mobile.png`

Deployment:

- Vercel production deployment: `dpl_D2et9hZqAuynXbHaMjMcEPuwSyyt`
- Production alias available now: `https://sheetpilot-workbench-three.vercel.app`

## Verification

Passed:

- `npm run build:seo && npm test` (`37/37`)
- `python3 -m json.tool vercel.json`
- Stripe checkout URL returned HTTP `200`
- Preview route returned HTTP `200` and contains `Write the Excel formula you're stuck on`
- Preview homepage returned HTTP `200` and links `/excel-formula-help/`
- Preview sitemap returned HTTP `200` and includes `https://writemyformula.com/excel-formula-help/`
- Desktop/mobile screenshots captured from the preview deployment
- Public-copy scan found no internal process terms, approval-gate language, stale pricing, official-affiliation claim, or guarantee language in the changed public files

Blocked:

- `https://writemyformula.com/excel-formula-help/` returns HTTP `404`
- `https://writemyformula.com/` returns HTTP `200` but does not include `/excel-formula-help/`
- `vercel domains inspect writemyformula.com --scope travis-buerkys-projects` returned no access to the domain

## Gate

Added owner/account gate:

`RESOLVE: WRITEMYFORMULA.COM VERCEL DOMAIN ACCESS`

No spend, ad setting change, bid/budget change, payment infrastructure change, DNS/domain/account change, outreach, contact form, public post, bulk send, or destructive production change occurred.

Current cash balance remains `$35.93`.
