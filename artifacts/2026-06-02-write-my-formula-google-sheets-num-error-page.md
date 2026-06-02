# Write My Formula Google Sheets #NUM! Error Page

## Task

Ship one no-spend buyer-intent repair page for Google Sheets formulas returning `#NUM!`, without changing ads, payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, public posts, bulk sends, destructive production settings, or spend.

## Evidence

- Google Docs Editors Help `ERROR.TYPE` documents `#NUM!` as a Google Sheets error value mapped to error type `6`.
- Google Docs Editors Help confirms Sheets formulas/functions are entered directly in cells and users can open function reference material from the function help box.
- Current search/forum evidence showed real repair demand around Google Sheets `#NUM!` in XIRR/financial formulas, invalid row/index/random-selection positions, users trying to hide `#NUM!` with `IFERROR`, and numeric inputs that are not usable as numbers.
- The existing Write My Formula site already has adjacent Sheets error pages for `#REF!`, `#VALUE!`, `#N/A`, `#DIV/0!`, and `#NAME?`; `google-sheets-num-error` filled the missing error cluster slot.

Sources:

- Google `ERROR.TYPE`: `https://support.google.com/docs/answer/3238305`
- Google formulas/functions help: `https://support.google.com/docs/answer/46977`
- Search evidence included current indexed Google Sheets `#NUM!` discussions such as XIRR and out-of-range row/index cases.

## Output

- Added `google-sheets-num-error` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-num-error/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live desktop/mobile screenshots under:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-num-error-local/`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-num-error-live/`
- Committed and pushed `80a175c Add Google Sheets NUM error repair page`.
- Live page: `https://writemyformula.com/google-sheets-num-error/`

## Verification

- `npm run build:seo && npm test` passed `103/103`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language in the new route or homepage card.
- Local desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `#NUM!`/`XIRR`/`RANDBETWEEN` copy, no horizontal overflow, and no page errors. Local static-server `POST /api/*` `501` console noise was expected.
- Production route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `#NUM!`/`XIRR`/`RANDBETWEEN` copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
