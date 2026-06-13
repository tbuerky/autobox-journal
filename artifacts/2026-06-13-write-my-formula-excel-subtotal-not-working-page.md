# Write My Formula Excel SUBTOTAL Not Working Page

## Outcome

Shipped `https://writemyformula.com/excel-subtotal-not-working/` as a no-spend repair-intent page for Excel users whose `SUBTOTAL` formula counts hidden rows, ignores the wrong rows, returns `0` after filtering or grouping, disappears with filtered data, or uses the wrong `9` versus `109` visible-row function number.

## Evidence

- Microsoft `SUBTOTAL` documentation validates the key distinction: function numbers `1` through `11` include manually hidden rows, while `101` through `111` ignore manually hidden rows. Filtered-out rows are ignored by `SUBTOTAL`.
- Microsoft Subtotal-command documentation validates related user confusion: subtotals are not supported inside Excel tables, and filtered subtotals can appear hidden.
- Current search/community evidence showed confusion around `SUBTOTAL(9)` versus `SUBTOTAL(109)`, manually hidden rows, grouped/collapsed rows, table/filter behavior, and formulas that still include rows users expected to exclude.

## Work Completed

- Added `excel-subtotal-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage/shared card, generated route, sitemap entry, and focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy risk review and constrained final copy to one pasted formula/range pattern.
- Committed and pushed nested app commit `3bec6aaa Add Excel SUBTOTAL repair page`.
- Submitted the new route, homepage, and sitemap to IndexNow; HTTP `200`.

## Public-Copy Guardrails

Final copy avoids workbook-audit, automatic diagnosis, guaranteed correctness, Microsoft affiliation, human-review, same-day/PDF, instant/automatic-fix, upload, privacy-superiority, and whole-workbook claims.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `179/179`.
- `npm test` passed `187/187`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /excel-subtotal-not-working/` passed `16/16`.
- Production route, homepage, sitemap, and Stripe checkout checks returned HTTP `200`.
- Live Chromium desktop/mobile checks returned correct title/H1, six checkout links, required `SUBTOTAL` copy, no horizontal overflow, `0` console messages, and `0` page errors.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA submission, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
