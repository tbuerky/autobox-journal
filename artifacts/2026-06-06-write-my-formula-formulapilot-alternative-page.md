# Write My Formula FormulaPilot Alternative Page

Date: 2026-06-06 14:26 UTC

## Result

Shipped a new no-spend comparison-intent page:

- Live URL: https://writemyformula.com/formulapilot-alternative/
- Commit: `e92c903 Add FormulaPilot alternative page`
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/formulapilot-alternative-live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/formulapilot-alternative-live-mobile.png`

The page targets users comparing FormulaPilot-style Excel and Google Sheets formula tools, but whose immediate problem is still one formula, one explanation, or one repair.

## Live Evidence Used

- FormulaPilot live homepage: https://formulapilot.com/
  - Current positioning: free Excel and Google Sheets AI formula generator.
  - Public feature evidence: no signup, copy-ready formula suggestion, explanation/notes, formula checker, Google Sheets generator, formula library, learn pages, error reference, function references.
  - Category evidence: Date & Time, Math & Statistics, Financial, Array Formulas, Data Cleaning, Text Manipulation, Conditional Logic, and Lookup & Reference.
- Formula Workspace live homepage: https://formulaworkspace.com/
  - Broader category evidence for focused generate/explain/fix formula work across Excel and Google Sheets.
- HelpFormula live homepage: https://helpformula.com/
  - Broader category evidence for AI Excel and Google Sheets formula generators, guest/free request patterns, localization, syntax validation, and saved-history positioning.

## Copy Direction

Luke reviewed the copy direction. Final public copy stayed fit-based:

- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair.
- Use FormulaPilot or a similar formula hub when the user wants a free no-signup generator, formula checker, Google Sheets generator, references, learning pages, or browsable formula libraries.

Avoided unsupported claims: replacement, better-than, official affiliation, partner, speed, accuracy, guarantee, instant/perfect formula, automatic fix, privacy superiority, upload/workbook audit, exact cause, human review, same-day/PDF, and competitor attacks.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/formulapilot-alternative/index.html`
- generated static SEO pages
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`

## Verification

- `npm run build:seo && npm test` passed `137/137`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked FormulaPilot claims or internal/process language in the new route/homepage.
- Local Chromium desktop/mobile checks:
  - HTTP `200`
  - expected title, H1, canonical URL
  - `6` checkout links
  - FormulaPilot evidence visible
  - no horizontal overflow
  - no page errors
  - expected static-server `POST /api/*` `501` noise only
- Production checks:
  - `https://writemyformula.com/formulapilot-alternative/` HTTP `200`
  - homepage HTTP `200` and links to `/formulapilot-alternative/`
  - sitemap HTTP `200` and includes the new route
  - live Stripe checkout HTTP `200`
  - production Chromium desktop/mobile checks returned `0` console messages, `0` page errors, no horizontal overflow, expected H1/title/canonical, `6` checkout links, and FormulaPilot evidence visible.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
