# StrikeRewind backend trust-proxy fix

**Run:** 5 of 2026-05-07 (fired ~14:17 UTC)
**Branch:** `autobox/strikerewind-rename`
**Commit:** `533b875` — "Trust Render's proxy so rate-limiting uses the real client IP"
**Deploy:** `dep-d7ua16p9rddc73cut470` — created 14:24:28 UTC, live at 14:27:31 UTC (~3 min)

## What was wrong

`backend/src/index.ts` never called `app.set('trust proxy', ...)`. With the
Express default of `false`, `req.ip` resolves to the immediate proxy address
(Render's load balancer) for every request, not the real client. Two
consequences:

1. `express-rate-limit` logged a `ValidationError` on every cold-start probe
   when it noticed the `X-Forwarded-For` header without a corresponding
   trust setting. Sample line from this morning's deploy
   (`2026-05-07T08:22:34.175Z`):
   > `ValidationError: The 'X-Forwarded-For' header is set but the Express
   > 'trust proxy' setting is false (default). This could indicate a
   > misconfiguration which would prevent express-rate-limit from
   > accurately identifying users.`
2. With every request appearing to come from the same proxy IP, the rate
   limiters in `backend/src/middleware/validation.ts` (general 100/15min,
   analysis 10/min, hunt 10/min, auth 5/15min) collapse to global counters,
   which means a single noisy client could lock everyone else out.

The bug was found by pulling `~6 hours` of Render app-logs against
`srv-d7r408favr4c73fb3670` to verify the post-watchlist-fix deploy was
clean. The morning fix worked (zero traffic-class errors after 08:27),
but the trust-proxy ValidationError surfaced as a recurring cold-start
log noise that would have masked future real errors and was actively
breaking rate-limiting correctness.

## Fix

Single-block edit in `backend/src/index.ts`, immediately after `const app
= express()`:

```ts
// Trust the first proxy hop (Render's load balancer) so req.ip resolves to the
// real client IP. Without this, express-rate-limit treats every request as
// coming from the proxy and rejects the X-Forwarded-For header.
app.set('trust proxy', 1);
```

`1` is the minimum hop count that lets `req.ip` walk one entry back in
`X-Forwarded-For` while not blindly trusting the entire chain. Render
terminates TLS at its own load balancer and rewrites the header, so one
hop is the right number.

## Verification

Live verification against `https://strikerewind-api.onrender.com`:

| Probe | Result |
|---|---|
| `GET /api/health` | HTTP 200, 336ms |
| `POST /api/analyze {ticker:AAPL}` | HTTP 200, returned fixture price `$189.42` |
| `GET /api/watchlist` | HTTP 200, list shape preserved |

Render app-log scan against `srv-d7r408favr4c73fb3670`, window
`2026-05-07T14:27:30Z → 14:28:31Z` (post-deploy):

- 25 log entries.
- **0** `X-Forwarded-For` / `ValidationError` occurrences.
- **0** real errors (the only `error`-level entry is the long-standing
  "Sentry DSN not found, error tracking disabled" config notice; Sentry
  was never wired up, intentional).

The previous deploy (`dep-d7u4n1e8bjmc73bj5tjg`, 08:22:27 UTC) emitted
the ValidationError within 7 seconds of going live. This deploy
(`dep-d7ua16p9rddc73cut470`, 14:27:31 UTC) has 60+ seconds of clean
post-live logs.

## Risk note

`app.set('trust proxy', 1)` is the standard recommended setting for apps
behind a single managed proxy (Render, Heroku, Fly). It is strictly
safer than the previous default (`false`) because the previous default
made rate-limiting a global counter; a malicious actor could not spoof
their way past per-IP limits because there were no per-IP limits to
spoof. The fix moves the system to actual per-client rate limiting,
which is the security posture the limiters were configured for.

## State changes

- Repo `tbuerky/StrikeSight` branch `autobox/strikerewind-rename`: pushed
  `533b875` on top of `b032b48`.
- Render service `srv-d7r408favr4c73fb3670` redeployed; service is live.
- No env vars touched.
- No customer-facing copy or layout changed.
- No new gate raised — autonomous and complete.

## Spend

$0. Cash balance unchanged at $162.45. Render starter accruing
~$0.23/day toward end-of-cycle invoice.
