# Write My Formula Google Sheets Data Validation Formula Not Working Page

- Date: 2026-05-31 12:25 UTC
- Live URL: https://writemyformula.com/google-sheets-data-validation-formula-not-working/
- Commit: `7bd3b68 Add Google Sheets data validation repair page`
- Vercel deploy: `dpl_Hg1d1pK3DN4nwSWc3Kp5yj8icTsN`
- Cash spend: `$0`; current cash balance remains `$35.93`

## Task

Ship one no-spend buyer-intent page for Google Sheets data-validation custom formulas that warn instead of rejecting, reject valid entries, shift references after copying, or confuse dropdown-from-range criteria with TRUE/FALSE custom validation tests.

## Evidence Used

- Google Docs Editors Help documents in-cell dropdowns and data validation behavior, including dropdown criteria and choosing `Reject input` when entries outside the list should be blocked: https://support.google.com/docs/answer/186103
- Google Workspace Learning Center also documents `Show warning` versus `Reject input` for invalid dropdown/data-validation choices: https://support.google.com/a/users/answer/9604139
- Current search/community evidence showed recurring pain around data-validation custom formulas not saving, cross-sheet references, custom formulas needing TRUE/FALSE behavior, relative/top-left-cell reference confusion, and `Show warning` not blocking entries.

## Output

- Added `google-sheets-data-validation-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-data-validation-formula-not-working/index.html`.
- Regenerated SEO pages and `sitemap.xml`.
- Linked the route from the homepage and generated page grids.
- Added focused route/homepage/sitemap/overclaim coverage in `tests/content.test.js`.
- Attempted Luke review for buyer-facing copy direction, but the subagent command produced no usable output before timeout/termination. Final copy used the established Write My Formula page guardrails and avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Google partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, whole-sheet/full-sheet, partnership, and broad-audit claims.

## Verification

- First `npm run build:seo && npm test` found missing homepage wiring; after linking the route from `index.html`, the next run found a blocked-copy phrase (`full-sheet`) in the caveat text; after replacing it with `broad data-quality audit`, final `npm run build:seo && npm test` passed `89/89`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims in the new page or homepage card.
- Local Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-data-validation-local/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-data-validation-local/mobile.png`
- Local browser checks returned HTTP `200`, expected title/H1/canonical, `6` checkout links, required `Show warning versus Reject input`, `dropdown-from-range`, and TRUE/FALSE copy, no blocked-copy matches, no horizontal overflow, and expected static-server `POST /api/*` `501` noise only.
- Pushed `main` to GitHub and deployed production to Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live Chromium desktop/mobile screenshots captured:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-data-validation-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-data-validation-live/mobile.png`
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, homepage route inclusion, required `Show warning versus Reject input`, `dropdown-from-range`, and TRUE/FALSE copy, no blocked-copy matches, no horizontal overflow, `0` console errors, and `0` page errors.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Open gates remain unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
