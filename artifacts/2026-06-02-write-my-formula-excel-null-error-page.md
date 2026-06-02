# Write My Formula Excel #NULL! Error Repair Page

## Task

Ship one no-spend buyer-intent page for Excel users searching because a formula returns `#NULL!` after a space, comma, colon, or range-intersection mistake.

## Evidence

- Microsoft Support documents `#NULL!` as an Excel error that appears when a formula specifies an intersection of two areas that do not intersect.
- Microsoft Support's broader formula-error guidance lists `#NULL!` among formula error values and frames formula errors as issues users need to detect and repair.
- Current search evidence showed live troubleshooting demand around `#NULL!` formulas, especially accidental spaces where users meant commas or colons, non-overlapping intersections, and confusion because the error is rarer than `#VALUE!`, `#REF!`, or `#N/A`.
- Luke reviewed the public-copy direction. Final copy used his plain-language framing around "a space where a comma or colon belonged" while avoiding his unsafe assumptions about email delivery and frequency claims.

Sources:

- Microsoft Support, Correct a #NULL! error: `https://support.microsoft.com/en-au/office/correct-a-null-error-11a15515-5df3-4a82-899e-e4c0070ea9c4`
- Microsoft Support, Detect formula errors in Excel: `https://support.microsoft.com/en-us/office/detect-errors-in-formulas-3a8acca5-1d61-4702-80e0-99a36a2822c1`

## Output

- Shipped page: `https://writemyformula.com/excel-null-error/`
- Commit: `6f0ed29 Add Excel NULL error repair page`
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`, generated `workspace/sheetpilot-workbench/excel-null-error/index.html`, regenerated generated SEO pages and `sitemap.xml`, added a homepage link card, and added focused content tests.
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-null-error-live/desktop.png` and `mobile.png`.

## Verification

- `npm run build:seo && npm test` passed `102/102`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or blocked overclaim phrases.
- GitHub push to `main` completed and Vercel production served the route.
- Live route returned HTTP `200`.
- Live homepage includes the new route; live sitemap includes the new route; live Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, required `#NULL!` copy, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the page, homepage, and sitemap with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
