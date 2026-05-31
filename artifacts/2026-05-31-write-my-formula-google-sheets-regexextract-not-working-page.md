# Write My Formula Google Sheets REGEXEXTRACT repair page

Date: 2026-05-31 16:22 UTC

## Task

Shipped a no-spend repair-intent page for Google Sheets `REGEXEXTRACT` formulas that return `#N/A`, fail because the pattern does not match, extract too much text, spill unexpected capture groups, choke on numeric input, or use regex syntax that works elsewhere but not in Google Sheets.

Live URL: https://writemyformula.com/google-sheets-regexextract-not-working/

## Evidence

- Google Docs Editors Help documents `REGEXEXTRACT(text, regular_expression)`, first matching substring behavior, capture groups returning multiple results, RE2 usage with a Unicode character-class exception, and the text-only input / text-output constraint.
- Current troubleshooting evidence showed repeated pain around `#N/A` no-match errors, rigid patterns, escaping literal punctuation, greedy matches, RE2 lookaround/lookbehind limitations, capture groups spilling columns, number input type errors, and `IFERROR` / `ARRAYFORMULA` wrapper mistakes.
- Luke reviewed buyer-facing copy direction and flagged the strongest angle: mirror the exact repair query, avoid tutorial sprawl, be precise about RE2 limits, and avoid unsupported speed, guarantee, data-access, or broad-fix claims.

## Changes

- Added `google-sheets-regexextract-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-regexextract-not-working/index.html`.
- Added homepage and generated-page links to the new route and regenerated `sitemap.xml`.
- Added focused tests for homepage discoverability, sitemap inclusion, REGEXEXTRACT / RE2 copy, checkout wiring, and unsupported-claim avoidance.
- Committed `dd173c2 Add Google Sheets REGEXEXTRACT repair page`.
- Pushed `main` to GitHub and deployed Vercel production `dpl_5RKhS614fT36drTYXnLR5Vvqk8Bg`.

## Verification

- `npm run build:seo && npm test` passed `91/91`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims in the new route or homepage card.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/google-sheets-regexextract-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, required `REGEXEXTRACT`, `RE2`, and `lookbehind` copy, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `$35.93`.
