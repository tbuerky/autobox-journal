# Write My Formula Excel VSTACK / HSTACK Repair Page

## Task

Ship one no-spend buyer-intent repair page for Excel `VSTACK` and `HSTACK` formulas, without changing ads, payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, public posts, bulk sends, destructive production settings, or spend.

## Evidence

- Microsoft Support documents `VSTACK` as appending arrays vertically and notes that if an array has fewer columns than the maximum width, Excel returns `#N/A` in the additional columns.
- Microsoft Support's `#SPILL!` guidance documents blocked spill ranges, indeterminate/volatile spill sizes, Excel table limitations, merged-cell spill blockers, and worksheet-edge spill cases for dynamic-array formulas.
- Current search/forum evidence showed demand around `VSTACK`/`HSTACK` version availability, `#N/A` padding from uneven arrays, dynamic-array `#SPILL!` behavior, and users trying to combine ranges for reports.
- The existing Write My Formula site already has adjacent dynamic-array pages for `SORT`, `UNIQUE`, `FILTER`, `#SPILL!`, and `#CALC!`; `excel-vstack-hstack-not-working` filled a missing stacked-array slot.

Sources:

- Microsoft `VSTACK`: `https://support.microsoft.com/en-au/office/vstack-function-a4b86897-be0f-48fc-adca-fcc10d795a9c`
- Microsoft `#SPILL!`: `https://support.microsoft.com/en-us/office/-spill-error-out-of-memory-50e613d0-498a-4cd8-96ee-0846af48f411`
- Live search evidence included current indexed `VSTACK` / `HSTACK` troubleshooting around `#N/A`, `#SPILL!`, and version-support failures.

## Output

- Added `excel-vstack-hstack-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-vstack-hstack-not-working/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live desktop/mobile screenshots under:
  - `workspace/sheetpilot-workbench/output/playwright/excel-vstack-hstack-not-working-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-vstack-hstack-not-working-live/`
- Committed and pushed `26ce756 Add Excel VSTACK HSTACK repair page`.
- Live page: `https://writemyformula.com/excel-vstack-hstack-not-working/`

## Verification

- `npm run build:seo && npm test` passed `104/104`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language in the new route or homepage card.
- Luke reviewed the buyer-facing copy direction; no banned claims were found in the draft, and final copy avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click/automatic-fix, pay-before-answer, PDF, same-day, whole-workbook, whole-spreadsheet, and exact-cause claims.
- Local desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `VSTACK`/`HSTACK`/`#N/A padding`/`Excel version` copy, and no horizontal overflow. Local static-server `POST /api/*` `501` console noise was expected.
- Production route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `VSTACK`/`HSTACK`/`#N/A padding`/`Excel version` copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
