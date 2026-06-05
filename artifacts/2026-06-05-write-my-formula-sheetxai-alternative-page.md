# Write My Formula SheetXAI Alternative Page

Date: 2026-06-05 02:25 UTC

## Outcome

Shipped `https://writemyformula.com/sheetxai-alternative/` as a no-spend comparison-intent page for users comparing SheetXAI-style spreadsheet AI workspaces but needing one Excel or Google Sheets formula, explanation, or repair.

The page frames Write My Formula as narrow by design and routes broader needs to SheetXAI-style tools: sidebar chat inside Excel or Google Sheets, PDF or image extraction, connected business apps, bulk data movement, analysis, content generation, and workflow automation.

## Evidence

- SheetXAI official homepage currently positions around plain-English spreadsheet tasks in Excel and Google Sheets, PDF/image extraction, spreadsheet automation, business connections, content generation, and launch via an extension/sidebar.
- SheetXAI official formula-generator page validates the category-specific formula-generation angle.
- Broader active category evidence came from AI Formula Generator, Sheeter, SheetAI, and SheetGPT.
- `https://sheetplus.ai/` currently resolves to a domain-for-sale page, so the run avoided building a fresh page around stale Sheet+ product claims.

Primary live references:
- `https://www.sheetxai.com/`
- `https://www.sheetxai.com/ai-formula-generator`
- `https://www.aiformulagenerator.com/`
- `https://sheeter.ai/`
- `https://sheetai.co/`
- `https://sheetgpt.pro/`

## Copy Guardrails

Luke reviewed the comparison-copy direction. Final copy stayed fit-based and avoided unsupported replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, instant/perfect-formula, privacy-superiority, upload support by Write My Formula, whole-workbook audit, exact-cause, human-review, same-day/PDF, and competitor-attack claims.

## Implementation

- Added `sheetxai-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card to `workspace/sheetpilot-workbench/index.html`.
- Regenerated all static SEO pages because the homepage card grid is embedded in generated routes.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke output at `workspace/sheetpilot-workbench/luke-sheetxai-alternative-page.md`.
- Committed and pushed `8a648e2 Add SheetXAI alternative page`.

## Verification

- `npm run build:seo && npm test` passed `122/122`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no new unsupported SheetXAI comparison claims.
- Local Chromium desktop/mobile checks passed with expected title, H1, canonical URL, six checkout links, no horizontal overflow, and no real console/page errors after filtering known local static-server API noise.
- Production route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks passed with expected title, H1, canonical URL, six checkout links, no horizontal overflow, and `0` console/page errors.
- IndexNow submission returned HTTP `200`.

## Permissions And Budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
