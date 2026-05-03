# StrikeRewind — Render service audit (post-deploy day +1)

**Date**: 2026-05-03 06:21 UTC
**Service**: `srv-d7r408favr4c73fb3670` (`strikerewind-api`), Starter plan, oregon
**Goal**: Surface first-24h infrastructure issues (cold-start latency, restart loops, build warnings, auto-deploy gaps) before Travis's `TESTING COMPLETE` round so testing time goes to UX/product, not setup.
**Mode**: Read-only Render API + 5x `/api/health` probes spaced ~25s apart.

## TL;DR
**Service is healthy.** No remediation required.
- Service status: `live`, `not_suspended`.
- 2 of 2 deploys completed `live` (one `deactivated` because superseded; not a failure).
- 5 of 5 health probes return HTTP 200 in 109-254ms.
- 0 restart events, 0 build failures, 0 deploy errors in event log.

## Service config (verified vs. creation packet)
| Field | Live value | Expected |
|---|---|---|
| name | `strikerewind-api` | match |
| plan | `starter` | match (pre-approved $7/mo) |
| region | `oregon` | match |
| branch | `autobox/strikerewind-rename` | match |
| rootDir | `backend` | match |
| autoDeploy | `yes` | match |
| healthCheckPath | `/api/health` | match |
| numInstances | `1` | match |
| env | `node` | match |
| URL | `https://strikerewind-api.onrender.com` | match |

## Deploy history (latest 10; only 2 exist)
| ID | Status | Trigger | Commit | Build dur. | Notes |
|---|---|---|---|---|---|
| `dep-d7r62qugvqtc73baesr0` | **live** | api (autodeploy) | `5d27cfc` "vercel.json: strip serverless backend..." | ~37s build, ~24s deploy phase | Current. Auto-fired when frontend `5d27cfc` was pushed to the watched branch — backend rebuilt cleanly even though the commit only touched root `vercel.json`. |
| `dep-d7r408navr4c73fb3790` | deactivated | manual (initial create) | `aa7b3d9` "logo: route fills through CSS variables..." | ~35s build, ~24s deploy phase | First deploy. Superseded 2h22m later by the next push. |

**Observation**: yesterday's smoke test (`2026-05-03-strikerewind-pre-testing-smoke-test.md`) reported the live deploy as `dep-d7r408...` because that was current at 18:20 UTC. By 20:42 UTC, `dep-d7r62...` (commit `5d27cfc`) had taken over. Endpoint contract unchanged — `strikerewind-api.onrender.com` always points at the latest live deploy. Yesterday's smoke-test assertions remain valid.

## Event log (latest 30; 8 exist)
4 events per deploy: `build_started` → `build_ended` → `deploy_started` → `deploy_ended`. **Nothing else.** No `instance_restarted`, no `cron_triggered`, no `service_resumed`, no error events. The first 12 hours of production were genuinely uneventful.

## Health probe (5x over ~100s)
| # | HTTP | Elapsed | Body |
|---|---|---|---|
| 1 | 200 | 0.120s | `{"status":"ok","timestamp":"2026-05-03T06:19:06.446Z","version":"1.0.0"}` |
| 2 | 200 | 0.128s | `{"status":"ok","timestamp":"2026-05-03T06:19:31.572Z","version":"1.0.0"}` |
| 3 | 200 | 0.254s | `{"status":"ok","timestamp":"2026-05-03T06:19:56.828Z","version":"1.0.0"}` |
| 4 | 200 | 0.109s | `{"status":"ok","timestamp":"2026-05-03T06:20:21.938Z","version":"1.0.0"}` |
| 5 | 200 | 0.128s | `{"status":"ok","timestamp":"2026-05-03T06:20:47.067Z","version":"1.0.0"}` |

**Mean 0.148s, median 0.128s, max 0.254s** — all well under any cold-start envelope. **No spin-down behavior** (correct: Render Starter does NOT spin down; only Free tier does). Probe 3's 254ms is normal client-side variance, not service drift.

## What this confirms for `TESTING COMPLETE`
1. **Backend stays warm** during Travis's testing window — Starter plan keeps the instance hot, sub-300ms median latency.
2. **Auto-deploy is wired and verified** — pushing `5d27cfc` to the branch triggered a clean rebuild within seconds, completed in <90s end-to-end. Future fixes during testing land deterministically.
3. **No latent infrastructure issues** from the first ~12h of production. Travis can focus testing on UX/product.
4. **Deploy rollback path exists** — Render keeps deactivated deploys available; `dep-d7r408...` can be re-promoted via API if `5d27cfc`-and-later introduce a regression. Documented for completeness; not needed today.

## What was deliberately NOT done
- **Build/runtime log scrape via `/v1/logs`** — the deploys all completed `live` with no error events, so log-level audit would be diminishing returns. Available on request.
- **Stress / load probe of `/api/hunt` or `/api/analyze`** — would require authenticated requests (Supabase user + valid `x-user-id` header), and creating a real test account would pollute production auth (same reason yesterday's smoke test stopped at the unauthenticated contract).
- **Vercel deploy log audit** — separate property, separate service. Vercel deploy `dpl_2ep9LU5FSy1fA76TbMMUf5Tav4vR` was already verified `READY` 2026-05-02 with successful smoke 2026-05-03; no signal in re-checking.
- **Fix for the api.strikerewind.com DNS bug or the apex/www canonical mismatch** — both were surfaced in yesterday's smoke test, both are documented as Travis-side fixes that fold into the `TESTING COMPLETE` round; autonomous fix would touch the user-visible address bar (apex/www) or unbind a working configuration (api subdomain) for negligible gain.

## Reproducer
`workspace/render_audit_strikerewind.py` — single-shot Python, loads `RENDER_API_KEY` from `.env`, never echoes secrets. Re-run anytime to verify service health.

Output dump: `workspace/render_audit_strikerewind.json`.
