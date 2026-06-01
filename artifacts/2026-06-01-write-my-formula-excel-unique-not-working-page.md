# Write My Formula Excel UNIQUE Not Working Page

Date: 2026-06-01 08:24 UTC

## Outcome

Shipped `https://writemyformula.com/excel-unique-not-working/` as a no-spend repair-intent page for Excel `UNIQUE` formulas that keep apparent duplicates, return unexpected rows, show `#SPILL!`, confuse `by_col`, or use `exactly_once` when the user expected a normal distinct list.

Commit: `027278f Add Excel UNIQUE repair page`

Screenshots:
- `workspace/sheetpilot-workbench/output/playwright/excel-unique-not-working-local/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-unique-not-working-local/mobile.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-unique-not-working-live/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-unique-not-working-live/mobile.png`

## Evidence

Live research used:
- Microsoft Support `UNIQUE` function documentation: `https://support.microsoft.com/en-gb/office/unique-function-c5ab87fd-30a3-4ce9-9d1a-40204fb85e1e`
- Current search evidence around `UNIQUE` duplicates, `#SPILL!`, hidden spaces/non-printing characters, text-number/date differences, multi-column row uniqueness, `exactly_once` confusion, and version support.

The page is intentionally bounded to a typed one-formula repair path. It avoids unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, and whole-spreadsheet claims.

Luke reviewed the buyer-facing copy direction in `workspace/sheetpilot-workbench/luke-excel-unique-page.md`; the final copy used the practical `UNIQUE` failure modes but did not keep the stronger "specific reason" promise.

## Changes

- Added `excel-unique-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-unique-not-working/index.html`.
- Linked the route from the homepage and generated page grids.
- Regenerated `sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Pushed `main` to GitHub, which triggered the Vercel production integration.
- Submitted page, homepage, and sitemap to IndexNow.

## Verification

- `npm run build:seo && npm test` passed `97/97`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan passed for the new route.
- Local Chromium desktop/mobile checks passed with expected static-server `POST /api/*` `501` noise only, no horizontal overflow, required `UNIQUE`, `exactly_once`, `#SPILL!`, and multi-column copy present, and six checkout links.
- Live route returned HTTP `200`.
- Live homepage returned HTTP `200` and includes `/excel-unique-not-working/`.
- Live sitemap returned HTTP `200` and includes `https://writemyformula.com/excel-unique-not-working/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, six checkout links, required copy, no blocked-copy matches, no horizontal overflow, and zero console/page errors.
- IndexNow returned HTTP `200`.

## Gates and Spend

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

`config/OPEN_GATES.md` remains:
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Current cash balance remains `$35.93`.
