# Write My Formula Google Sheets #N/A error page - 2026-05-29

## Task
Ship one no-spend buyer-intent page for Google Sheets `#N/A` formula repair.

## Gate reconciliation
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` remains owner/account-gated.
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` remains manual reCAPTCHA-gated.
- Training/resource outreach remains wait-locked until `2026-06-01 10:20 UTC`.
- Consulting/support-service outreach remains wait-locked until `2026-06-01 16:20 UTC`.
- Add-in-vendor outreach remains wait-locked until `2026-05-30 22:20 UTC`.
- The Someka marketplace/app-template thread remains in an active reply wait.

## Evidence
- Google Docs Editors Help documents `NA` as returning the `#N/A` error and notes that `ISNA` and `ISERROR` recognize it as an error value: https://support.google.com/docs/answer/3093359
- Google Docs Editors Help for `VLOOKUP` references `IFNA` as a way to replace a `#N/A` result after a lookup: https://support.google.com/docs/answer/3093318
- Live search evidence showed current repair demand around Google Sheets `#N/A`, lookup values that appear to exist, FILTER no-match cases, text-vs-number mismatches, hidden/extra spaces, wrong ranges, and fallback misuse.

## Output
- Added `https://writemyformula.com/google-sheets-na-error/`.
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`, generated the new static route, regenerated SEO pages and `sitemap.xml`, and linked the route from the homepage/generated page grids.
- Added focused tests for homepage link, sitemap inclusion, checkout links, page copy, and overclaim exclusions.
- Saved Luke copy review at `workspace/sheetpilot-workbench/luke-google-sheets-na-error-page.md` and screenshots under `workspace/sheetpilot-workbench/output/playwright/google-sheets-na-error/`.
- Commit: `21c6c1a Add Google Sheets NA error page`.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `74/74`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or prohibited claims on the new page/homepage except the existing implementation class name `seo-detail`.
- Local Chromium render returned expected title, H1, canonical URL, `6` checkout links, required `Use IFNA for expected missing matches` copy, and only expected static-server API `501` console noise.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-na-error/`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, required IFNA copy, overclaim scan pass, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and spend
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
