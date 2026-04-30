# StrikeRewind — `spread_results` warehouse migration packet

**Date:** 2026-04-30
**Branch:** `autobox/strikerewind-rename`
**File:** `backend/supabase-migration-spread-results.sql` (new, 100 lines)
**Owner action:** apply via Supabase Dashboard → SQL Editor on project `hjfsapwessfvdcfytpuk`. Idempotent — safe to re-run.

## Why this exists

The 2026-04-28 product definition session locked the data architecture as: nightly batch job pre-computes all credit spread results across the S&P 500 → stores in a Supabase results warehouse → user queries are instant DB lookups instead of on-demand math. Different historical windows (1yr / 2yr / 3yr / 5yr) are filters on the same pre-computed dataset.

The initial 6-table schema Travis applied via dashboard is the user-state schema (users, usage_tracking, watchlists, analysis_cache, hunt_cache, subscription_events). It does not include the warehouse table. Repeated handoffs have flagged the `spread_results` migration as still-needed-from-Travis but the actual SQL has not been written until now.

Without this table the current code path for Hunt / Ticker Analysis is "compute on-demand → write to a 15-min/30-min TTL cache." That works for a small dev S&P scan with fixtures, but it does not scale to the full 500-ticker × 8-DTE × 12-OTM × 4-history-window grid the product is sold on, and it forecloses the watchlist daily-digest and weekly curated-report features Pro/Ultra promise.

## What the migration adds

Two tables and one helper function. All are server-written only — RLS enabled with no policies, so anon/authenticated have no access; backend uses the service role key.

### `spread_results`
One row per (ticker, spread_type, otm_pct bucket, dte_weeks bucket, analysis_years window, as_of_date). The unique constraint enforces upsert-on-conflict so the nightly job can re-run safely.

Columns:
- **Position** — `ticker`, `spread_type` (`PUT` | `CALL`), `otm_percentage` (negative = ITM), `timeframe_weeks` (DTE bucket), `analysis_years` (`1` | `2` | `3` | `5`)
- **Performance** — `win_rate`, `ev_percent`, `premium`, `total_trades`
- **Snapshot context** — `current_price`, `iv_rank` (denormalized so the matrix render does not need a second query)
- **Provenance** — `as_of_date`, `computed_at`, `data_source` (`polygon` | `yfinance` | `fixture`)

Three indexes covering the three primary access patterns:
- Hunt: `(as_of_date DESC, analysis_years, spread_type, ev_percent DESC)` — top-N by EV for a spread type and history window on the latest day
- Ticker matrix: `(ticker, as_of_date DESC, analysis_years)` — full grid for one ticker
- Watchlist top-signal: `(ticker, as_of_date DESC, ev_percent DESC)` — best signal per ticker across a list

### `batch_runs`
Nightly job status + diagnostics. One row per run; tracks `started_at`, `completed_at`, `status`, `tickers_total`, `tickers_processed`, `rows_written`, `error_message`, `metadata`. Lets the operator see at a glance whether last night's run completed, which ticker failed if it failed mid-run, and how long it took.

### `prune_spread_results(retention_days)`
Drops rows where `as_of_date < CURRENT_DATE - retention_days`. Default 30 days. The nightly job calls this after a successful write to keep the table from growing unboundedly. Sizing math: 500 tickers × 2 types × ~12 OTM buckets × ~8 DTE buckets × 4 history windows ≈ 380 K rows per snapshot; at ~250 bytes per row that is ~95 MB per day, ~2.8 GB at 30 days — comfortably within Supabase Pro Compute. Free-tier 500 MB ceiling fits ~5 days, which is why the retention window is configurable.

## Apply instructions for Travis

1. Open Supabase Dashboard → project `hjfsapwessfvdcfytpuk` → SQL Editor → New query.
2. Paste the contents of `backend/supabase-migration-spread-results.sql` (or the SQL block at the bottom of this artifact).
3. Run.
4. Reply with `MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE`.

Verification query (run in the same editor after apply):

```sql
SELECT table_name FROM information_schema.tables
WHERE table_schema = 'public' AND table_name IN ('spread_results', 'batch_runs');
-- expect 2 rows.

SELECT indexname FROM pg_indexes
WHERE schemaname = 'public' AND tablename = 'spread_results';
-- expect spread_results_hunt_idx, spread_results_ticker_idx, spread_results_watchlist_idx (+ the implicit unique-constraint index).
```

## What unblocks after apply

Three downstream autonomous-runnable steps that have been blocked on this table existing:

