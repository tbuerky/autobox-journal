# Write My Formula Excel Date Formula Not Working Page

- Date: 2026-05-31 14:25 UTC
- Live URL: https://writemyformula.com/excel-date-formula-not-working/
- Commit: `353350f Add Excel date formula repair page`
- Vercel deploy: `dpl_4L21syZL7mRErrZwF3wgmazXjC6k`
- Cash spend: `$0`; current cash balance remains `$35.93`

## Task

Ship one no-spend buyer-intent page for Excel date formulas failing because imported dates are text, day/month order is ambiguous, `DATEVALUE` returns `#VALUE!`, date serials display instead of formatted dates, or `DATEDIF`, `TODAY`, `SUMIFS`, `COUNTIFS`, and `FILTER` compare the wrong value type.

## Evidence Used

- Microsoft Support documents `DATEVALUE` `#VALUE!` failures when the date text format conflicts with system Date and Time settings: https://support.microsoft.com/en-au/office/how-to-correct-a-value-error-in-the-datevalue-function-d17c72f0-8829-482f-a334-14c4f124876e
- Microsoft Support documents `DATE` returning the serial number for a date and notes that Excel stores dates as sequential serial numbers: https://support.microsoft.com/en-us/office/date-function-e36c0c8c-4104-49da-ab83-82328b832349
- Microsoft Support documents date-system differences and serial-number behavior in Excel: https://support.microsoft.com/en-us/office/date-systems-in-excel-e7fe7167-48a9-4b96-bb53-5612a800b487
- Microsoft Support documents date-difference calculations with `DATEDIF` and `TODAY`: https://support.microsoft.com/en-us/office/calculate-the-difference-between-two-dates-8235e7c9-b430-44ca-9425-46100a162f38
- Current search/community evidence showed ongoing repair demand around text dates, `DATEVALUE` returning `#VALUE!`, regional date settings, serial-number confusion, and formulas comparing date values incorrectly.

## Output

- Added `excel-date-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-date-formula-not-working/index.html`.
- Regenerated SEO pages and `sitemap.xml`.
- Linked the route from the homepage repair grid.
- Added focused homepage, route, sitemap, and overclaim coverage in `tests/content.test.js`.
- Invoked Luke for public-copy review and incorporated the useful direction while softening unsupported DATEDIF wording.

## Verification

- `npm run build:seo && npm test` passed `90/90`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, or whole-spreadsheet claims in the new page. Benign `locale/local` substring matches were reviewed manually.
- Playwright CLI wrapper was attempted, but its default Chrome channel was missing at `/opt/google/chrome/chrome`; screenshots and browser assertions used the installed Playwright Chromium binary.
- Local Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/excel-date-formula-not-working-local/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/excel-date-formula-not-working-local/mobile.png`
- Local browser checks returned HTTP `200`, expected title/H1/canonical, checkout links, required `DATEVALUE`, serial-number, `DATEDIF`, and `SUMIFS`/`COUNTIFS`/`FILTER`/`TODAY` copy, no blocked-copy matches, and no horizontal overflow. Static-server `POST /api/*` `501` noise was expected.
- Pushed `main` to GitHub and deployed production to Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/excel-date-formula-not-working-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/excel-date-formula-not-working-live/mobile.png`
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, checkout links, required date-formula copy, no blocked-copy matches, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Open gates remain unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
