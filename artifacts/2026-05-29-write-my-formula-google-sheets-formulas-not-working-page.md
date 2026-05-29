# Write My Formula Google Sheets formulas not working page - 2026-05-29

## Task
Ship one no-spend buyer-intent page for broad Google Sheets formula repair demand while outreach classes and owner/manual gates remained closed.

## Live research
- Google Sheets function list documents supported functions, function syntax, quoted alphabetic components, and error-checking helpers such as `ISERROR`, `ISNA`, `ISREF`, `ISFORMULA`, and `VALUE`: https://support.google.com/docs/table/25273?hl=en
- Google `ERROR.TYPE` maps common spreadsheet error values including `#VALUE!`, `#REF!`, `#NAME?`, `#NUM!`, `#N/A`, and other errors: https://support.google.com/docs/answer/3238305?hl=en
- Google `NA` docs state `#N/A` marks missing information and can halt downstream calculations: https://support.google.com/docs/answer/3093359?hl=en
- Current search evidence showed active repair demand around Google Sheets formulas not updating, showing as text, formula parse errors, invalid references, text-vs-number issues, locale separators, and wrong results.

## Output
- Added `https://writemyformula.com/google-sheets-formulas-not-working/`.
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Regenerated static SEO pages and `sitemap.xml`.
- Linked the new route from the homepage formula grid.
- Added focused content tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Luke copy direction saved at `workspace/sheetpilot-workbench/luke-google-sheets-formulas-not-working-copy.md`.
- Commit: `2a32fde Add Google Sheets formulas repair page`.
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-formulas-not-working/live-desktop.png` and `live-mobile.png`.

## Verification
- `npm run build:seo && npm test` passed `71/71`.
- `python3 -m json.tool vercel.json` passed.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-formulas-not-working/`.
- Live browser check returned expected title, H1, canonical URL, `6` checkout links, homepage link present, required `#ERROR!` and `commas or semicolons` copy, and `0` console warnings/errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and spend
`config/OPEN_GATES.md` remains unchanged with:
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
