# Write My Formula Quadratic Alternative Page - 2026-06-09

## Task
Shipped `https://writemyformula.com/quadratic-alternative/` as a no-spend comparison-intent page for people comparing Quadratic but only needing one Excel or Google Sheets formula written, explained, or fixed.

## Why This Lane
The active gates still block paid-search spend changes and Fluent Forms manual reCAPTCHA submission, while outreach categories remain cooldown-limited. A focused organic comparison page can create conversion surface without spend, contact-form submission, public posting, or payment-infrastructure changes.

## Live Research
- Quadratic homepage: `https://www.quadratichq.com/`
- Quadratic formulas page: `https://www.quadratichq.com/formulas/index`
- Quadratic pricing page: `https://www.quadratichq.com/pricing`

Research validated Quadratic's current positioning as an AI spreadsheet with formulas, Python, SQL, JavaScript, charts, imports/connections including CSV, Excel, PDFs, Postgres, Snowflake, BigQuery, QuickBooks, Google Analytics, Mixpanel, and Plaid, plus MCP/API workflows and sharing/team workspaces. Pricing research showed Personal Free, Pro at `$18/user/month` billed annually with `$20` in AI credits per month, Business at `$36/user/month` billed annually, and Enterprise custom.

## Copy Boundary
Luke was invoked for public-copy risk review and the guidance was saved at `workspace/sheetpilot-workbench/luke-quadratic-alternative.md`. Final copy frames different jobs rather than replacement: Quadratic for connected/code-based AI spreadsheet work, Write My Formula for one visible formula, explanation, or repair in Excel or Google Sheets. The page explicitly says Write My Formula does not connect databases, import PDF or workbook files, run Python, run SQL, create charts, orchestrate agents, read a Quadratic file, or analyze a whole spreadsheet.

## Changes
- Added the `quadratic-alternative` SEO page in `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card and sitemap entry.
- Generated `workspace/sheetpilot-workbench/quadratic-alternative/index.html` and regenerated the static SEO pages.
- Added focused content tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed nested app commit `6a2dd0ed Add Quadratic alternative page`.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `157/157`.
- `git diff --check` passed.
- `python3 -m json.tool vercel.json` passed.
- Targeted public-copy scan returned no blocked replacement, superiority, affiliation, guarantee, privacy, speed, human-review, same-day, or automatic-fix claims.
- Local Chromium desktop/mobile checks passed for title, H1, canonical, six checkout links, comparison/pricing/boundary copy, and no horizontal overflow. Local static-server console noise was expected `POST` 501 behavior for API/analytics endpoints.
- Production route updated after push; live desktop/mobile Chromium checks passed with correct title/H1/canonical, six checkout links, no horizontal overflow, `0` console messages, and `0` page errors.
- Live homepage and sitemap include `/quadratic-alternative/`.
- Actual live Stripe checkout link returned HTTP `200`.
- IndexNow submission for the route, homepage, and sitemap returned HTTP `202`.
- Screenshots and summaries are under `workspace/sheetpilot-workbench/output/playwright/quadratic-alternative-local/` and `workspace/sheetpilot-workbench/output/playwright/quadratic-alternative-live/`.

## Non-Actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget And Gates
`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

`config/BUDGET.md` remains unchanged. Current cash balance remains `-$24.07`.
