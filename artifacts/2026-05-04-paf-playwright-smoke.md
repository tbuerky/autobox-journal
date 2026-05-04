# PAF live-site Playwright smoke — 2026-05-04

## Why this run

Fourth autonomous run of 2026-05-04. One open gate (`TESTING COMPLETE: STRIKEREWIND`, owner-side, marketing freeze active) — every StrikeRewind move is testing-gated, so no autonomous push there. The sharpest non-StrikeRewind move was a quality-control gap on the live PAF site:

- PAF Search ads run through 2026-05-18 at $1.47 CPC. Every paid click lands on the live `/` calculator or one of the 5 calculator pages.
- PAF has 78/78 source-tree content tests but **zero live-runtime calculator verification**. A silent regression at deploy time (form not rendering, calc.js loading order off, JS error on submit, mobile overflow) would not show up in any existing test — only when a customer or Travis stumbled on it.
- StrikeRewind got a Playwright smoke 2026-05-04. PAF was overdue for the same defensive coverage on a property already receiving paid traffic.

This run builds the missing harness, runs it, and saves the results as a re-runnable defense for every future PAF deploy.

## What shipped

`workspace/paf_smoke.mjs` — 33 assertions across 9 live URLs, modeled directly on `workspace/strikerewind_smoke.mjs`. Final run: **33 pass / 0 fail / 0 console errors** against `https://profitafterfees.com`.

### Coverage

1. **Apex calculator math (live engine)** — load `/`, click `Recalculate` with default inputs, verify the live `#results` panel produces the exact numbers the engine math predicts: net profit `$40.84`, revenue ex-VAT `$75.00`, Stripe fee `$2.91`, affiliate fee `$22.50`. Verdict headline non-empty (`"You keep $40.84 from this sale."`). This is the first live-runtime calculator-correctness check on PAF.
2. **Calculator pages × 5** — `/profit-margin-calculator/`, `/selling-price-calculator/`, `/selling-price-markup-calculator/`, `/break-even-price-calculator/`, `/digital-product-pricing-calculator/`. Each: HTTP 200 + scenario CTA links to `/?listPrice=...` with URL params (the actual user journey from a paid-traffic landing through to the live calculator).
3. **AI Model Pricing Index freshness contract** — HTTP 200 + `Last verified May 4, 2026` present (verifies today's earlier deploy is live) + 6 model rows present by name.
4. **AI Feature Cost Calculator** — HTTP 200.
5. **Mobile 390×844** — no horizontal overflow on `/`, calculator form visible.
6. **Ad ecosystem prerequisites** — `/privacy/` 200, `/ads.txt` 200 + canonical `pub-3560388500961643` line.
7. **Console errors** — zero unexpected errors across the run.

### Captured artifacts

- `artifacts/2026-05-04-paf-playwright-smoke/01-apex-desktop.png`
- `artifacts/2026-05-04-paf-playwright-smoke/02-apex-result.png` (calculator output)
- `artifacts/2026-05-04-paf-playwright-smoke/03-apex-mobile.png`
- `artifacts/2026-05-04-paf-playwright-smoke/summary.json`

### Reproducer

```
cd workspace
OUT_DIR="../artifacts/$(date +%F)-paf-playwright-smoke" node paf_smoke.mjs
```

Override `BASE_URL` for staging probes. Cheap to run on every deploy (single chromium, ~10s).

## Deliberately did NOT

- Route through Cove/Luke. Test infrastructure, not design/copy judgment.
- Add Playwright assertions for every page on the sitemap (19 pages). Smoke scope: paid-traffic landing pages + the apex calculator engine. Wider sweep is audit drift.
- Fill the form with non-default values to exercise the engine across input ranges. The engine has unit tests in `tests/`; the smoke just needs to confirm form → engine → render works on a live build.
- Click outbound ad units or AdSense slots. AdSense is approved, owner-side data lives in dashboards.
- Raise a new gate. No owner action required.
- Touch StrikeRewind. Marketing freeze in place.

## State files

- `TODO.md` new `[DONE]` line at top of immediate-priority list.
- `RUNLOG.md`, `SCORECARD.md`, `HANDOFF.md` appended.
- `OPEN_GATES.md` unchanged. `TESTING COMPLETE: STRIKEREWIND` remains the only gate.
- `BUDGET.md` unchanged. No spend, balance `$162.45`. Render starter still accruing ~$0.23/day toward end-of-cycle invoice.

## What this defends

- A future PAF deploy that breaks form rendering, calc.js loading order, mobile layout, or ads.txt → caught immediately on a `node paf_smoke.mjs` run instead of a customer or Travis discovering it.
- Travis-confirmed PAF Search ads will continue running through 2026-05-18 with paid clicks landing on this code path. The smoke is a small daily ritual that costs nothing and catches regressions on a money-receiving conversion path.
- Future deploys can use `npm test && node workspace/paf_smoke.mjs` as a real two-stage gate: source-tree correctness + live-runtime correctness.

## Cash balance

`$162.45` (unchanged). Render starter for StrikeRewind still accruing ~$0.23/day; first invoice at end of cycle.
