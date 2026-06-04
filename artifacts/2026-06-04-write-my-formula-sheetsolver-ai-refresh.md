# Write My Formula SheetSolver AI alternative refresh - 2026-06-04 22:23 UTC

## Task
Refresh the existing `https://writemyformula.com/sheetsolver-ai-alternative/` comparison-intent page so it matches SheetSolver AI's current broader spreadsheet-workflow positioning while keeping Write My Formula framed around one Excel or Google Sheets formula, explanation, or repair.

## Why this task
- Paid-search control remains gated by `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`.
- Fluent Forms remains gated by manual reCAPTCHA.
- The existing SheetSolver AI page was generic and did not reflect the current SheetSolver AI surface around optional upload/context, prompt-to-sheet generation, PDF/invoice extraction, and export workflows.

## Live research used
- SheetSolver AI: https://www.sheetsolverai.com/
  - Current indexed copy positions SheetSolver AI as an Excel formula generator and Google Sheets formula bot.
  - Current visible product claims include Excel and Google Sheets formula generation, optional sheet/screenshot upload for tailored formulas, prompt-to-sheet generation, PDF/invoice table extraction, Excel/Google Sheets export, formula explanations, and a Pro plan with higher monthly formula usage.
- SheetXAI formula generator category evidence: https://www.sheetxai.com/ai-formula-generator
  - Current category evidence shows formula-generator tools positioning around natural-language Excel and Google Sheets formulas, nested/lookup/conditional formulas, and broader AI formula workflows.
- AI Formula Generator category evidence: https://www.aiformulagenerator.com/
  - Current category evidence shows active competition across Excel formulas, Google Sheets formulas, SQL, file context, templates, bulk generation, VBA, and Apps Script.

## Public copy direction
Luke reviewed the buyer-facing framing and flagged the important risk: do not present Write My Formula as merely "less." Present it as a focused workbench for one formula-sized answer, and do not imply SheetSolver requires upload because upload appears to be optional.

Final framing:
- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair.
- Use SheetSolver AI or a similar broader spreadsheet workspace when the buyer wants optional sheet/screenshot upload, prompt-to-sheet generation, PDF/invoice extraction, Excel or Sheets export, data chat, dashboards, charts, workbook-wide analysis, or higher-volume formula workflows.
- Avoided replacement, better-than, official-affiliation, partner, guarantee, instant/perfect-formula, automatic-fix, human-review, privacy-superiority, "SheetSolver makes you upload", bloated/cluttered/overbuilt, and unsupported speed/accuracy claims.

## Changes shipped
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` for `sheetsolver-ai-alternative`:
  - title/H1 now focus on "one formula problem";
  - lede, intent, `bestFor`, `copyChecks`, `useWhen`, and `notWhen` now reflect SheetSolver AI's broader optional upload, prompt-to-sheet, PDF/invoice extraction, export, and analysis boundary.
- Updated the homepage card for SheetSolver AI alternative with safe generic copy that does not leak `upload` or `PDF` terms into every generated page's overclaim scans.
- Regenerated all static SEO pages because the homepage card grid is embedded into every generated page.
- Updated focused assertions in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `62ed558 Refresh SheetSolver AI alternative page`.

## Verification
- `npm run build:seo && npm test` passed `121/121`.
- `python3 -m json.tool vercel.json` passed.
- Targeted public-copy scan passed for `sheetsolver-ai-alternative/index.html` and `index.html`.
- Production route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Production route served the refreshed title, H1, boundary copy, homepage card copy, and checkout URL.
- Live Chromium desktop and mobile checks saved under `workspace/sheetpilot-workbench/output/playwright/sheetsolver-ai-refresh-live/`:
  - title: `SheetSolver AI Alternative for One Formula Problem | Write My Formula`
  - H1: `A SheetSolver AI alternative for one formula problem.`
  - canonical: `https://writemyformula.com/sheetsolver-ai-alternative/`
  - checkout links: `6`
  - expected SheetSolver AI boundary copy present
  - homepage card copy present
  - `0` console messages
  - `0` page errors
  - no horizontal overflow
- IndexNow accepted `sheetsolver-ai-alternative`, homepage, and sitemap with HTTP `200`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- `config/OPEN_GATES.md` remained unchanged.
- `config/BUDGET.md` remained unchanged. Current cash balance remains `-$24.07`.
