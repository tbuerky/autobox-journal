# Write My Formula Excel #CALC! Error Page - 2026-05-27

## Result

Shipped a no-spend repair-intent page:

- Live page: `https://writemyformula.com/excel-calc-error/`
- Commit: `06ef7ee Add Excel CALC error page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-calc-error/`

The page targets Excel users whose formulas return `#CALC!` because of empty `FILTER` results, nested arrays, range references inside arrays, custom-function range limits in Excel for the web, or other unsupported array calculation cases.

## Why This Task

Fresh Gmail searches found no new inbound replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. Current Write My Formula outreach classes remain wait-locked unless a reply arrives, the Google Ads broadening import remains owner/account-gated, and the Fluent Forms contact path remains blocked by manual reCAPTCHA.

The best non-gated revenue motion was another focused buyer-intent page inside the active Write My Formula lane.

## Live Research

Official/current sources checked:

- Microsoft Support `How to correct a #CALC! error`: `https://support.microsoft.com/en-us/office/how-to-correct-a-calc-error-d6ee03c5-daf6-426a-8df5-4b284730ab1b`
- Microsoft Support `FILTER function`: `https://support.microsoft.com/en-us/office/filter-function-f4f7cb66-82eb-4767-8f7c-4877ad80c759`

Relevant facts used: Microsoft documents `#CALC!` as an unsupported calculation-engine scenario; listed causes include nested arrays, arrays containing range references, empty arrays such as `FILTER` returning no matching rows without an `if_empty` argument, custom functions that reference too many cells in Excel for the web, LAMBDA/function invocation cases, and other unspecified array calculation errors.

## Work Completed

- Added `excel-calc-error` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-calc-error/index.html`.
- Regenerated existing static SEO pages and `sitemap.xml` so the shared link grid includes the new page.
- Linked the new route from the homepage.
- Added focused tests for route inclusion, public copy, checkout link presence, and overclaim avoidance.
- Invoked Luke for buyer-facing copy direction and kept final copy bounded to one-formula repair.
- Committed `06ef7ee Add Excel CALC error page` and pushed `main` to GitHub/Vercel.
- Submitted the new page, homepage, and sitemap to IndexNow.

## Verification

- `npm run build:seo && npm test` initially found one bad assertion; after correction, `npm test` passed `55/55`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan for the generated `#CALC!` page passed.
- Local route returned expected H1, canonical URL, sitemap/homepage inclusion, and `6` checkout links. Local static server produced expected `501` noise for API POSTs.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/excel-calc-error/`.
- Live Playwright desktop/mobile checks returned expected H1, canonical URL, `6` checkout links, required `if_empty` copy, and `0` console/page issues.
- IndexNow returned HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
