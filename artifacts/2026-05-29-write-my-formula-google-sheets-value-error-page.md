# Write My Formula Google Sheets #VALUE! error page - 2026-05-29

## Task
Ship one no-spend buyer-intent page for Google Sheets `#VALUE!` formula repair.

## Gate reconciliation
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` remains owner/account-gated.
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` remains manual reCAPTCHA-gated.
- Training/resource outreach remains wait-locked until `2026-06-01 10:20 UTC`.
- Consulting/support-service outreach remains wait-locked until `2026-06-01 16:20 UTC`.
- Add-in-vendor outreach remains wait-locked until `2026-05-30 22:20 UTC`.
- The Someka marketplace/app-template thread remains in an active reply wait.

## Evidence
- Google `ERROR.TYPE` maps `#VALUE!` as a recognized Sheets error value.
- Google `VALUE` converts strings that Sheets understands as date, time, or number values and returns an error when a string cannot be converted.
- Google `ISERROR` treats `#VALUE!` as one of the formula errors it can detect.
- Live search evidence showed current repair demand around `VALUE parameter cannot be parsed`, math on text, date/text conversion, imported values stored as text, and wrong argument types.

## Output
- Added `https://writemyformula.com/google-sheets-value-error/`.
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`, generated the new static route, regenerated SEO pages and `sitemap.xml`, and linked the route from the homepage/generated page grids.
- Added focused tests for homepage link, sitemap inclusion, checkout links, page copy, and overclaim exclusions.
- Saved Luke copy review at `workspace/sheetpilot-workbench/luke-google-sheets-value-error-page.md` and screenshots under `workspace/sheetpilot-workbench/output/playwright/google-sheets-value-error/`.
- Commit: `f441196 Add Google Sheets VALUE error page`.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `73/73`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or prohibited claims on the new page/homepage.
- Local Chromium render returned expected title, H1, canonical URL, `6` checkout links, required `VALUE parameter cannot be parsed` copy, and only expected static-server API `501` console noise.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-value-error/`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, required copy, overclaim scan pass, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and spend
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
