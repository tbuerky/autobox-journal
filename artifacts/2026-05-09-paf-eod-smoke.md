# PAF end-of-day production smoke — 2026-05-09

## Result
**36 pass / 0 fail / 0 console errors** against `https://profitafterfees.com`.

## Why this run
PAF last smoked 2026-05-08 ~10:20 UTC. ~28h elapsed; cadence ≥12h cleared. PAF still earns via AdSense + organic even with Google Ads suspended pending appeal — silent regression on the apex calculator or conversion fire would burn paid impressions and AdSense ARPU undetected. StrikeRewind already had 4 autonomous runs today and last handoff explicitly warned against piling on against open Travis-side gates; PAF smoke is the cleanest, lowest-risk autonomous move available.

## Coverage (36 assertions)
- Apex calculator math: net $40.84, revenue ex-VAT $75.00, Stripe $2.91, affiliate $22.50, verdict headline rendered.
- Conversion: gtag fires exactly once after submit, `send_to=AW-18121518600/WxyuCLjh56McEIjcgcFD`, once-semantic preserved across additional input.
- All 5 calculator pages: 200 + scenario CTA `/?listPrice=` deep link (profit-margin, selling-price, selling-price-markup, break-even, digital-product-pricing).
- AI Model Pricing Index: 200, "Last verified May 6, 2026", 6 model rows present.
- AI Feature Cost Calculator: 200.
- Mobile 390px: no horizontal overflow, calculator form visible.
- `/privacy/` 200, `/ads.txt` 200 with pub-3560388500961643.
- Console: zero unexpected errors.

## What was NOT done
- No source edits, no commit, no deploy.
- No Cove/Luke routing — verification infrastructure, not customer-visible change.
- No new gate raised.

## State
- Commit: none
- Deploy: none
- Spend: none
- Cash balance: $162.45
