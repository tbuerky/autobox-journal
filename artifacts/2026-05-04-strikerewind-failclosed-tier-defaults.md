# StrikeRewind: fail-closed tier defaults in UserContext

## What was wrong
`frontend/src/contexts/UserContext.tsx:45` initialized fresh-load state to:

```ts
tier: 'PRO' as const,
limits: { maxAnalysesPerDay: -1, maxScansPerDay: -1, hasIVData: true,
          historicalYears: 5, canSaveWatchlist: true }
```

Every fresh-localStorage page load briefly showed PRO branding (Hunt
unlocked, unlimited analyses, save-to-watchlist enabled) until the
`/api/usage` request returned and `setUserData(...)` overwrote those
defaults with the real tier. On API failure the user remained on PRO
defaults indefinitely.

Server enforces real tier on every protected endpoint, so this was
client-side UI only — but the flash was customer-visible on every cold
load and would surface during Travis's `TESTING COMPLETE` round on a
fresh browser.

## How the audit found it
Cross-referenced every frontend `/api/...` call against the routes
defined in `backend/src/index.ts`. All 14 frontend → backend routes
exist (the two added today closed the gap surfaced by the morning
Playwright run). The only mismatches:

- `/api/dev/reset-tier` and `/api/dev/user-data` — frontend exports them
  but production gates `handleResetTier` behind `import.meta.env.DEV`
  and never calls `getUserData`. Production-safe, dead in dist.

While reading `UserContext.tsx` for the cross-reference, the PRO
defaults stood out: every other state in the codebase fails closed.

## Fix shipped
Single-file commit `6ce5b06` — flip defaults to FREE-tier shape mirrored
from `backend/src/services/usageServiceDB.ts:22-31`:

```ts
tier: 'FREE' as 'FREE' | 'STANDARD' | 'PRO',
limits: { maxAnalysesPerDay: 3, maxScansPerDay: 1, hasIVData: false,
          historicalYears: 1, canSaveWatchlist: false }
```

Type widened from `'PRO' as const` to the full union so `setUserData`
keeps accepting any of the three tier values from the API.

## Verification
- `cd frontend && npm run build` — clean, 1921 modules, JS 356.04 kB,
  CSS 23.32 kB, no TS errors.
- Pushed to `autobox/strikerewind-rename`. Render auto-deploy fires for
  backend changes only — this is frontend-only, no Render redeploy.
- `vercel deploy --prod --yes --token "$VERCEL_TOKEN_TSS"` from
  `frontend/` — `dpl_EkHPY7Z9ChS7aqoN7Ty3fETG9NaC`, status `READY`,
  target `production`.
- `vercel alias set <deployment> www.strikerewind.com` — alias updated.
- `curl https://www.strikerewind.com/` returns the new bundle; grep
  confirms `tier:"FREE` is the literal default in the live JS.
- `node workspace/strikerewind_smoke.mjs` against live —
  **22 pass / 0 fail / 0 unfiltered console errors**. Same suite that
  was green this morning. No regressions.

## Deliberately did NOT
- Route through Cove/Luke (state-management bug, not design/copy).
- Add a Playwright assertion that *specifically* catches the flash —
  would require slow-network mocking or service-worker delay; bundle
  literal-grep is a stronger check than a page-load timing test.
- Touch `Account.tsx` tier badge or upgrade-button visibility (the
  defaults change is the correct fix; UI components consume state).
- Migrate UserContext to react-query or SWR (out of scope, would
  introduce a dependency).

## Why this run
- Today's earlier Playwright run surfaced one missing-route class of
  bug (`/api/stripe/subscription` and `/api/stripe/portal` 404s).
- Sharper next move was: are there *other* frontend → backend mismatches
  of the same shape Travis would hit during `TESTING COMPLETE`?
- Cross-reference came back clean except for this fail-open default,
  which is the same class of "silently wrong customer-facing state"
  that makes the testing playbook longer.
- Closes a bug Travis would have surfaced; doesn't add the gate-stalling
  fix-list churn the playbook is designed to avoid.

## State
- One open gate unchanged: `TESTING COMPLETE: STRIKEREWIND` (Travis-side).
- Cash balance unchanged at `$162.45`.
- No new gate raised, no spend, marketing freeze still in effect.
