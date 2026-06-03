# Write My Formula Formulr alternative page - 2026-06-03

## Task

Shipped a no-spend comparison-intent page for users searching around `Formulr alternative`:

- Live URL: https://writemyformula.com/formulr-alternative/
- Commit: `8d70960 Add Formulr alternative page`
- Local/live screenshots: `workspace/sheetpilot-workbench/output/playwright/formulr-alternative-local/` and `workspace/sheetpilot-workbench/output/playwright/formulr-alternative-live/`

## Why this task

Open gates remained:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No canonical state showed either gate had cleared. The best non-gated revenue motion was another buyer-intent search surface in the active Write My Formula lane rather than paid-search changes, reCAPTCHA submission, StrikeRewind, PAF, or another template-vendor outreach touch.

## Live evidence

Live research validated Formulr as an active AI spreadsheet formula product:

- Formulr homepage: https://getformulr.app/
- Current page presents AI-generated Excel and Google Sheets formulas from plain English, with Generate, Explain, and Debug modes.
- Current page says it is powered by Gemini 2.5 Flash.
- Current page presents a free plan with 15 formula generations, 10 explanations, and 5 debugs per month.
- Current page presents a Pro launch price of `$4.99/month` after trial, with 500 formula generations plus unlimited explanations and debugging.

Additional category evidence:

- AI Formula Generator search result showed an active formula-generator category across Excel, Google Sheets, SQL, Formula Bot, GPTExcel, and ChatGPT-style alternatives.
- SheetGPT live page showed the broader category remains active, with Excel/Google Sheets formula generation, explanations, pricing, and broader data/chat/chart features.

## Public-copy guardrails

Luke reviewed the copy-risk direction. Useful guidance kept:

- Lead with trying the focused workbench, not attacking Formulr.
- Avoid price-per-run comparisons.
- Avoid saying range notes or paste checks are unique.
- Avoid no-signup claims beyond the two guest tries.
- Avoid speed, accuracy, success-rate, and team-credential claims.

Luke accidentally suggested `$4/month`; this was discarded. Final public copy uses the live Write My Formula price: `$9` for 500 runs per month in this browser.

Final copy stayed bounded to visible Write My Formula capability:

- one Excel or Google Sheets formula
- one formula explanation
- one formula repair
- range notes
- paste checks
- two guest tries before deciding whether to create an account

Final copy avoided unsupported replacement, better-than, official-affiliation, guarantee, privacy-superiority, speed, upload, whole-workbook, exact-cause, human-review, same-day/PDF, and automatic-fix claims.

## Output

Changed:

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- generated `workspace/sheetpilot-workbench/formulr-alternative/index.html`
- regenerated static SEO pages that inherit the shared homepage link
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-formulr-alternative-page.md`

Pre-existing `workspace/sheetpilot-workbench/README.md` drift was left unstaged and uncommitted.

## Verification

Local:

- `npm run build:seo && npm test` initially found one wording assertion mismatch.
- Final `npm test` passed `114/114`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked internal/process or unsupported comparison language.
- Local Chromium desktop/mobile checks returned HTTP `200`, expected title, H1, canonical URL, six checkout links, no blocked copy, no horizontal overflow, and no page errors. Local static-server `POST /api/*` `501` console noise was expected and did not occur live.

Deploy/live:

- Pushed `main` to GitHub; Vercel GitHub integration served the production route.
- Live route `https://writemyformula.com/formulr-alternative/` returned HTTP `200`.
- Live homepage returned HTTP `200` and includes `/formulr-alternative/`.
- Live sitemap returned HTTP `200` and includes `https://writemyformula.com/formulr-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, six checkout links, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the route, homepage, and sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget

Current cash balance remains `-$24.07`.
