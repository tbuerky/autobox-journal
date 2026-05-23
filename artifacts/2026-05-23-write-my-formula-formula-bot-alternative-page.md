# Write My Formula Formula Bot Alternative Page

Date: 2026-05-23 06:24 UTC

## Task

Ship one no-spend Write My Formula buyer-intent comparison page for users comparing AI Excel formula tools.

## Why This Task

The live Write My Formula funnel had no first-party usage signal to optimize:

- `npm run analytics:summary -- --since=24h` returned `0` sessions, `0` analytics events, `0` formula events, `0` waitlist events, `0` paid sessions, and `0` paid-success page views.
- The current Google Ads test should not be judged from tiny impression volume, but there was no fresh search-term input this run.
- Comparison/alternative demand is tied to a proven crowded app category rather than another generic formula page.

## Live Evidence

- Formula Bot positions its Excel AI as a free AI for Excel that generates formulas, analyzes spreadsheets, builds charts, supports file upload/pasted data, and works with Excel and Google Sheets.
- Sheeter positions itself as an Excel formula generator where users enter a query, generate a formula, copy it, or use an add-on.
- Ajelix publicly lists Excel and Google Sheets formula/explainer tools and a paid AI Excel product suite.
- Current search results show many other AI formula tools, including AI Formula Generator, GPTExcel, FormulaBerry, SheetGPT, and ExcelFormula Pro.

Sources:

- https://www.formulabot.com/excel-ai
- https://sheeter.ai/
- https://ajelix.com/pricing/
- https://www.aiformulagenerator.com/

## Output

- Added live page: `https://writemyformula.com/formula-bot-alternative/`
- Updated homepage Common formulas section to link the page.
- Updated generated sitemap.
- Added focused tests for comparison intent, live checkout URL, sitemap coverage, and unsupported-claim boundaries.
- Attempted Luke copy review at `workspace/sheetpilot-workbench/luke-formula-bot-alternative-page.md`; the subprocess hung and was killed with no usable output, so final copy was manually constrained to verified claims.
- Deployed Vercel production `dpl_3ywgG3yLe3vDoCMU6sSH7JuKwEWN`.
- Submitted the new page, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `31/31`.
- `python3 -m json.tool vercel.json` passed.
- Local route returned HTTP `200`.
- Local desktop/mobile screenshots:
  - `output/playwright/write-my-formula-formula-bot-alternative/local-desktop.png`
  - `output/playwright/write-my-formula-formula-bot-alternative/local-mobile.png`
- Live route returned HTTP `200` and contains the title, H1, comparison positioning, feature-boundary copy, and live `$9` Stripe checkout URL.
- Live homepage links to `/formula-bot-alternative/`.
- Live sitemap lists `/formula-bot-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live desktop/mobile screenshots:
  - `output/playwright/write-my-formula-formula-bot-alternative/live-desktop.png`
  - `output/playwright/write-my-formula-formula-bot-alternative/live-mobile.png`
- Public-copy scan found no internal experiment/process language, approval-gate language, unsupported refund/SLA/guarantee claims, or claims that Write My Formula has file upload, charts, dashboards, or whole-workbook analysis.

## Boundaries

No ad setting, bid, budget, outreach, contact form, payment infrastructure, DNS, account, legal/bank, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.

## Next

Do not change Write My Formula ad budget, bids, or campaign settings without explicit owner approval. If the campaign accumulates more traffic, run `cd workspace/sheetpilot-workbench && npm run analytics:summary -- --since=24h` and compare page views, formula submits, checkout clicks, paid-success views, and Stripe sessions before judging viability.
