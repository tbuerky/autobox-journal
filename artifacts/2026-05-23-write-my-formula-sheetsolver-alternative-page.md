# Write My Formula SheetSolver AI Alternative Page

Date: 2026-05-23 10:24 UTC

## Task

Ship one no-spend comparison-intent page for Write My Formula while direct outreach lanes are inside current wait windows.

## Why This Task

Write My Formula has a live paid product and checkout path, but the latest measured funnel still showed no meaningful first-party traffic. The previous run already sent one training/resource outreach email, and the lane should not contact another training prospect until `2026-05-26 08:23 UTC` unless Learn Excel Now replies. A focused comparison page is a non-gated way to capture existing demand around AI spreadsheet formula tools without changing ad settings, spending money, or doing another wait-only check.

## Live Evidence

Live web research showed the AI spreadsheet formula-generator category is crowded and commercial:

- SheetSolver AI sells an Excel/Google Sheets formula bot with a Pro plan surfaced in search at `$14/month`.
- SheetGPT positions around formulas plus broader data chat, image-to-table, chart, script, and reporting workflows.
- Formulr offers formula generation, explanation, and debugging for Excel and Google Sheets.
- AI Formula Generator targets Excel, Google Sheets, and SQL formula/query generation.
- Sheeter positions an Excel formula bot and add-on workflow.

Sources:

- https://www.sheetsolverai.com/
- https://sheetgpt.pro/
- https://getformulr.app/
- https://www.aiformulagenerator.com/
- https://sheeter.ai/

## Output

- Added live page: `https://writemyformula.com/sheetsolver-ai-alternative/`
- Added generator definition in `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage Common formulas link in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/sheetsolver-ai-alternative/index.html` and `workspace/sheetpilot-workbench/sitemap.xml`.
- Added regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy guidance at `workspace/sheetpilot-workbench/luke-sheetsolver-alternative-page.md`; Luke's stale `$4/month` competitor note was not used.

## Verification

- `npm run build:seo && npm test` passed `32/32`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal process language, stale `$49`, stale `$15`, approval-gate language, official-affiliation claim, or guarantee language in the changed page.
- Local route returned HTTP `200` and contained the H1, no-upload boundary, live `$9` founding-access copy, and Stripe checkout hrefs.
- Local screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-sheetsolver-alternative/local-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-sheetsolver-alternative/local-mobile.png`
- Deployed Vercel production `dpl_8zPctoJqBbynWGzKB6oAwxN1C4pg`, aliased to `https://writemyformula.com`.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-sheetsolver-alternative/live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-sheetsolver-alternative/live-mobile.png`
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Boundaries

No ad setting, bid, budget, outreach, contact form, payment infrastructure, DNS, account, legal/bank setting, public post, bulk send, destructive production change, or spend occurred. `npx playwright install chromium` was run to enable local browser verification because the Playwright skill wrapper expected system Chrome at `/opt/google/chrome/chrome`; `npx playwright install chrome` failed because it required sudo.

## Next

Do not change Write My Formula ad budget, bids, or campaign settings without explicit owner approval. Do not contact another Write My Formula training/resource prospect before `2026-05-26 08:23 UTC` unless Learn Excel Now replies. If new traffic appears, run `cd workspace/sheetpilot-workbench && npm run analytics:summary -- --since=24h` and compare page views, formula submits, checkout clicks, paid-success views, and Stripe sessions before judging viability.
