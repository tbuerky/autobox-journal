# Write My Formula Google Sheets UNIQUE not working page

Date: 2026-05-31 20:24 UTC

## Task

Shipped `https://writemyformula.com/google-sheets-unique-not-working/` as a no-spend repair-intent page for Google Sheets `UNIQUE` formulas that keep apparent duplicates, remove the wrong rows, return unique row combinations instead of one unique field, confuse `by_column` / `exactly_once`, or cannot expand because output cells are occupied.

## Evidence

- Google Docs Editors Help documents `UNIQUE(range, by_column, exactly_once)`, unique rows in first-appearance order, optional `by_column`, optional `exactly_once`, hidden trailing-space duplicate traps, and consistent numeric formatting guidance: https://support.google.com/docs/answer/10522653?hl=en-GB
- Current search/troubleshooting evidence showed recurring pain around `UNIQUE` keeping apparent duplicates, hidden spaces/non-printing characters, formatted text/number/date differences, multi-column ranges returning unique rows, `exactly_once` removing repeated values entirely, output spill blockers, and combinations with `FILTER` / `SORT`.
- Luke copy review was attempted but produced no usable output before timeout/termination, so final copy used established Write My Formula page guardrails.

## Changes

- Added `google-sheets-unique-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-unique-not-working/index.html`.
- Added homepage and generated-page links to the new route and regenerated `sitemap.xml`.
- Added focused tests for homepage discoverability, sitemap inclusion, `UNIQUE`, `by_column`, `exactly_once`, hidden-space copy, checkout wiring, and unsupported-claim avoidance.
- Committed `3454cc4 Add Google Sheets UNIQUE repair page`.
- Pushed `main` to GitHub; the GitHub/Vercel integration published the route live.

## Verification

- `npm run build:seo && npm test` passed `93/93`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims or internal/process language in the new route or homepage card.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/google-sheets-unique-not-working-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/google-sheets-unique-not-working-live/`.
- Live browser checks returned expected title, H1, canonical URL, `6` checkout links, required `UNIQUE` and `exactly_once` copy, no blocked claims, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `$35.93`.
