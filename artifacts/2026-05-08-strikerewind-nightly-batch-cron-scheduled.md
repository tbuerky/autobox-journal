# StrikeRewind nightly SP500 win-rate batch — scheduled (run 13 of 2026-05-08)

## What I shipped

- New script `scripts/strikerewind_nightly_batch.sh` — POSTs to Render Jobs API
  (`POST /v1/services/srv-d7r408favr4c73fb3670/jobs`) with the `startCommand`
  `node --max-old-space-size=400 node_modules/.bin/tsx scripts/run-spread-results-batch.ts sp500`.
  Loads `RENDER_API_KEY` from `/home/autoproj/AutonomyProjectV2/.env`. Logs
  HTTP code + response body to `logs/strikerewind_nightly_batch.log`. Exit 0 on
  2xx, 1 on other status, 2 on missing key.
- New crontab entry under the existing `CRON_TZ=America/Detroit` block:
  `0 6 * * * /home/autoproj/AutonomyProjectV2/scripts/strikerewind_nightly_batch.sh`
  Fires daily at 06:00 ET — well after Massive's prior-day flat-file lands and
  before any STANDARD/PRO user is likely to query Hunt.

## Why this was the highest-leverage move

Run 12 fired the first live SP500 batch by hand from a one-off Render Job and
landed 46,520 distinct rows in `spread_results`. Without scheduling, those rows
go stale within one trading day and Hunt rows freeze at 2026-05-07. Travis
flagged this in TODO.md the same run: "schedule the SP500 win-rate batch as a
nightly Render Cron Job (or Render scheduled job) so `spread_results` stay
current. One-shot fire today is good for ~24h; freshness depends on
`as_of_date`."

The Jobs-API-from-VPS-cron path is strictly cheaper than a dedicated Render
Cron Job service: no new billable service, no extra approval gate, reuses
RENDER_API_KEY already on this box, and matches the exact mechanism we proved
out in run 12 (run-12 HANDOFF: "Render starter web services support one-off
Jobs via `POST /v1/services/{id}/jobs`. Job containers ship with full repo +
`node_modules`, so `node_modules/.bin/tsx scripts/foo.ts` runs directly").

## Live verification

- Test-fire from this VPS at 22:18:47 UTC: HTTP 201, `job-d7v62hv7f7vs73fejv7g`,
  status `pending`.
- Status re-check ~25s later: status `running`, `startedAt 2026-05-08T22:18:47Z`.
- Full-run evidence carried over from run 12 (same script, same start command,
  same service): 518/518 tickers, 51,020 rows, 189s, smoke 35/35.

## Deliberately NOT done

- Did not switch to a dedicated Render Cron Job service. The VPS-cron path is
  free, already-approved, and uses the exact same firing mechanism. If the VPS
  ever moves, the Render Cron Job service is a clean fallback that just needs
  `APPROVED: SUBSCRIBE RENDER CRON JOB, $X/MO`.
- Did not back-fill historical batches. The upsert dedup on `(ticker, otm_pct,
  dte_weeks, direction, as_of_date, data_source)` means daily fires are
  idempotent and the rolling 5y window self-extends.
- Did not raise a new gate. No owner action required.

## State changes

- `OPEN_GATES.md` — unchanged. Single Travis-side gate
  `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`.
- `BUDGET.md` — no spend; cash unchanged $162.45.
- `TODO.md` — close the "schedule the SP500 win-rate batch as a nightly Render
  Cron Job" entry; the Hunt data is now self-refreshing.

## Cash balance: $162.45
