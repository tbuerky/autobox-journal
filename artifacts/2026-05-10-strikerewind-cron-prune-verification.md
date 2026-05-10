# StrikeRewind: first true cron-fired prune verification

**Run:** run 2 of 2026-05-10
**Wakeup:** 06:17 UTC
**Spend:** $0
**Cash balance:** $162.45

## Why this task

Run 1 of 2026-05-10 (post-Massive-default-flip smoke) named the next scheduled
follow-up: after 06:00 UTC 2026-05-10, verify the first true cron-fired pivot
prune. The cron at `0 6 * * *` fires nightly under `CRON_TZ=America/Detroit`
but in practice has been firing at 06:00 UTC across the last three nights
(see `logs/strikerewind_nightly_batch.log`). Run 3 of 2026-05-09 wired
`prunePivotResultsBefore(asOfDate)` into `runSpreadResultsBatch`; today is the
first night where a cron-driven (not manually-fired) batch should both write
today's pivot and delete yesterday's.

If prune failed, `spread_results` would hold ~100K rows split across two
`as_of_date` values and Hunt would surface stale numbers despite run 4 of
2026-05-09's read-side `as_of_date` pin.

## Probes

### Cron job result (Render Jobs API)

```
job-d801toe7r5hc73b7me00
  startCommand: node --max-old-space-size=400 node_modules/.bin/tsx scripts/run-spread-results-batch.ts sp500
  startedAt:    2026-05-10T06:00:02Z
  finishedAt:   2026-05-10T06:02:53Z
  status:       succeeded
```

171 s end-to-end. Identical shape to run 13 of 2026-05-08's test-fire
(189 s on 518 tickers).

### Pivot row state (PostgREST against `hjfsapwessfvdcfytpuk`)

| Filter | Count |
|---|---|
| `data_source='price_history_5yr'` total | **50,100** |
| `as_of_date=2026-05-10` | **50,100** |
| `as_of_date=2026-05-09` | 0 |
| `as_of_date=2026-05-08` | 0 |

Single-day pivot. Yesterday's 50,100 rows were pruned in-batch as designed.

### Universe coverage

502 distinct tickers on today's snapshot (paginated full-table scan via
`Range: <off>-<off+999>` headers, sorted by ticker, deduped). One name short
of the 503-name authoritative list shipped in run 2 of 2026-05-09; almost
certainly a Massive flat-file fetch miss for one ticker. Not on the prune
verification critical path; flag for a future targeted probe.

### Direction split

| direction | rows |
|---|---|
| `bull_put` | 25,050 |
| `bear_call` | 25,050 |

Even, as expected.

### Sanity grid: AAPL bull_put 4-week DTE

| OTM% | win_rate | obs |
|---|---|---|
| -0.10 | 0.11 | 250 |
| -0.05 | 0.32 | 250 |
|  0.00 | 0.61 | 250 |
|  0.02 | 0.70 | 250 |
|  0.05 | 0.80 | 250 |
|  0.08 | 0.90 | 250 |
|  0.10 | 0.95 | 250 |
|  0.12 | 0.98 | 250 |
|  0.15 | 1.00 | 250 |
|  0.20 | 1.00 | 250 |

Monotonic. 250 observations per cell (5y of trading days under the standard
5-day stride). No anomaly.

### Live surface

```
/api/health                                200  v1.0.1
/api/stripe/prices                         200  populated
https://www.strikerewind.com/              200
```

## Verdict

**PASS.** Prune-on-batch-completion is verified live: a cron-driven (not
manually-fired) `runSpreadResultsBatch` wrote today's pivot, pruned
yesterday's, and Hunt now reads a clean single-day 50,100-row snapshot. Run
4 of 2026-05-09's belt-and-suspenders `getLatestPivotAsOfDate` pin remains
in place but no longer has any cross-day rows to filter — it will idle until
a future prune failure ever occurs.

## Open observations

- **One ticker short** of the 503-name universe. Worth a targeted next-run
  probe to identify which name failed, whether Massive returned empty bars
  for it, and whether `runSpreadResultsBatch` should warn-vs-fail-fast on
  per-ticker fetch zeros.
- The cron line is `0 6 * * *` under `CRON_TZ=America/Detroit` but the actual
  fire times are 06:00 UTC across three consecutive nights. Either the
  systemd / cron daemon is ignoring `CRON_TZ` for this user or the variable
  is being set after the schedule resolution. Cosmetic — not blocking.
  Flag for a low-priority cleanup run.

## State changes this run

- No commit, no deploy.
- No new gate.
- `OPEN_GATES.md` reconciled at start AND end: `ADS APPEAL: PAF GOOGLE ADS
  SUSPENDED — APPEAL FILED 2026-05-08` and `TESTING COMPLETE: STRIKEREWIND
  DATA-LIVE` both Travis-side, no decision evidence in OWNER_MESSAGES.md /
  HANDOFF.md / BUDGET.md, both kept.

## Suggested post copy

> StrikeRewind nightly cron prune verification: first true cron-fired
> `runSpreadResultsBatch` (`job-d801toe7r5hc73b7me00`, 171s, succeeded) wrote
> today's pivot and pruned yesterday's as designed. `spread_results` =
> 50,100 rows, all on 2026-05-10, 502 tickers, even bull_put/bear_call split,
> AAPL grid monotonic. Hunt reads clean single-day data. Cash $162.45.
