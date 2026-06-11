# Write My Formula Sheet Formula alternative page - 2026-06-11

## Task
Shipped `https://writemyformula.com/sheet-formula-alternative/` as a no-spend comparison-intent page for users comparing Sheet Formula but needing one Excel or Google Sheets formula written, explained, or fixed in a browser tab.

## Why this task
The current owner instruction asked for one revenue-focused task with live web validation, minimal human involvement, no spend, no permission-gated action, and config state updates before exit. Paid-search control and Fluent Forms reCAPTCHA remain gated, while the latest outreach categories are on cooldown. A new buyer-intent comparison page adds a public sales surface without spending money or crossing an owner gate.

## Live evidence used
Live research checked Sheet Formula's public site. The site currently redirects to a Google Sheets formula-generation page with one prompt box, generated output, and a copy-to-clipboard action. Its FAQ says the service is free but has usage limits because AI generations cost money; anonymous usage is limited by IP address and signed-in usage by email address. It also says signing in unlocks extras such as AI formula analysis, and it links to separate Google Sheets add-ons such as Sheet Automation, Sheet Notification, and Share Single Sheet.

## Output
- Added `sheet-formula-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/sheet-formula-alternative/index.html`.
- Added the homepage comparison card and regenerated the static comparison grids.
- Updated shared public copy to soften Stripe return wording and formula-check boundaries.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js`.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Committed and pushed nested app commit `9b9aea6a Add Sheet Formula alternative page`.
- Submitted the new route, homepage, and sitemap to IndexNow; response HTTP `200`.

## Copy boundaries
Luke reviewed the customer-facing copy posture. Final public copy frames Sheet Formula for a free Google Sheets formula-generator page, IP/email-based usage limits, sign-in extras, and separate Google Sheets add-ons. It frames Write My Formula for one visible formula, explanation, or repair in a browser tab. It avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, automatic insertion, Google Sheets add-on behavior, workbook reading/upload, exact-cause, human-review, same-day/PDF, and competitor-attack claims.

## Verification
- `npm run build:seo && npm test` passed `163/163`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy risk scan passed.
- Local `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /sheet-formula-alternative/` passed `16/16`.
- Local desktop/mobile Chromium checks passed with no horizontal overflow and only expected local static-server API/analytics `POST` misses.
- Production route returned HTTP `200` after Vercel deploy.
- Live homepage returned HTTP `200` and includes `/sheet-formula-alternative/`.
- Live sitemap returned HTTP `200` and includes `/sheet-formula-alternative/`.
- Actual Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct title, H1, canonical URL, six checkout links, Sheet Formula evidence copy, softened Stripe copy, no blocked copy, no horizontal overflow, `0` console errors, and `0` page errors.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget and gates
`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

`config/BUDGET.md` remains unchanged. Current cash balance remains `-$24.07`.
