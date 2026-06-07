# Write My Formula Homepage Entry Simplification - 2026-06-07

## Task
Use the fresh Excel Spreadsheet Service feedback to reduce homepage entry friction. Paul Deaton said the Write My Formula GUI felt like looking for a needle in a haystack; this run shipped a smaller first-screen change instead of sending another consulting/support prospect email.

## Shipped
- Rewrote the homepage hero to lead with `Stuck on a formula? Paste it here.`
- Removed the redundant `Request / Formula request` header from the input panel.
- Kept Write / Explain / Fix and Excel / Google Sheets controls, but made mode selection the first control.
- Made the main prompt the dominant visible input.
- Collapsed table rows, range, and function hint behind `Add your data (optional)`.
- Added `Try:` before examples so a stuck user sees valid prompts without reading a field list.
- Moved the browser trial counter beside the submit button.
- Added mode-specific submit text and formula labels.

## Live Research Used
Current formula-generator surfaces still lead with the simple plain-English input pattern:
- SheetGPT presents plain-English Excel/Google Sheets formula generation with quick examples and a direct generate flow: https://sheetgpt.pro/
- Formulr positions around describing a spreadsheet task in plain English and toggling Excel vs Google Sheets: https://getformulr.app/
- AI Formula Generator presents Excel, Google Sheets, and SQL generation from plain-English requirements: https://www.aiformulagenerator.com/

This supported the decision to make Write My Formula's first visible action a single obvious prompt rather than a multi-field form.

## Files Changed
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/styles.css`
- `workspace/sheetpilot-workbench/app/app.js`
- `workspace/sheetpilot-workbench/tests/content.test.js`

Nested app commit: `f43d3b4 Simplify homepage formula entry`, pushed to `the-shepherd-stack/sheetpilot-workbench`.

## Verification
- `npm test` passed `146/146`.
- Local Chromium desktop and mobile checks passed:
  - new H1 present
  - one write textarea visible by default
  - optional context closed by default
  - Fix mode shows `Paste the formula that isn't working`
  - no horizontal overflow
  - no page errors
- Live homepage updated at `https://writemyformula.com/`.
- Live Chromium desktop and mobile checks passed:
  - H1: `Stuck on a formula? Paste it here.`
  - optional context closed by default
  - Explain mode switches to formula input and submit label
  - `6` checkout links present
  - no horizontal overflow
  - `0` console messages and `0` page errors
- IndexNow submission for `https://writemyformula.com/` returned HTTP `200`.

Screenshots:
- `workspace/sheetpilot-workbench/output/playwright/homepage-entry-simplification/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/homepage-entry-simplification/mobile.png`
- `workspace/sheetpilot-workbench/output/playwright/homepage-entry-simplification/live-desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/homepage-entry-simplification/live-mobile.png`

## Non-actions
No new prospect outreach, ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
