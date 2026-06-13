# Write My Formula Excel RANDARRAY not working page - 2026-06-13

## Task
Shipped `https://writemyformula.com/excel-randarray-not-working/` as a no-spend repair-intent page for Excel users whose `RANDARRAY` formula returns `#VALUE!`, `#SPILL!`, `#NAME?`, changing output, wrong rows/columns, wrong min/max values, or decimal-vs-whole-number issues.

## Why this task
Open gates still block paid-search control changes and the Fluent Forms manual reCAPTCHA submission. Outreach categories remain wait-locked until 2026-06-14 unless a relevant active prospect replies. A new buyer-intent repair surface is a non-gated revenue motion that can capture existing demand without spend.

## Evidence used
- Microsoft RANDARRAY documentation: `RANDARRAY([rows],[columns],[min],[max],[whole_number])`, dynamic random-number output, optional shape/range arguments, and whole-number TRUE/FALSE behavior. Source: https://support.microsoft.com/en-us/office/randarray-function-21261e55-3bec-4885-86a6-8b0a47fd4d33
- Microsoft #SPILL documentation: dynamic array formulas return `#SPILL!` when Excel cannot return the results to the grid. Source: https://support.microsoft.com/en-us/office/how-to-correct-a-spill-error-ffe0f555-b479-4a17-a6e2-ef9cc9ad4023
- Current search results showed live support confusion around RANDARRAY and spill/volatile array behavior, including Stack Overflow and Reddit threads. Those were used only as demand/context signals; final public copy relies on Microsoft-documented behavior.

## What changed
- Added `excel-randarray-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage related-link card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/excel-randarray-not-working/index.html`.
- Regenerated static generated pages and `sitemap.xml` so the new page is linked across the site.
- Added focused content tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed nested app commit `6ef404a3 Add Excel RANDARRAY repair page`.

## Public-copy boundaries
Luke reviewed the buyer-facing copy. Final copy leads with the recognizable failure modes and keeps the page scoped to one visible formula plus expected output notes. It avoids Google Sheets RANDARRAY claims, file upload, workbook-audit claims, guarantees, Microsoft affiliation, human review, same-day/PDF claims, instant/automatic fixes, exact-cause claims, whole-workbook claims, works-in-every-version claims, and privacy-superiority claims.

## Verification
- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `175/175`.
- `npm test` passed `183/183`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Public-copy tripwire scan on the generated page found no blocked terms.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /excel-randarray-not-working/` passed `16/16`.
- Production route became live on poll attempt 2 with HTTP `200`.
- Live desktop/mobile Chromium checks passed: correct title, H1, canonical URL, six Stripe checkout links, required RANDARRAY and volatility copy, no horizontal overflow, `0` console messages, and `0` page errors. Screenshots saved under `workspace/sheetpilot-workbench/output/playwright/excel-randarray-live/`.
- Production homepage returned HTTP `200` and includes `/excel-randarray-not-working/`.
- Production sitemap returned HTTP `200` and includes the new route.
- Actual Stripe checkout URL returned HTTP `200`.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget
Current cash balance remains `-$24.07`.