1. **`spreadResultsService.ts`** — write/read shim around the table. Same shape as `watchlistServiceDB.ts` etc. Methods: `upsertResults(rows)`, `getHuntResults(spreadType, years, limit)`, `getTickerMatrix(ticker, years)`, `getTopSignalForTickers(tickers, years)`. Adds `getFromStorage`/`setInStorage`-style symmetry with the existing `SupabaseDatabaseService` shape.
2. **Nightly batch wiring** (`schedulerService.ts`) — node-cron job that runs the existing `analysisEngine.analyzeStock` over the S&P 500 list, writes one snapshot per run to `spread_results`, calls `prune_spread_results(30)`, logs to `batch_runs`. Already gated on Polygon approval (`APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO`) — the wiring is independent of the data source, so the same code path serves Polygon in prod and the existing yfinance/fixtures path in dev.
3. **Watchlist top-signal-per-ticker render** — `Watchlist.tsx` currently shows `{ticker, addedAt}`. With this table populated, a single `getTopSignalForTickers(watchlistTickers, 1)` query yields the daily-digest payload Pro/Ultra promise.

None of those three are part of this packet — they are the next-three autonomous runs that become available once the table exists.

## What this does NOT do

- Does not subscribe to Polygon. Data source remains yfinance + fixtures until `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` lands.
- Does not change Hunt / Ticker Analysis read paths. Existing `analysis_cache` and `hunt_cache` tables continue to serve ad-hoc requests until the services are repointed.
- Does not run a backfill. First populated row arrives the first time the nightly batch job runs after Polygon goes live (or against fixtures on a manual trigger, for testing).

## Public-copy hygiene

Not applicable — this is internal database schema, no public surface affected.

## Suggested post copy

```
MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE
```

(Reply with this line after pasting the SQL into Supabase Dashboard and running it; AutoBox will pick it up on the next autonomous run and queue the service shim + nightly batch wiring.)

## SQL (for direct paste)

```sql
-- StrikeRewind — spread_results warehouse migration
-- Apply via Supabase Dashboard → SQL Editor on project hjfsapwessfvdcfytpuk
-- Idempotent: safe to re-run.

CREATE TABLE IF NOT EXISTS spread_results (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  ticker TEXT NOT NULL,
  spread_type TEXT NOT NULL CHECK (spread_type IN ('PUT', 'CALL')),
  otm_percentage NUMERIC(6, 2) NOT NULL,
  timeframe_weeks INTEGER NOT NULL,
  analysis_years INTEGER NOT NULL CHECK (analysis_years IN (1, 2, 3, 5)),
  win_rate NUMERIC(5, 2) NOT NULL,
  ev_percent NUMERIC(8, 2) NOT NULL,
  premium NUMERIC(10, 4) NOT NULL,
  total_trades INTEGER NOT NULL,
  current_price NUMERIC(12, 2),
  iv_rank NUMERIC(5, 2),
  as_of_date DATE NOT NULL,
  computed_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  data_source TEXT NOT NULL DEFAULT 'polygon',
  UNIQUE (ticker, spread_type, otm_percentage, timeframe_weeks, analysis_years, as_of_date)
);

CREATE INDEX IF NOT EXISTS spread_results_hunt_idx
  ON spread_results (as_of_date DESC, analysis_years, spread_type, ev_percent DESC);
CREATE INDEX IF NOT EXISTS spread_results_ticker_idx
  ON spread_results (ticker, as_of_date DESC, analysis_years);
CREATE INDEX IF NOT EXISTS spread_results_watchlist_idx
  ON spread_results (ticker, as_of_date DESC, ev_percent DESC);

CREATE TABLE IF NOT EXISTS batch_runs (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  run_type TEXT NOT NULL,
  started_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  completed_at TIMESTAMPTZ,
  status TEXT NOT NULL DEFAULT 'running'
    CHECK (status IN ('running', 'succeeded', 'failed', 'partial')),
  tickers_total INTEGER,
  tickers_processed INTEGER,
  rows_written INTEGER,
  error_message TEXT,
  metadata JSONB
);

CREATE INDEX IF NOT EXISTS batch_runs_recency_idx
  ON batch_runs (run_type, started_at DESC);

ALTER TABLE spread_results ENABLE ROW LEVEL SECURITY;
ALTER TABLE batch_runs ENABLE ROW LEVEL SECURITY;

CREATE OR REPLACE FUNCTION prune_spread_results(retention_days INTEGER DEFAULT 30)
RETURNS INTEGER AS $$
DECLARE
  deleted_count INTEGER;
BEGIN
  DELETE FROM spread_results
  WHERE as_of_date < (CURRENT_DATE - (retention_days || ' days')::INTERVAL);
  GET DIAGNOSTICS deleted_count = ROW_COUNT;
  RETURN deleted_count;
END;
$$ LANGUAGE plpgsql;
```
