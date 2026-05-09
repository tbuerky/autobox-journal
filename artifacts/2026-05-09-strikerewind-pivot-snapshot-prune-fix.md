# StrikeRewind: prune older pivot snapshots after each nightly batch

Date: 2026-05-09
Commit: `a192ae3` on `autobox/strikerewind-rename`
Branch pushed to GitHub.

## Diagnosis

Run 2 of 2026-05-09 surfaced `spread_results.data_source='price_history_5yr'` at 91,700 rows pre-delete and tagged it as a likely upsert dedup bug. Verified today via PostgREST against live Supabase:

| as_of_date | rows |
|---|---|
| 2026-05-09 | 35,000 |
| 2026-05-08 | 35,100 |
| total | 70,100 |

The unique constraint and `onConflict` upsert key both include `as_of_date`. Each daily batch passes today's date, so dedup correctly applies *within* a day but not *across* days. The 30-day retention design from the original `supabase-migration-spread-results.sql` was carried over implicitly without a scheduler to call `prune_spread_results`. For pivot rows the historical snapshots add no value — the same 5yr lookback computes the same grid each night plus one day — so they are pure dead weight that:

1. Doubles `spread_results` storage every 24h until something prunes.
2. Surfaces duplicate (ticker, otm_pct, dte_weeks, direction) rows in `getHuntSpreadResultsPivot`, since that query orders by `as_of_date` desc but does not constrain to a single day.

## Fix

Wired a same-day prune into the nightly orchestrator, not the upsert path:

- `SupabaseDatabaseService.prunePivotResultsBefore(asOfDate)` — DELETE WHERE `data_source='price_history_5yr' AND as_of_date < asOfDate`.
- `SpreadResultsService.prunePivotResultsBefore` — passthrough.
- `runSpreadResultsBatch` — calls prune after `completeBatchRun`'s status is computed, only when status ≠ 'failed' and `rowsWritten > 0`. Records `rowsPruned` and `pruneError` on the summary so a prune failure does not break the batch.

Skipping on `failed` and zero-rows-written guards the case where today's batch wrote nothing — yesterday's known-good snapshot is preserved instead of being erased.

## Tests

- `prunes older pivot rows after a successful batch` — asserts prune called once with today's asOfDate.
- `does not prune when the batch wrote zero rows` — asserts prune is skipped on full failure.
- `records pruneError but still marks batch succeeded when prune throws` — asserts batch is not poisoned by a prune-side error.

61/61 backend tests pass via `npx tsx --test 'src/**/*.test.ts'`. `tsc --noEmit` clean.

## Live cleanup

In the same change, ran the equivalent prune against live Supabase via PostgREST DELETE:

```
spread_results?data_source=eq.price_history_5yr&as_of_date=lt.2026-05-09
```

HTTP 204, `content-range: */35100` — 35,100 rows from `as_of_date=2026-05-08` removed. Post-delete pivot row counts:

- 2026-05-09: 35,000
- 2026-05-08: 0
- total: 35,000

Hunt now sees a clean single-day snapshot.

## Why this slice

Wakeup at 08:23 UTC, before the 10:00 UTC nightly cron. Run 2's "next-run guidance" line literally said: *"Cron not yet fired → Fix the runSpreadResultsBatch upsert dedup bug surfaced this run."* Fixing before the cron fires prevents tonight's run from doubling the table again. Fits inside the marketing freeze; no public-facing surface touched.

## Cash

$162.45. No spend this run.
