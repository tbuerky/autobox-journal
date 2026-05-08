# PAF — end-of-day production smoke (2026-05-08)

**Date:** 2026-05-08 02:19 UTC
**Run:** autonomous, single task
**Target:** https://profitafterfees.com (live apex)
**Harness:** `workspace/paf_smoke.mjs` (Playwright headless Chromium)
**Result:** **36 pass / 0 fail / 0 console errors**

## Why this move

Cadence-appropriate baseline-defending check on the earning asset. Last EOD smoke was 2026-05-07 10:20 UTC (~16h prior). PAF carries Google Ads + AdSense; silent regressions on the apex calculator or the conversion fire would burn ad spend without anyone noticing. Smoke is the cheapest evidence that the live earning surface is intact while Travis owns the active StrikeRewind testing window.

Both open gates (`LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`, `ADS DECISION: PAF SEARCH EXTEND TO 2026-05-21`) remain Travis-side. Reconciled at run start; no decision evidence in OWNER_MESSAGES / HANDOFF / BUDGET — both held.

## What was checked (36 assertions)

- Apex `/`: HTTP 200, `#calculator-form`, `listPrice` input
- Conversion fire: `gtag('event','conversion', AW-18121518600/WxyuCLjh56McEIjcgcFD)` fires exactly once after submit, stays at 1 across additional input (once-semantic)
- Result panel: net profit `$40.84`, revenue ex-VAT `$75.00`, Stripe fee `$2.91`, affiliate fee `$22.50`, verdict headline non-empty
- Calculator pages (200 + scenario CTA carries `/?listPrice=` deep link): `/profit-margin-calculator/`, `/selling-price-calculator/`, `/selling-price-markup-calculator/`, `/break-even-price-calculator/`, `/digital-product-pricing-calculator/`
- AI Model Pricing Index: 200, "Last verified May 6, 2026", all 6 model rows (Sonnet 4.6, Haiku 4.5, Opus 4.7, Gemini 2.5 Flash, Flash-Lite, Gemini 2.5 Pro)
- AI Feature Cost Calculator: 200
- Mobile 390px: no horizontal overflow, calculator form visible
- `/privacy/`: 200; `/ads.txt`: 200, contains `pub-3560388500961643`
- Console: zero unexpected errors

## Outcome

Live site healthy across the 36-assertion surface. No regressions vs prior EOD run. No deploy. No commit. No spend. Current cash balance: `$162.45`.

## Next autonomous-runnable steps if approvals don't land soon

1. StrikeRewind end-of-day smoke (≥12h cadence; last was 2026-05-07 20:18 UTC, comes due ~08:18 UTC).
2. `OptionsDataProvider` interface + fixture-backed implementation (additive scaffolding, no consumer-side change) — works regardless of which provider Travis picks.
3. Data-provider single-recommendation packet (Polygon vs Intrinio Bronze vs Massive) — only if Travis explicitly asks; he is currently weighing on his own and a packet now is pile-on.
4. PAF Google Ads close-out check — Travis-pulled numbers required.
