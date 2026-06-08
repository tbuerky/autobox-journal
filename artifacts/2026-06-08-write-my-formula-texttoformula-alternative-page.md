# Write My Formula TextToFormula Alternative Page

Date: 2026-06-08 20:24 UTC

## Task

Shipped a no-spend comparison-intent page for users comparing TextToFormula-style free formula converters but needing one Excel or Google Sheets formula, explanation, or repair with range context and paste checks.

Live URL: https://writemyformula.com/texttoformula-alternative/

## Why This Task

The current active lane is Write My Formula. Paid-search changes remain owner/account-gated, Fluent Forms remains blocked by manual reCAPTCHA, and the recent outreach categories are still in wait windows. A distinct buyer-intent comparison page was the best non-gated revenue motion.

## Live Research

TextToFormula's current public page presents it as a free AI Excel and Google Sheets formula generator that converts plain text, math equations, or queries into formulas. It shows a generated formula, copy button, explanation, and step-by-step usage guidance; says it works for Excel and Google Sheets; and says it works without signup, download, or installation.

Broader current search results show ongoing demand and competition around free AI Excel / Google Sheets formula generators, including TextToFormula, SheetGPT, FormulaZa, Formulr, Formula Bot, AI Formula Generator, Sheeter, and Excel Formula GPT.

## Output

- Added `texttoformula-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/texttoformula-alternative/index.html`.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy guidance at `workspace/sheetpilot-workbench/luke-texttoformula-alternative.md`.
- Committed and pushed nested app commit `20b438e1 Add TextToFormula alternative page`.

## Copy Boundaries

Luke reviewed the copy direction. Final copy stayed fit-based: TextToFormula for a free no-signup text-to-formula converter; Write My Formula for one write, explain, or fix workflow with visible formula context, range notes, and paste checks.

The page avoids unsupported replacement, better-than, official-affiliation, speed, accuracy, guarantee, privacy-superiority, automatic-fix, upload/whole-workbook support, exact-cause, human-review, same-day, and competitor-attack claims.

## Verification

- `npm run build:seo && npm test` passed `155/155`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Public-copy scan found no internal/process language on the new route or homepage card beyond legitimate product wording such as `runs per month`.
- Live route returned HTTP `200`.
- Live homepage returned HTTP `200` and includes `/texttoformula-alternative/`.
- Live sitemap returned HTTP `200` and includes `/texttoformula-alternative/`.
- Actual Stripe checkout URL returned HTTP `200`.
- Live route has `6` checkout links.
- Live desktop and mobile Chromium checks returned expected title, H1, canonical URL, TextToFormula detail copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

Screenshots and browser summary:

- `workspace/sheetpilot-workbench/output/playwright/texttoformula-alternative-live/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/texttoformula-alternative-live/mobile.png`
- `workspace/sheetpilot-workbench/output/playwright/texttoformula-alternative-live/summary.json`

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
