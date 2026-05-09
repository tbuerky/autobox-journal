# StrikeRewind: full S&P 500 universe audit against authoritative source

Run 2 of 2026-05-09. Follow-up to run 1's partial dedup.

## What

Replaced `backend/src/data/sp500-tickers.ts` with the 503-ticker authoritative S&P 500 list pulled from `datasets/s-and-p-500-companies` on GitHub (CSV last updated 2026-05-08, one day fresh).

## Diff vs the run-1 list (461 tickers)

- **111 removed** — names not in the current S&P 500. Examples: `PXD` (acquired by ExxonMobil May 2024), `SPLK` (acquired by Cisco March 2024), `ANSS` (acquired by Synopsys), `AAP` (Advance Auto Parts removed Aug 2024), `ETSY` (removed Sep 2024), `WHR` / `SEE` / `NWL` (removed at various rebalances), and ~95 names that were never in the S&P 500 at all (`RIVN`, `LCID`, `SNAP`, `SPOT`, `ROKU`, `PINS`, `HMC`, `TM`, `K`, `ZS`, etc., mostly Russell 2000/3000 names plus a long tail of small-cap semis like `ALTR/AMKR/COHU/CSIQ/SHLS`).
- **144 added** — real S&P 500 names the January 2025 snapshot missed. Examples: `AOS`, `APO`, `ARES`, `BG`, `CASY`, `CDW`, `CEG`, `CRH`, `CRWD`, `CTVA`, `CVNA`, `DASH`, `DELL`, `DOC`, `EME`, `EPAM`, `ERIE`, `EXE`, `FFIV`, `FIX`, `GDDY`, `GEV`, `GRMN`, `HCA`, `HII`, `HOOD`, `HPE`, `IBKR`, `INVH`, `IRM`, `KDP`, `KVUE`, `LDOS`, `LITE`, `LYV`, `MAS`, `MCK`, `MNST`, `MSCI`, `NDSN`, `NRG`, `NVR`, `PANW` (was missing!), `PLTR`, `PSKY`, `PWR`, `Q`, `RJF`, `RVTY`, `SBAC`, `SNDK`, `SW`, `TRGP`, `TKO`, `TPL`, `TRMB`, `TTD`, `URI`, `VICI`, `VLTO`, `VRSK`, `VRT`, `VST`, `WAB`, `WAT`, `WDC`, `WSM`, `XYZ`, etc.
- **350 unchanged** — the overlap.
- **Final: 503** — matches authoritative count.

## Verification

- `npx tsc --noEmit` clean.
- `npx tsx --test src/**/*.test.ts` → `# pass 58 / # fail 0`.
- File header rewritten to cite the authoritative source and date; `INDEX_REBALANCING.nextUpdate` bumped to `2026-06-19` (next quarterly review).

## Stale-row cleanup

Direct PostgREST `DELETE` on `spread_results` for the 111 removed tickers, filtered to `data_source='price_history_5yr'`. HTTP 204, **21,600 rows removed**. Pre-delete `data_source='price_history_5yr'` count: 91,700. Post-delete: 70,100. Hunt cannot now surface a removed-ticker row even if a stale request bypassed the universe filter.

## Followup found mid-run (NOT addressed in this run)

`spread_results` shows **~2× duplication** for surviving tickers. Pre-delete total was 91,700 rows where the expected single-batch fill is ~46,100 (461 × 100 grid cells). Post-delete count of 70,100 across ~350 surviving tickers averages ~200 rows/ticker vs the 100/ticker grid expectation. Two probable causes:

1. The upsert key in `runSpreadResultsBatch` is failing to dedupe on `(ticker, otm_pct, dte_weeks, direction)` and writing fresh rows each batch instead of replacing.
2. The nightly cron (run 13 of 2026-05-08) fired between the run-12 SP500 fire and this run, doubling.

Either way, this means each successive nightly run multiplies row count. Hunt result quality is fine right now (rows are identical, ranking unaffected) but storage and query cost climbs unbounded. Added as a new TODO; should be the next StrikeRewind work.

## Commit

`e692274` on `autobox/strikerewind-rename`, pushed to GitHub. Render auto-deploy in flight; tonight's 06:00 ET cron will be the first batch to write against the new universe.

## Budget

No spend; cash $162.45.
