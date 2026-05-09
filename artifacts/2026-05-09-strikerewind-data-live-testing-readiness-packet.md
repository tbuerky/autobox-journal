# StrikeRewind data-live testing readiness packet

**Date**: 2026-05-09 16:20 UTC (run 5 of 2026-05-09)
**Owner action**: Travis to run a fresh testing pass on `https://www.strikerewind.com`. Reply on Discord with `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` to lift the 2026-05-02 marketing freeze, or with specific bugs to fix.

## Why this packet now

Travis's 2026-05-02 directive: *"block any public-facing moves toward traffic/marketing of StrikeRewind until I can do a full round of testing. Also, we have not turned on real data yet."*

Both halves of that directive have moved since:

- **Real data is on.** Massive (rebranded Polygon) S3 flat-files wired 2026-05-08; first live S&P 500 win-rate batch landed 51,020 rows that day; nightly cron at 06:00 ET has fired cleanly twice; latest pivot snapshot holds 35,000 rows for `as_of_date = 2026-05-09`. Fixture mode for the AAPL/MSFT/UNH demo path is preserved and untouched.
- **Hunt now reads real win rates.** `/api/hunt` was repointed at the pivot warehouse on 2026-05-08 (commit `f1aa576`), with read-side belt-and-suspenders pinning to the latest `as_of_date` added today (commit `2b38dff`). Cross-day duplicates cannot leak even if a future prune fails.
- **Watchlist regression class fixed** 2026-05-07.
- **Subscription path defended** 2026-05-07: live Stripe webhook signature verification holds; trial-period bug removed; `trialing` status treated as entitled.

The product Travis would test today is materially different from the product he last touched on 2026-05-02. A fresh testing pass is the bottleneck on lifting the marketing freeze.

## Current live state

| Surface | Status |
|---|---|
| `https://www.strikerewind.com` | HTTP 200 |
| `https://strikerewind-api.onrender.com/api/health` | HTTP 200, v1.0.1 |
| Pivot rows in `spread_results` (`price_history_5yr`) | 35,000 rows / latest `as_of_date = 2026-05-09` (per run 4 today) |
| Nightly batch | Render cron `0 6 * * *` America/Detroit, last success today |
| Free-tier Hunt limit | 1 scan/day, gated server-side |
| Stripe live keys | Configured; webhook verified; price IDs populated |

## Suggested 30-minute testing checklist

The full playbook is at `artifacts/2026-05-03-strikerewind-testing-playbook.md`. The bounded version focused on what changed since 2026-05-02:

1. **Sign in, run one Hunt** with default Free-tier criteria. Confirm results table populates with real tickers + win-rate column + OTM%/DTE/direction. Sort each column. Confirm row click navigates to `/analysis/:ticker`.
2. **Open Watchlist.** Confirm rows render values, no "Data refreshing" placeholder anywhere.
3. **Run a second Hunt as Free.** Confirm the daily limit gate fires and the upgrade prompt is honest, not aggressive.
4. **Hit `/account`.** Confirm tier badge + plan cards render. Do NOT click Upgrade unless you want to actually transact (live Stripe).
5. **Phone test on `https://www.strikerewind.com`.** Confirm no horizontal scroll, no broken cards, copy reads cleanly.
6. **Try a nonsense ticker (`ZZZZZ`)** in Analyze. Confirm the error state renders with a recovery path, not a blank page.

The Playwright suite covers (1)–(6) automatically and is green at 35/35 against production as of run 4 today, but Travis-as-human eyes is the decision-maker.

## What lifts the freeze

A Discord reply of `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` lifts the marketing freeze and unlocks:

- Founder-voice X launch post (pre-written, Luke-polished, sitting in `artifacts/2026-04-30-strikerewind-x-launch-post.md` — paste-ready under `Suggested post copy:`)
- Resumed work on the `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` decision (Option A/B/C from the 2026-05-04 packet)
- Outbound distribution experiments (small, bounded, separately-approved)

A reply with specific bugs converts directly into the next run's task list.

## What does NOT need approval

- Continued backend hygiene (legacy IV / `analysisEngine` deletion slice surfaced in run 6 of 2026-05-08 audit)
- PAF cadence smokes
- Anything internal-facing

## Cash

$162.45. Recurring spend: Render starter $7/mo + Massive Stocks Starter $29/mo = $36/mo. Google Ads suspended pending appeal — out of scope per 2026-05-08 owner directive.

## Suggested post copy

> StrikeRewind has changed materially since you set the marketing freeze on May 2. Real S&P 500 win-rate data now flows nightly via Massive — Hunt returns 35,000 real rows from yesterday's snapshot, no synthetic IV anywhere. Watchlist regression is gone. Subscription path is hardened. When you can grab 30 minutes for a fresh testing pass on `https://www.strikerewind.com`, reply `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` to lift the freeze and unlock the launch-post path. Bounded checklist in `artifacts/2026-05-09-strikerewind-data-live-testing-readiness-packet.md`. Cash $162.45.
