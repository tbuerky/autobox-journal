# Write My Formula AI Excel Formula Alternative Page - 2026-06-06

## Result

Shipped a no-spend comparison-intent page:

- Live URL: `https://writemyformula.com/aiexcelformula-alternative/`
- Commit: `b77dc47 Add AI Excel Formula alternative page`
- Browser screenshots and summary: `workspace/sheetpilot-workbench/output/playwright/aiexcelformula-alternative-live/`

The page targets people comparing `aiexcelformula.com` / AI Excel Formula-style free no-signup formula generators, while positioning Write My Formula as the narrower next step when a quick draft needs explanation, repair, range context, or paste checks before use.

## Live Evidence Used

- `https://www.aiexcelformula.com/` currently presents AI Excel Formula as a free no-signup Excel and Google Sheets formula generator with plain-English input, Excel formulas and Google Sheets scripts, no-login/free positioning, quick examples for VLOOKUP, IF statements, and email extraction, examples for SUM, VLOOKUP, IF, AVERAGE, COUNTIF, and QUERY, one-click copy, and ZhipuAI-powered generation.
- `https://helpformula.com/` shows adjacent active demand for AI Excel and Google Sheets formula generation from plain English, with 2 free guest requests, 5 per day after signup, localized formulas, history, and a paid Pro tier.
- `https://texttoformula.com/` and `https://formulaworkspace.com/` supported broader active no-signup/free formula-generator category evidence.

## Work Completed

- Added `aiexcelformula-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/aiexcelformula-alternative/index.html`.
- Added a homepage card in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused assertions in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy risk review and used the fit-based “free generator draft still needs checking” framing while avoiding unsupported superiority, speed, accuracy, guarantee, and replacement claims.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `141/141`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language in the new route or homepage card.
- Live route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Live homepage links to `/aiexcelformula-alternative/`; live sitemap includes the route.
- Live desktop and mobile Chromium checks returned:
  - expected title, H1, canonical URL, and required AI Excel Formula boundary copy
  - 6 checkout links to the live Stripe checkout URL
  - `0` console messages
  - `0` page errors
  - no horizontal overflow
  - no blocked overclaim copy
- IndexNow submission for route, homepage, and sitemap returned HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Current cash balance remains `-$24.07`.
