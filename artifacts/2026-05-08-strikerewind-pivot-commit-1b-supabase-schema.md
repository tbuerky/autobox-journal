# StrikeRewind pivot — Commit 1b: Supabase schema migration

**Date:** 2026-05-08 (run 4)
**Branch:** `autobox/strikerewind-rename`
**Commit:** `117e41e`
**Supabase project:** `hjfsapwessfvdcfytpuk`
**Spec:** `artifacts/2026-05-08-strikerewind-price-history-pivot-spec.md` §4

## What landed

Migration file: `backend/supabase-migration-pivot-1b-spread-results-pivot-columns.sql`

Applied live via Supabase Management API
(`POST /v1/projects/hjfsapwessfvdcfytpuk/database/query`, HTTP 201).

### Columns added to `spread_results`

| Column | Type | Notes |
|---|---|---|
| `otm_pct` | NUMERIC(8,4) | strike distance, positive=OTM, negative=ITM |
| `dte_weeks` | INTEGER | DTE bucket in weeks |
| `direction` | TEXT | CHECK ∈ {`bull_put`, `bear_call`, NULL} |
| `observation_count` | INTEGER | sample size |
| `min_premium_pct` | NUMERIC(8,4) | premium floor as fraction of width |
| `min_premium_100` | NUMERIC(10,4) | $/contract on $100-wide |
| `min_premium_500` | NUMERIC(10,4) | $/contract on $500-wide |
| `low_confidence` | BOOLEAN | true when 20 ≤ obs < 40 |

### Default change

`data_source` default flipped from `'polygon'` → `'price_history_5yr'`.
Spec called the prior default "the lying default" — no Polygon data ever
flowed into this table. Existing rows keep whatever value they were
written with; only new inserts pick up the new default.

### Index added

`spread_results_pivot_hunt_idx` on
`(data_source, win_rate DESC, dte_weeks, otm_pct)` — supports the Hunt
query in spec §5.

## What was deliberately NOT done

- **Did not drop or rename existing columns.** `otm_percentage`,
  `timeframe_weeks`, `spread_type`, `total_trades`, `ev_percent`,
  `premium`, `current_price`, `iv_rank`, `analysis_years` are all left
  intact. Removing them is a later commit once consumer services are
  repointed to the new columns. Additive only.
- **Did not write any rows** to the new columns. Commit 2 (overnight
  scheduler) populates them.
- **Did not repoint Hunt or Ticker Analysis read paths** to the new
  columns. Commits 3+ handle that.
- **Did not route through Cove / Luke** — backend schema only, no
  customer-visible surface.
- **Did not raise a new gate** — autonomous and bounded.

## Verification

`information_schema.columns` query against the live DB returned all 8
new columns nullable + the new `data_source` default
`'price_history_5yr'::text`. Index `spread_results_pivot_hunt_idx`
present in `pg_indexes`. 26/26 backend tests still pass via
`npx tsx --test src/services/*.test.ts` (no test code changes — schema
delta is invisible to existing services).

## Idempotency

Migration uses `ADD COLUMN IF NOT EXISTS` and `CREATE INDEX IF NOT
EXISTS`. Re-running is a no-op. Safe to bundle into a future
DEPLOYMENT.md migration list.

## Cash impact

None. No spend.

## Next step in the pivot sequence

Commit 2 — overnight scheduler that calls `calculateGrid` (shipped in
Commit 1) for every S&P 500 ticker against 5yr yfinance history and
writes one row per (ticker, otm_pct, dte_weeks, direction) into
`spread_results` with `data_source = 'price_history_5yr'`. Spec §3.
