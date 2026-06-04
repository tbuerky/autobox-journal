# Write My Formula FormulaWiz Alternative Page

Date: 2026-06-04 02:22 UTC

## Task

Ship one no-spend comparison-intent surface for Write My Formula: `https://writemyformula.com/formulawiz-alternative/`.

## Why This Task

Paid search control remains gated by `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`, and Fluent Forms remains blocked by manual reCAPTCHA. Recent outreach touched several template/resource targets, so the highest-leverage non-gated move was another buyer-intent page in the active AI spreadsheet formula category.

## Live Evidence

- FormulaWiz is live at `https://formulawiz.vercel.app/`.
- FormulaWiz positions itself as a natural-language spreadsheet formula generator for Excel, Google Sheets, and Airtable.
- FormulaWiz exposes Generate, Explain, and Debug modes.
- FormulaWiz states it has 5 free formulas per month with no account and Pro plans starting at `$6.99/month`.
- FormulaWiz claims multi-platform output across Excel, Sheets, and Airtable, so the Write My Formula page is positioned as a different fit, not as a replacement or superior product.
- Broader active category evidence came from current formula-generator surfaces including Sheeter and AI Formula Generator.

Sources:
- `https://formulawiz.vercel.app/`
- `https://sheeter.ai/`
- `https://www.aiformulagenerator.com/`

## Output

- Added `formulawiz-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/formulawiz-alternative/index.html`.
- Linked the route from the homepage card grid.
- Regenerated generated SEO pages and `sitemap.xml`.
- Added focused content regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Created Luke copy-risk review at `workspace/sheetpilot-workbench/luke-formulawiz-alternative-page.md`.
- Committed and pushed `6bf9494 Add FormulaWiz alternative page`.

## Copy Guardrails

Luke recommended a fit-based frame: FormulaWiz covers Excel, Sheets, and Airtable; Write My Formula is focused on one Excel or Google Sheets formula problem. Final public copy avoided:

- better-than or replacement claims
- official-affiliation or partner claims
- price-comparison claims
- accuracy, speed, guarantee, or automatic-fix claims
- upload, whole-workbook, human-review, same-day, or PDF claims
- stale quoted FormulaWiz numbers on the public page

## Verification

- `npm run build:seo && npm test` passed `115/115`.
- Public-copy scan found no internal/process language in the new route or homepage card.
- Public overclaim scan found no blocked FormulaWiz comparison claims.
- Live route returned HTTP `200`.
- Live homepage returned HTTP `200` and links to `/formulawiz-alternative/`.
- Live sitemap returned HTTP `200` and includes `https://writemyformula.com/formulawiz-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop and mobile checks found expected title/H1, `6` checkout links, `0` console errors, `0` page errors, and no horizontal overflow.
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/formulawiz-alternative-live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/formulawiz-alternative-live-mobile.png`
- IndexNow submission returned HTTP `200`.

## Gates And Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance: `-$24.07`.
