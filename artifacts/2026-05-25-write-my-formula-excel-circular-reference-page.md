# Write My Formula Excel circular reference page - 2026-05-25

## Result

Shipped a new no-spend buyer-intent page:

- Live page: https://writemyformula.com/excel-circular-reference/
- Commit: `40db9e8 Add Excel circular reference page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/write-my-formula-circular-reference/`

## Why this task

The current direct account gate is still `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`, and the prepared one-to-one outreach lanes were still wait-locked at run time. A circular-reference repair page is adjacent to the live Write My Formula repair-intent cluster and fits the pending broader paid-search posture without changing ad settings or spending money.

## Live evidence used

- Microsoft Support documents Excel circular references as formulas that refer to their own cell directly or indirectly, and describes removing them or intentionally allowing them with iterative calculation: https://support.microsoft.com/en-us/office/remove-or-allow-a-circular-reference-in-excel-8540bd0f-6e97-4483-bcf7-1b49cd50d123
- Microsoft Support also documents formula recalculation and iterative calculation controls: https://support.microsoft.com/en-gb/office/change-formula-recalculation-iteration-or-precision-in-excel-73fc7dac-91cf-4d36-86e8-67124f6bcce4
- Current search results and Microsoft Q&A/forum-style pages show ongoing user confusion around finding circular references and whether iteration should be enabled.

## Implementation

- Added `excel-circular-reference` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-circular-reference/index.html`.
- Linked the new route from the homepage Common formulas section.
- Regenerated `sitemap.xml`.
- Added focused content tests and overclaim checks in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy guidance at `workspace/sheetpilot-workbench/luke-excel-circular-reference-page.md`.

The public copy is bounded to one-formula repair and avoids upload, workbook-audit, reference-chain tracing, guarantee, refund, PDF, and official-affiliation claims.

## Verification

- `npm run build:seo && npm test` passed `40/40`.
- Public-copy scan found no upload, workbook-audit, trace-chain, guarantee, official-affiliation, PDF, or refund claims in the new page/homepage changed copy.
- Local route returned HTTP `200`; local desktop/mobile screenshots captured.
- Live route returned HTTP `200` after GitHub/Vercel deploy.
- Live Playwright check passed: route/home/sitemap HTTP `200`, expected H1, homepage link present, sitemap route present, checkout link valid, `0` console errors, `0` warnings.
- Live desktop/mobile screenshots captured.
- Stripe checkout link returned HTTP `200`.
- IndexNow accepted page/home/sitemap submission with HTTP `202`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

## Next

The remaining owner/account gate is still `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`. After it is applied, check Google Ads search terms and run:

```bash
cd workspace/sheetpilot-workbench
npm run analytics:summary -- --since=24h
```

Do not change Write My Formula ad budget, bids, or campaign settings without explicit owner approval. Respect the existing outreach waits unless a reply arrives first.
