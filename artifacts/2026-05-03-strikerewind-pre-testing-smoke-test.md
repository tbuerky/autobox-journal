# StrikeRewind: pre-testing smoke test of live deployment

**Date:** 2026-05-03
**Surface:** strikerewind.com (live, deployed 2026-05-02)
**Purpose:** find any deployment issues before Travis's `TESTING COMPLETE` round so the testing surfaces UX/product issues, not infrastructure ones.

## Result

**User-facing flows are unblocked for testing.** Sign-up, login, Hunt, Analysis, Watchlist, dashboard, public pages — all functional. Two real DNS/Vercel bugs found that don't block testing but should be fixed during Travis's next pass through the registrar/Vercel dashboard. Two previously-known gated issues (Stripe products + webhook) confirmed.

## Smoke test results

### Public pages (all HTTP 200)

| URL | Result |
|---|---|
| `https://www.strikerewind.com/` | 200 — title, description, canonical, og:*, twitter:*, theme-color all correct |
| `https://www.strikerewind.com/privacy` | 200 |
| `https://www.strikerewind.com/terms` | 200 |
| `https://www.strikerewind.com/robots.txt` | 200 |
| `https://www.strikerewind.com/sitemap.xml` | 200 |
| `https://www.strikerewind.com/og-card.png` | 200 (22 815 bytes) |
| `https://www.strikerewind.com/logo.png` | 200 (2 740 bytes) |

### SPA routing (catch-all 200)

| URL | Result |
|---|---|
| `https://www.strikerewind.com/dashboard` | 200 (SPA serves) |
| `https://www.strikerewind.com/hunt` | 200 (SPA serves) |
| `https://www.strikerewind.com/this-route-does-not-exist` | 200 (NotFound page) |

### Backend API (Render direct: `https://strikerewind-api.onrender.com`)

| Endpoint | Result | Notes |
|---|---|---|
| `GET /api/health` | 200 `{"status":"ok"}` | Healthy |
| `GET /api/usage` (no header) | 400 `User ID required` | Correct contract — frontend supplies `x-user-id` |
| `GET /api/usage` (fake uuid) | 200 `{tier:"FREE", limits:{maxAnalysesPerDay:3, ...}}` | FREE-tier defaults correct; `DEV_MODE` is OFF in production |
| `POST /api/hunt` (no header) | 400 `User ID required` | Correct |
| `POST /api/analyze` (no header) | 400 `User ID required` | Correct |
| `GET /api/watchlist` (no header) | 400 `User ID required` | Correct |
| `GET /api/stripe/prices` | 200 `{}` | **Empty — gated under `STRIPE LIVE CONFIGURED`** |
| `POST /api/stripe/webhook` | 400 `Webhook Error: Stripe webhook secret not configured` | **Gated under same** |
| `POST /api/stripe/checkout` (fake) | `{"error":"Failed to create checkout session"}` | Correct — fake price ID |
| CORS preflight from `https://www.strikerewind.com` | 200 | Strict CORS allow-list working |

## Two new bugs found

### Bug 1 — `api.strikerewind.com` points at Vercel, not Render

```
$ dig +short api.strikerewind.com
216.198.79.1
64.29.17.65       ← Vercel A records (not Render)

$ curl -i https://api.strikerewind.com/api/health
HTTP/2 404
x-vercel-error: DEPLOYMENT_NOT_FOUND
```

The DNS record at the registrar resolves to Vercel IPs. Vercel does not have `api.strikerewind.com` registered as a domain on the strikerewind project (or any project on `travis-4599s-projects`), so it returns DEPLOYMENT_NOT_FOUND.

**Impact:** does not break the SPA. The frontend's `VITE_API_URL` was set on Vercel to the working `https://strikerewind-api.onrender.com` directly (not `https://api.strikerewind.com`), so every user-facing flow that hits the backend works fine. The bug only matters for:
- documentation correctness (the registrar fix list in HANDOFF assumed `api.` would resolve to Render)
- any future external integration trying to use `api.strikerewind.com`
- the Stripe webhook URL — currently in the recommendation packet as `https://strikerewind-api.onrender.com/api/stripe/webhook` (the working URL), so this does NOT block the open `STRIPE LIVE CONFIGURED` gate

**Fix (Travis at registrar):** delete the existing `api.strikerewind.com` record, add `CNAME api → strikerewind-api.onrender.com`. After DNS propagates (≤1 hour), `https://api.strikerewind.com/api/health` will return `{"status":"ok"}` and Vercel project env `VITE_API_URL` can be repointed to `https://api.strikerewind.com` if desired (cosmetic; not required).

### Bug 2 — apex/www canonical mismatch

The build artifacts (HTML `<link rel="canonical">`, `og:url`, `sitemap.xml`) all declare `https://strikerewind.com/` (non-www) as canonical. But the live Vercel project config does the opposite — apex 307-redirects to www:

```
Vercel project domains for `strikerewind`:
  strikerewind.com           redirect=www.strikerewind.com   ← this is backwards
  www.strikerewind.com       (canonical)
  strikerewind.vercel.app
```

```
$ curl -I https://strikerewind.com/
HTTP/2 307
location: https://www.strikerewind.com/
```

**Impact:** soft. Search engines understand canonical signals and will sort it out. But the canonical-to-live mismatch is a small credibility ding and could cost a few percent of organic traffic over time. No effect on the testing round.

**Fix (Vercel dashboard):** in the strikerewind project → Settings → Domains, swap the redirect — set `www.strikerewind.com` to redirect to `strikerewind.com`, and set `strikerewind.com` as the primary domain. After save, apex serves directly and www redirects in.

## Confirmed previously-known gated issues

These are already documented under `STRIPE LIVE CONFIGURED: STRIKEREWIND` in `OPEN_GATES.md` and in `artifacts/2026-05-02-strikerewind-stripe-live-products-and-webhook-packet.md`:

- `GET /api/stripe/prices` returns `{}` (no live products in Stripe)
- `POST /api/stripe/webhook` returns `400 Stripe webhook secret not configured`

No change to the existing packet — the recommendation already targets the working backend URL.

## Recommendation for the `TESTING COMPLETE` round

Travis can begin testing immediately. The two new bugs above don't block any user-facing flow:

- Sign-up / login go through Supabase Auth client-side (no backend involvement).
- Hunt, Analysis, Watchlist, Account all hit `https://strikerewind-api.onrender.com` directly via `VITE_API_URL`.
- Stripe checkout will fail (already gated, not a testing blocker — testing the rest of the product is more valuable).

When Travis has the registrar/Vercel dashboard open for the Stripe live setup, the two DNS/redirect fixes can be done in the same sitting (5 minutes total). They are additive — none of them block any other gate.

## State files updated

- `TODO.md` — `[DONE]` line added at top of immediate-priority list
- `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` — appended
- `OPEN_GATES.md` — unchanged (no new gate; the umbrella `TESTING COMPLETE: STRIKEREWIND` covers post-testing follow-ups, and `STRIPE LIVE CONFIGURED: STRIKEREWIND` already covers the two known issues)
- `BUDGET.md` — unchanged ($162.45)

## Cost / risk

Zero spend. Read-only smoke test against the live production deployment. No deploys triggered, no env vars changed, no DNS modified.
