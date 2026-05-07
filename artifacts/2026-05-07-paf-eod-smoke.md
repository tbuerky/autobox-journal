# PAF end-of-day production smoke — 2026-05-07

**Run:** 3 of 2026-05-07, fired ~10:19 UTC.
**Target:** `https://profitafterfees.com`.
**Harness:** `workspace/paf_smoke.mjs`.
**Result:** 36 pass / 0 fail / 0 console errors.
**Outputs:** `artifacts/2026-05-07-paf-playwright-smoke/` (3 fullpage PNGs + `summary.json`).

## Why this move now

PAF morning smoke last ran 2026-05-06 12:17 UTC (22h ago) — past the ≥18h cadence threshold prior-run handoff named as the eligibility window. Run 1 of 2026-05-07 02:17 UTC produced an owner-decision packet (Google Ads extend); run 2 of 2026-05-07 ~08:25 UTC fixed StrikeRewind watchlist and cleared `TESTING COMPLETE`. With both Travis-side gates parked, the eligible bounded autonomous move is the cadence smoke that defends the live AdSense surface + the paid-traffic conversion path PAF Search Ads will reuse once `ADS DECISION: PAF SEARCH EXTEND TO 2026-05-21` clears.

## Coverage

- Apex `/` HTTP 200 + `#calculator-form` + `listPrice` input present.
- Conversion gtag fires exactly once after submit, `send_to` matches `AW-18121518600/WxyuCLjh56McEIjcgcFD`, stays at one call after additional input (Once semantic).
- Engine produces `$40.84` net / `$75.00` revenue ex-VAT / `$2.91` Stripe / `$22.50` affiliate; verdict headline `"You keep $40.84 from this sale."`
- 5 calc pages 200 + scenario CTAs link to `/?listPrice=...`: `/profit-margin-calculator/`, `/selling-price-calculator/`, `/selling-price-markup-calculator/`, `/break-even-price-calculator/`, `/digital-product-pricing-calculator/`.
- `/ai-model-pricing-index/` 200 + `Last verified May 6, 2026` + 6 model rows (Sonnet 4.6, Haiku 4.5, Opus 4.7, Gemini 2.5 Flash, Flash-Lite, Gemini 2.5 Pro).
- `/ai-feature-cost-calculator/` 200.
- Mobile 390px no horizontal overflow, calculator form visible.
- `/privacy/` 200, `/ads.txt` 200 + `pub-3560388500961643`.

Identical pass-content to 2026-05-06 morning smoke — nothing regressed across the day.

## Deliberately NOT done

- No source edits — smoke clean, nothing to fix.
- No deploy — no diff.
- No Cove / Luke routing — test infrastructure only, no public copy or layout changed.
- No new gate — autonomous and complete.
- No StrikeRewind smoke re-run — run 2's hardened harness ran 2h ago at 29/29 pass.
- No backup-file deletion (`config/TODO.md.bak-pre-cleanup`, `config/HANDOFF.md.bak-pre-relocate`) — both StrikeRewind smokes have passed today; could ship next run as the standalone cleanup move.

## Cash balance

`$162.45`. No spend. Render starter accruing ~$0.23/day.
