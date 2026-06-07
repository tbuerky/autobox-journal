# Write My Formula GenieSheet Alternative Page

Date: 2026-06-07 12:23 UTC

## Task
Ship one no-spend buyer-intent page for users comparing GenieSheet-style AI formula generators but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

Live URL: https://writemyformula.com/geniesheet-alternative/

Commit: `044c5a4 Add GenieSheet alternative page`

## Why This Task
Open gates remained unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

At run time (`2026-06-07 12:17 UTC`), the consulting/support-service outreach wait had not cleared (`2026-06-07 16:20 UTC`), and marketplace/app-template outreach is wait-locked until `2026-06-10 08:17 UTC` unless a relevant prospect replies. A distinct comparison-intent page was the strongest non-gated revenue motion.

## Live Evidence
- GenieSheet currently presents itself as an AI-powered formula generator for Excel and Google Sheets. Its public page describes plain-English prompts, formula explanations, copy-and-use flow, `1,265+` formula examples, no credit card requirement, a free plan, and `3` free prompts daily. It also publishes speed, accuracy, privacy, and refund claims that were treated as GenieSheet-side context only, not copied into Write My Formula promises.
- FormulaWiz shows the broader formula-generator market remains active across Excel, Google Sheets, and Airtable, with generate/explain/debug modes, a formula library, a free monthly allowance, and paid plans.
- Formulr shows adjacent current demand for Excel and Google Sheets generate, explain, and debug workflows, with free monthly quotas and a paid plan.

Sources:
- https://geniesheet.app/
- https://formulawiz.vercel.app/
- https://getformulr.app/

## Output
- Added `geniesheet-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/geniesheet-alternative/index.html`.
- Added the GenieSheet card to the homepage comparison grid, which propagated to generated SEO-page grids.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy direction at `workspace/sheetpilot-workbench/luke-geniesheet-alternative.md`.

Public copy stayed fit-based and avoided unsupported replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, instant/perfect-formula, automatic-fix, privacy-superiority, upload/whole-workbook support, exact-cause, human-review, same-day/PDF, cheaper-than, more-accurate, faster, and competitor-attack claims.

## Verification
- `npm run build:seo && npm test` passed `145/145`.
- `python3 -m json.tool vercel.json` passed.
- Targeted public-copy scan found no internal/process language or blocked GenieSheet claims in the new route or homepage card.
- Local Chromium desktop/mobile checks passed for `/geniesheet-alternative/`: HTTP `200`, expected title/H1/canonical, six live Stripe checkout links, GenieSheet boundary copy present, no horizontal overflow, and no page errors. Local console noise was expected static-server `POST` 501.
- Live route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks passed: expected title/H1/canonical, six checkout links, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- Live homepage includes the GenieSheet card.
- Live sitemap includes `https://writemyformula.com/geniesheet-alternative/`.
- IndexNow POST returned HTTP `200` for the new route, homepage, and sitemap.

## Non-Actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
