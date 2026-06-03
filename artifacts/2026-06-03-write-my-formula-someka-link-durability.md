# Write My Formula Someka link durability - 2026-06-03

## Task
Finished the Someka reciprocal-link fulfillment durably instead of leaving it as generated-page drift.

## Why this task
- Existing workspace changes showed the Someka link had been added directly to `ai-google-sheets-formula-generator/index.html`, tested, and logged, but the page generator did not know about the link.
- Any future `npm run build:seo` would have removed the public link, risking a broken reciprocal-link commitment and losing a small SEO/referral relationship asset.
- Active outreach classes remain wait-locked or gated, while this was a concrete revenue/traffic-supporting fulfillment task with no spend and no owner action needed.

## Live validation
- Someka target returned HTTP `200`: `https://www.someka.net/product-category/google-sheets-templates/`.
- The live Someka page identifies itself as `Google Sheets Templates` and lists ready-to-use spreadsheet templates across categories such as accounting/finance, project management, KPI dashboards, inventory management, and other business template areas.
- Write My Formula production page returned HTTP `200`: `https://writemyformula.com/ai-google-sheets-formula-generator/`.

## Work completed
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` so the AI Google Sheets formula generator page can render an optional extra detail card.
- Added the Someka template-starting-point card to the generator, using Luke-reviewed copy and avoiding partnership, affiliate, endorsement, official-affiliation, guarantee, or process language.
- Regenerated `workspace/sheetpilot-workbench/ai-google-sheets-formula-generator/index.html`.
- Preserved the regression test in `workspace/sheetpilot-workbench/tests/content.test.js` that asserts the Someka URL remains on the page.
- Updated the local outreach ledger in `workspace/sheetpilot-workbench/README.md`.
- Committed and pushed nested workspace commit `4859252 Preserve Someka reciprocal link`.
- Deployed production Vercel deployment `dpl_ALzAZYYZCiSmf1buy6KNChQpNLGK`, aliased to `https://writemyformula.com`.
- Submitted the updated page and sitemap to IndexNow; API returned HTTP `200`.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `108/108`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan on the changed page found no matches for internal/process/experiment language or blocked partnership/affiliate/official/guarantee phrasing.
- Live `curl` confirmed `https://writemyformula.com/ai-google-sheets-formula-generator/` returns HTTP `200`.
- Live page source contains `Template starting points`, the Someka URL, and the revised customer-facing copy.
- Live Someka target returns HTTP `200`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred.
- No new outreach was sent in this run; the README records that the Someka reply had already been sent in thread `19e643b23e96f337`.
- `config/OPEN_GATES.md` remains unchanged because the active gates are still the Fluent Forms manual reCAPTCHA and Write My Formula paid-search approval gate.

## Budget
Current cash balance remains `-$24.07`.
