# 2026-05-05 morning production smoke verification

## Verdict

Clean overnight. Both live properties survived the gap from yesterday's end-of-day smoke (2026-05-04) without regressions.

- **PAF — `https://profitafterfees.com`**: **33 pass / 0 fail / 0 console errors**
- **StrikeRewind — `https://www.strikerewind.com`**: **22 pass / 0 fail**

## Why this run

Two open gates entering this run, both unchanged from end of 2026-05-04:

- `TESTING COMPLETE: STRIKEREWIND` — Travis-side
- `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` — Travis-side

The 8th run on 2026-05-04 explicitly endorsed re-running the smoke verification when ≥12h has elapsed and gates have not moved (vs. piling another StrikeRewind packet or PAF audit on top). That window has now closed: it is 2026-05-05, no fresh `OWNER_MESSAGES.md` entries, marketing freeze still in effect, gates still owner-side.

A morning verification — first run after a full overnight gap — also catches a different class of failure than end-of-day: anything that broke during low-traffic hours (Render free-tier sleep recovery, DNS, certificates, Vercel build drift). It defends the active PAF Google Search ads ($1.47 CPC, running through 2026-05-18) where a silent regression on the apex calculator would burn paid-traffic dollars before anyone noticed.

## PAF results — 33/33

Reproducer: `cd workspace && OUT_DIR="../artifacts/2026-05-05-morning-smoke/paf" node paf_smoke.mjs`

- Apex calculator engine: load `/`, click `Recalculate` with default inputs, `#results` produces exact engine-predicted numbers.
  - Net profit `$40.84`, revenue ex-VAT `$75.00`, Stripe fee `$2.91`, affiliate fee `$22.50`.
  - Verdict headline live: `"You keep $40.84 from this sale."`
- All 5 calculator pages HTTP 200 + scenario CTA links to `/?listPrice=...` with full param-encoded scenarios.
- `/ai-model-pricing-index/` HTTP 200 + `Last verified May 4, 2026` + 6 model rows by name.
- `/ai-feature-cost-calculator/` HTTP 200.
- Mobile 390×844: no horizontal overflow + form visible.
- `/privacy/` HTTP 200, `/ads.txt` HTTP 200 + canonical `pub-3560388500961643` line.
- Zero unexpected console errors.

3 full-page screenshots + summary.json: `artifacts/2026-05-05-morning-smoke/paf/`.

## StrikeRewind results — 22/22

Reproducer: `cd workspace && OUT_DIR="../artifacts/2026-05-05-morning-smoke/strikerewind" node strikerewind_smoke.mjs`

- Landing renders.
- Analyze AAPL: 2441-char body with EV%, current price, strategy matrix.
- Nav active color `rgb(34, 197, 94)` on `/analysis/AAPL`.
- `/analysis/ZZZZZ`: error state with `Could not load`, ticker name in heading, Back button present, Back navigates to `/dashboard`.
- Hunt / Watch / Account tabs all non-blank.
- Account renders FREE/STANDARD/PRO plan cards.
- Mobile 390×844: no horizontal overflow.

8 full-page screenshots + summary.json: `artifacts/2026-05-05-morning-smoke/strikerewind/`.

## Delta vs. yesterday's end-of-day smoke

Identical pass counts. Identical engine numbers on PAF. Identical content on StrikeRewind (Analyze AAPL still 2441 chars; Account still renders all three plan cards). No drift, no regression, no new console errors.

## Recommendation — operating cadence

**No new gate raised this run.** Two gates remain:

- `TESTING COMPLETE: STRIKEREWIND` — single highest-leverage block on every StrikeRewind revenue move (marketing freeze lift, X launch post, Polygon greenlight). Travis runs the playbook (`artifacts/2026-05-03-strikerewind-testing-playbook.md`, ~36 min) against the now-Playwright-verified live site. Reply: `TESTING COMPLETE: STRIKEREWIND — all pass` or a fix list.
- `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` — closes on `LAUNCH POSTURE: HOLD FOR POLYGON` / `LAUNCH POSTURE: EARLY ACCESS` / `LAUNCH POSTURE: TIGHTEN COPY`. Recommended: TIGHTEN COPY. Canonical packet: `artifacts/2026-05-04-strikerewind-data-honesty-scope-correction.md`.

Next-run guidance if both gates stay open: prefer bounded backend hygiene flagged in the 10th run's handoff (clean `ivService.ts` dead `yahoo-finance2` import; correct `STATE.md` line 25 — there is no `OptionsDataProvider` interface in code, but `PriceDataProvider` was added in commit `095c96b`). Both are autonomous, concrete, useful regardless of LAUNCH POSTURE outcome, and ready to ship as a single small commit. Avoid: another smoke run inside the same 12h window (would be drift), another StrikeRewind packet (testing-gated), another PAF audit (78/78 source + 33/33 live tests already green).

## Suggested post copy

> Morning smoke check — PAF 33/33 (0 console errors) and StrikeRewind 22/22, no regressions overnight. Both gates still owner-side: `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE`. Ready when you are. Artifact: `artifacts/2026-05-05-morning-smoke.md`.

Cash balance: `$162.45`. No spend, no deploy, no source-tree change.
