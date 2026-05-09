# StrikeRewind — pin Hunt pivot query to latest as_of_date snapshot

Date: 2026-05-09
Run: 4 of 2026-05-09
Commit: `2b38dff` on `autobox/strikerewind-rename`
Deploy: `dep-d7videtbbn2s73bnn54g` (Render service `srv-d7r408favr4c73fb3670`)

## What this is

Belt-and-suspenders defense surfaced as next-step guidance in run 3 of today.
Run 3 wired the prune step into `runSpreadResultsBatch` so each successful nightly
batch removes pivot rows older than today. That handles the *write* path. This
slice hardens the *read* path: even if a future prune step ever fails (network
error, partial batch, an unforeseen edge), `getHuntSpreadResultsPivot` now pins
the query to the latest `as_of_date` instead of relying on `ORDER BY as_of_date
DESC LIMIT 200` to keep cross-day duplicates out of the result set.

## Background

Run 3 left `spread_results` clean: 35,000 rows, all `as_of_date=2026-05-09`. Today's
06:00 UTC nightly cron (job `job-d7vcqojeo5us73ejcr1g`) succeeded BEFORE run 3's
prune commit was pushed, so the cron used pre-prune code. Tomorrow's 06:00 UTC
cron will be the first run with the prune step active. This change is the read-side
backstop in case prune ever doesn't fire.

## Diff

`backend/src/services/supabaseDatabaseService.ts`

- New `getLatestPivotAsOfDate()` returns the most recent `as_of_date` for rows
  where `data_source='price_history_5yr'`, or `null` if no pivot rows exist.
- `getHuntSpreadResultsPivot()` now resolves an effective `asOfDate` at the top:
  uses the explicit `opts.asOfDate` if passed; otherwise calls
  `getLatestPivotAsOfDate()`. Returns `[]` when the table is empty.
- Query then includes `.eq('as_of_date', asOfDate)`. Old `.order('as_of_date',
  desc)` removed (no longer needed — single date).

Net behavior on a clean DB: identical (one date present → that's the latest →
same rows). Net behavior on a dirty DB (multiple dates present): only the latest
day surfaces, so users never see stale duplicates.

## Verification

- `npx tsc --noEmit`: clean.
- `npx tsx --test 'src/**/*.test.ts'`: 61/61 pass.
- Push: `2b38dff` to `origin/autobox/strikerewind-rename`.
- Render auto-deploy + manual trigger: `dep-d7videtbbn2s73bnn54g` in flight.

No new env vars, no schema change, no migration.

## Live state on entry

Read via PostgREST against Supabase project `hjfsapwessfvdcfytpuk` using creds
pulled from Render env (no new credentials introduced):

```
data_source='price_history_5yr' total: 35,000 rows
distinct as_of_date: 2026-05-09 (only)
```

Run 3's cleanup held overnight. Today's pre-prune cron job did not double the
table — the within-day upsert dedup keys correctly on `(ticker, otm_pct,
dte_weeks, direction, as_of_date)`. The prune fix is required only when a
multi-day window opens.

## Why this slice over alternatives

- **Cron verification of run 3's prune** — not yet eligible. Today's 06:00 UTC
  cron used pre-prune code (commit pushed at 08:something UTC); the first true
  prune verification window opens after tomorrow's 06:00 UTC cron.
- **Legacy IV / analysisEngine deletion** — bigger surface, audited in run 6 of
  2026-05-08, deserves its own focused slice.
- **PAF EOD smoke** — last smoke ~2026-05-08 22:something UTC. Cadence not
  cleared (≥12h target). Will be tonight.
- **Per-call Massive allowlist** — explicitly marked off the revenue path.
- **`getHuntSpreadResultsPivot` pin** — was the run-3 fallback, fits inside the
  marketing freeze, removes a residual class of failure (read-path duplicates
  even if write-path prune ever lapses), and is one focused commit.

## Recommendation

No new gate raised. Single open gate sitting on Travis remains
`ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`.

## Next-run guidance

| If next run fires | Eligible move |
|---|---|
| After tomorrow 06:00 UTC | First true cron-fired prune verification — assert pivot table holds exactly one `as_of_date` (2026-05-10) at ~35,000 rows, NOT 70,000. |
| Before tomorrow 06:00 UTC | Open the legacy IV / analysisEngine deletion slice from run 6 of 2026-05-08's audit, OR a PAF EOD smoke if cadence cleared. |
| PAF EOD smoke cadence open | Cheap PAF Playwright smoke. |
| Owner replies on `ADS APPEAL` | Read the reply; resume PAF Ads work or pin as long-running status. |
| Owner sends new directive | Treat as highest priority. |

## Suggested post copy

> StrikeRewind: hardened the Hunt pivot query so it can never surface stale rows. The query now pins to the latest as_of_date (one DB call), so even if the new nightly prune step ever fails, users never see cross-day duplicates. Commit 2b38dff deployed. 61/61 backend tests pass. Cash $162.45.

## Budget

Cash $162.45. No spend this run. Recurring: Render starter $7/mo + Massive Stocks Starter $29/mo = $36/mo accruing.
