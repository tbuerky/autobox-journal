# Write My Formula Excel REDUCE / SCAN Not Working Page - 2026-06-13

## Outcome

Shipped `https://writemyformula.com/excel-reduce-scan-not-working/` as a no-spend repair-intent page for Excel users whose `REDUCE` or `SCAN` formula returns `#VALUE!`, `#CALC!`, `#SPILL!`, `#NAME?`, a wrong initial accumulator value, a wrong final accumulator result, or an unexpected running array.

Nested app commit: `29ce33a8 Add Excel REDUCE SCAN repair page`.

## Why this task

The current owner prompt asked for one revenue-moving task, live web research, and no StrikeRewind/PAF default work. Paid-search changes remain gated, the Fluent Forms manual reCAPTCHA gate remains open, and delegated outreach categories remain cooling down until 2026-06-14 unless a relevant active prospect replies. A no-spend buyer-intent repair page was the best non-gated way to add another sales surface to the active Write My Formula lane.

## Evidence Used

- Microsoft REDUCE support: `https://support.microsoft.com/en-us/office/reduce-function-42e39910-b345-45f3-84b8-0642b568b7cb`
- Microsoft SCAN support: `https://support.microsoft.com/en-us/excel/scan-function`
- Microsoft Excel functions list: `https://support.microsoft.com/en-us/excel/excel-functions-by-category`

The page copy uses those sources to keep the repair surface narrow: REDUCE returns one accumulated result; SCAN returns intermediate accumulated results; both use `=REDUCE([initial_value], array, lambda(accumulator, value, body))` / `=SCAN([initial_value], array, lambda(accumulator, value, body))`; version support is framed as Microsoft 365 / Excel 2024 where appropriate.

## Changes

- Added `excel-reduce-scan-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage related-link card.
- Generated `workspace/sheetpilot-workbench/excel-reduce-scan-not-working/index.html`.
- Regenerated generated static pages and `sitemap.xml`.
- Added focused coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-excel-reduce-scan-not-working.md`.

Luke found no claim-risk issues and recommended copy tightening. Final copy avoids Google Sheets REDUCE/SCAN, workbook upload/audit, whole-workbook diagnosis, Microsoft affiliation, guarantees, human review, same-day/PDF, instant/one-click/automatic-fix, exact-cause, all-version, and handles-any-size claims.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `171/171`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Public-copy scan found no internal/process language or blocked claims on the new page/homepage.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /excel-reduce-scan-not-working/` passed `16/16`.
- Local desktop/mobile Chromium checks returned HTTP `200`, correct H1/canonical, six checkout links, `0` page errors, no unexpected console errors, and no horizontal overflow.
- Production route/home/sitemap/actual Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct H1/canonical, six checkout links, `0` console/page errors, and no horizontal overflow.
- IndexNow accepted route/home/sitemap with HTTP `200`.

## Non-actions

No ad settings, bids, budgets, checkout/payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, reCAPTCHA form submissions, public posts, bulk sends, destructive production changes, or spend changed.

Budget balance remains `-$24.07`.
