# Write My Formula Google Sheets date formula not working page

Date: 2026-05-30 18:25 UTC

## Outcome

Shipped a new no-spend repair-intent page:

- `https://writemyformula.com/google-sheets-date-formula-not-working/`
- Commit: `7aa81cc Add Google Sheets date repair page`
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-date-formula-not-working/local-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-date-formula-not-working/local-mobile.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-date-formula-not-working/live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-date-formula-not-working/live-mobile.png`

## Why this task

The add-in-vendor outreach wait had not cleared yet, consulting/training outreach waits remain open until 2026-06-01, the Google Ads broadening import is still owner/account-gated, and the Fluent Forms contact path is blocked by manual reCAPTCHA. The best non-gated revenue motion was another high-intent Write My Formula page aimed at a concrete repair problem: Google Sheets date formulas that fail because date text cannot be parsed, locale settings disagree with the text format, date criteria compare text instead of real dates, `QUERY` needs a date literal, or a converted date still displays as a serial number.

## Evidence used

- Google Docs Editors Help `DATEVALUE` documentation: `DATEVALUE` converts known date strings to date values; understood formats depend on region/language settings; it returns integers that can be formatted as dates; some date formats are not understood by Google Sheets. Source: https://support.google.com/docs/answer/3093039
- Google Sheets function list: `DATE(year, month, day)` and `DATEVALUE(date_string)` are date functions, with `DATEVALUE` converting a known-format date string to a date value. Source: https://support.google.com/docs/table/25273
- Current troubleshooting evidence showed demand around Google Sheets `QUERY` date literals, including the visible error pattern that date literals should be `yyyy-MM-dd`. Source: https://stackoverflow.com/questions/72898999/google-sheets-query-syntax-where-between-two-dates-that-are-variables

## Work performed

- Added `google-sheets-date-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added generated detail content covering `DATEVALUE`, imported text dates, locale ambiguity, `QUERY` date literals, serial-number display, and date criteria in `SUMIFS`, `COUNTIFS`, `FILTER`, and `SORT`.
- Added the route to the homepage link grid and regenerated all static SEO pages plus `sitemap.xml`.
- Added content tests for homepage inclusion, sitemap inclusion, checkout wiring, and overclaim avoidance.
- Invoked Luke for public-facing copy direction, used the error-led framing, and rejected unsupported free/no-cost, browser-local, guarantee, upload, whole-sheet, same-day/PDF, official-affiliation, human-review, instant, and automatic-repair claims.

## Verification

- `npm run build:seo && npm test` initially found one assertion mismatch; after copy/test alignment, `npm test` passed `83/83`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no unsupported claims in the new route or homepage card.
- Local HTTP checks returned `200` for the new route, homepage, and sitemap; homepage and sitemap included the route.
- Local browser checks captured desktop/mobile screenshots; no horizontal overflow. Expected local static-server `POST /api/*` `501` errors appeared because Python's static server does not implement production APIs.
- Pushed commit `7aa81cc` to `main`; Vercel/GitHub production served the new route.
- Live checks returned HTTP `200` for route, homepage, sitemap, and Stripe checkout; homepage and sitemap include the new route; the route includes the `DATEVALUE` copy.
- Live Chromium checks on desktop and mobile returned expected title, H1, canonical URL, `6` checkout links, required `DATEVALUE` and `yyyy-mm-dd` copy, unsupported-claim pass, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the new route, homepage, and sitemap with HTTP `200`.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. `config/OPEN_GATES.md` remains unchanged. Current budget balance remains `$35.93`.
