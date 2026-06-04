# Write My Formula Formula Bot alternative refresh - 2026-06-04 20:22 UTC

## Task
Refresh the existing `https://writemyformula.com/formula-bot-alternative/` comparison-intent page so it matches Formula Bot's current broader spreadsheet AI positioning while keeping Write My Formula framed as a narrow one-formula workbench.

## Why this task
- Paid-search control remains gated by `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`.
- Fluent Forms remains gated by manual reCAPTCHA.
- Consulting/support-service outreach is wait-locked until `2026-06-07 16:20 UTC` unless a relevant prospect replies first.
- The existing Formula Bot page was older and generic. It said "broader spreadsheet-analysis suite" but did not name the current Formula Bot workflows users are likely comparing against.

## Live research used
- Formula Bot Excel AI page: https://www.formulabot.com/excel-ai
  - Formula Bot currently positions as a free AI for Excel that generates formulas, analyzes spreadsheets, and builds charts from chat.
  - The page describes Excel/Google Sheets support, upload or paste-data workflows, formula writer/checker/explainer, data analysis, charts, and downloadable chart/analysis outputs.
- Formula Bot platform/pricing page: https://www.formulabot.com/?view=features
  - The platform surface includes dashboards, data visualization, data transformation, reports, text analysis, connectors, web scraping, embeddable analytics, and data security claims.
  - Current visible paid tiers include Starter at `$18/mo`, Max at `$29/user/mo`, and Enterprise at `$149/user/mo`, with file uploads, automated dashboards, AI Actions, add-ons, shared workspaces, and embeds.
- Ten Times AI Formula Bot listing: https://tentimes.ai/app/formula-bot/
  - Third-party category evidence describes Formula Bot as generating Excel formulas, Google Sheets formulas, and SQL queries from plain English with formula explanations and VBA macro generation.
- AI Formula Generator comparison/category evidence: https://www.aiformulagenerator.com/
  - Current category evidence shows competing AI formula tools explicitly comparing Formula Bot, GPT Excel, and ChatGPT for Excel/Google Sheets/SQL formula work.

## Public copy direction
Luke reviewed the buyer-facing framing in `workspace/sheetpilot-workbench/luke-formula-bot-refresh.md`.

Final framing:
- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair.
- Use Formula Bot or a similar broader spreadsheet AI suite when the buyer needs file upload, workbook analysis, charts, dashboards, connectors, SQL, VBA, Apps Script, PDF conversion, data chat, regex, or automated reporting.
- Avoided replacement, better-than, official-affiliation, Formula Bot partner, speed, accuracy, guarantee, instant/perfect-formula, privacy-superiority, upload-support, whole-workbook audit, exact-cause, human-review, same-day, and stale/attack claims.

## Changes shipped
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` for `formula-bot-alternative`:
  - title/H1 now focus on "one formula problem";
  - description/lede now separate one-formula work from broader Formula Bot workflows;
  - `bestFor`, `steps`, `copyChecks`, `useWhen`, and `notWhen` now reflect the current Formula Bot comparison boundary.
- Updated `workspace/sheetpilot-workbench/index.html` homepage card for Formula Bot alternative with safe shared copy that avoids terms blocked by unrelated generated-page overclaim scans.
- Regenerated all static SEO pages because the homepage card grid is embedded into every generated page.
- Added/updated focused assertions in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `b684db6 Refresh Formula Bot alternative page`.

## Verification
- `npm run build:seo && npm test` passed `121/121`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked Formula Bot overclaims in `formula-bot-alternative/index.html` or `index.html`.
- Live route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live route served the new title and homepage card text.
- Live Chromium desktop and mobile checks saved under `workspace/sheetpilot-workbench/output/playwright/formula-bot-alternative-refresh/`:
  - title: `Formula Bot Alternative for One Formula Problem | Write My Formula`
  - H1: `A Formula Bot alternative for one formula problem.`
  - canonical: `https://writemyformula.com/formula-bot-alternative/`
  - checkout links: `6`
  - expected Formula Bot boundary copy present
  - `0` console messages
  - `0` page errors
  - no horizontal overflow
- IndexNow accepted `formula-bot-alternative`, homepage, and sitemap with HTTP `200`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- `config/OPEN_GATES.md` remained unchanged.
- `config/BUDGET.md` remained unchanged. Current cash balance remains `-$24.07`.
