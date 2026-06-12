# Write My Formula Sourcetable Alternative Refresh

Date: 2026-06-12 02:30 UTC

## Result

Refreshed the existing `https://writemyformula.com/sourcetable-alternative/` buyer-intent page with current Sourcetable evidence and safer fit-based copy.

Nested app commit:
- `22ed6c20 Refresh Sourcetable alternative page`

## Live Evidence

Live research checked Sourcetable official surfaces and current third-party comparison evidence:
- `https://sourcetable.com/`
- `https://blog.sourcetable.com/introducing-pricing/`
- G2 Sourcetable alternatives/search result evidence

The refreshed page now anchors Sourcetable around AI spreadsheet/data analyst positioning, uploaded files, connected data, multi-tab analysis, charts, reports, SQL, Python, data science libraries, visualizations, files up to 10GB, and pricing-announcement figures of Free 30 AI messages, Pro `$20/user/month` with 500 AI messages, and Max `$200/user/month`.

## Public-Copy Scope

Luke reviewed the buyer-facing posture. Final copy sorts by job size: Sourcetable for whole-spreadsheet, file, connected-data, dashboard, chart, report, SQL, Python, data-science, and multi-tab analysis workflows; Write My Formula for one visible formula, rule, explanation, or repair in a browser tab.

The final page avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, file upload/reading by Write My Formula, workbook-wide analysis, human-review, same-day/PDF, price-attack, and competitor-attack claims.

## Changes

- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Regenerated `workspace/sheetpilot-workbench/sourcetable-alternative/index.html`.
- Updated focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy notes at `workspace/sheetpilot-workbench/luke-sourcetable-alternative.md`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `169/169`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Local Chromium desktop/mobile checks passed for the refreshed route with correct title/H1/canonical, six checkout links, June 12 Sourcetable evidence, pricing copy, no forbidden copy, and no horizontal overflow; local static server produced only expected `POST 501` noise.
- Production route, homepage link, sitemap entry, and actual Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks passed with zero console errors, zero page errors, no forbidden copy, and no horizontal overflow.
- IndexNow returned HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
