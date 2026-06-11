# Write My Formula Formula.dog alternative page - 2026-06-11

## Outcome

Shipped `https://writemyformula.com/formula-dog-alternative/` as a no-spend comparison-intent page for users comparing Formula.dog but needing one Excel or Google Sheets formula, explanation, or repair with visible headers, sample rows, and range notes.

Nested app commit: `372b2a8b Add Formula.dog alternative page`

## Live evidence used

- Formula.dog public page: `https://formula.dog/` says Formula.dog has fetched formulas since 2022, accepts plain-English spreadsheet problems, returns Excel or Google Sheets formulas, offers the first five formulas per day free with no sign-up, knows VBA, and says there are no sales calls.
- Current Write My Formula production page: `https://writemyformula.com/` still shows two guest tries, free email access, and `$9` for `500` runs/month stored in this browser.

## Positioning

Luke reviewed the customer-facing comparison direction in `workspace/sheetpilot-workbench/luke-formula-dog-alternative.md`. Final copy uses a fit-based comparison:

- Formula.dog: five free formulas per day, no sign-up, VBA help, formula-bot style.
- Write My Formula: one formula, explanation, or repair in a browser tab with optional headers, sample rows, range hints, paste checks, and a `$9` burst path for `500` runs/month.

The page avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, workbook reading/upload, automatic insertion, human-review, same-day/PDF, price-attack, and competitor-attack claims.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/formula-dog-alternative/index.html`
- regenerated static pages so existing card grids include the new route
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-formula-dog-alternative.md`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `167/167`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy regression test passed for the new route and homepage card.
- Local Chromium desktop/mobile checks passed for the new route and homepage; local-only analytics/API `POST` 501 messages were expected from `python -m http.server`.
- Production HTTP checks returned `200` for:
  - `https://writemyformula.com/formula-dog-alternative/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - actual Stripe checkout URL `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Production Chromium desktop/mobile checks found correct title, H1, Formula.dog evidence copy, homepage link, six checkout links, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
