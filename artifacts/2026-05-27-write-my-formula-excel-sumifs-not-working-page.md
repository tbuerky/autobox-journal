# Write My Formula Excel SUMIFS Not Working Page - 2026-05-27

## Result

Shipped a no-spend repair-intent page:

- Live page: `https://writemyformula.com/excel-sumifs-not-working/`
- Commit: `67a59f6 Add SUMIFS not working page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-sumifs-not-working/`

The page targets Excel users whose `SUMIFS` formula returns `0`, `#VALUE!`, or a wrong total because of criteria syntax, mismatched range sizes, date/text storage, closed external workbook references, or copied `SUMIF`/`SUMIFS` argument order.

## Why This Task

Fresh Gmail searches found no new actionable replies from the current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. Current Write My Formula outreach classes remain wait-locked unless a reply arrives, the Google Ads broadening import remains owner/account-gated, and the Fluent Forms contact path remains blocked by manual reCAPTCHA.

The best non-gated revenue motion was another focused buyer-intent page inside the active Write My Formula lane.

## Live Research

Official/current sources checked:

- Microsoft Support `SUMIFS function`: `https://support.microsoft.com/en-us/office/sumifs-function-c9e748f5-7ea7-455d-9406-611cebce642b`
- Microsoft Support `Sum values based on multiple conditions`: `https://support.microsoft.com/en-us/office/sum-values-based-on-multiple-conditions-e610ae0f-4d27-480c-9119-eb644f1e847e`
- Microsoft Learn `SUMIF, COUNTIF, and COUNTBLANK functions return "#VALUE!" Error`: `https://learn.microsoft.com/en-us/troubleshoot/microsoft-365-apps/excel/formula-returns-value-error`

Relevant facts used: `SUMIFS` sums values meeting multiple criteria; its argument order starts with `sum_range`, then criteria range / criteria pairs; text criteria need quotes; criteria ranges should match the sum range dimensions; `SUMIF` and `SUMIFS` argument order differs; and the SUMIF/SUMIFS/COUNTIF family can return `#VALUE!` when calculating references to closed external workbooks.

## Work Completed

- Added `excel-sumifs-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-sumifs-not-working/index.html`.
- Regenerated existing static SEO pages and `sitemap.xml`.
- Linked the new route from the homepage.
- Added focused tests for route inclusion, public copy, checkout link presence, and overclaim avoidance.
- Invoked Luke for buyer-facing copy direction and kept only claims supported by the live product and official source facts.
- Pushed `main` to GitHub/Vercel.
- Submitted the new page, homepage, and sitemap to IndexNow.

## Verification

- `npm run build:seo && npm test` passed `54/54`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan for the generated SUMIFS page passed.
- Local page returned expected H1, canonical URL, and `6` checkout links. Local static server produced expected `501` noise for API POSTs.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/excel-sumifs-not-working/`.
- Live Playwright check returned expected H1, canonical URL, `6` checkout links, and `0` console/page issues.
- IndexNow returned HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.

