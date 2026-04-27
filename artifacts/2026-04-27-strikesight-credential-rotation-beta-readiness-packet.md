# StrikeSight credential-rotation + beta-readiness packet

Created: 2026-04-27 10:18 UTC

## Current bottleneck

StrikeSight is close enough to a beta path that the next limiting factor is not another UI tweak. The scanner builds, boots, has a deterministic Hunt smoke path, and the repo no longer tracks the known production env/credential files.

The remaining blocker before production deploy, paid data credentials, payment setup, or beta outreach is key rotation for any real secrets that were ever committed.

## Why this matters now

A paid beta requires trust. If we connect a domain, add MarketData.app/Polygon credentials, enable Stripe, or send traders to a scanner while old committed secrets may still be live, we create avoidable launch risk.

This is also the cleanest prerequisite before spending the proposed ~$60/mo on real options data. Rotate first, then integrate provider data behind the existing scanner flow.

## Evidence

- Active branch checked: `autobox/strikesight-scanner-mvp`.
- Latest StrikeSight commits checked:
  - `f54afdf chore: remove tracked credential files`
  - `1bfa37a test: add deterministic hunt fixture smoke path`
  - `15a18b6 fix: stabilize scanner MVP startup and build`
- Current tracked env-ish files are examples only:
  - `backend/.env.example`
  - `backend/.env.supabase.example`
  - `frontend/.env.example`
- Previously tracked real/production-looking files included:
  - `backend/.env.production`
  - `frontend/.env.production`
  - `credentials.txt`
- Actual secret values were not printed into this artifact.

## Recommended action

Travis should rotate any real credentials that were ever present in those previously tracked files before approving public deploy, paid data provider credentials, payment setup, or beta traffic.

## Owner checklist

1. Rotate Supabase/database credentials that appeared in old tracked env files.
2. Rotate Xata credentials/database URLs that appeared in old tracked env files.
3. Rotate Stripe keys/webhook secrets that appeared in old tracked env files.
4. Rotate Sentry DSN/project credentials if they were real and still active.
5. Rotate email/SMTP/API credentials if they were real and still active.
6. Rotate any app/session/JWT/encryption secrets from old env files.
7. Confirm no production service still accepts the old values.
8. Reply with one of the exact statuses below.

## Exact reply options

`ROTATED: STRIKESIGHT KEYS READY`

Use this when all real credentials from the old tracked env/credential files have been rotated or confirmed dead.

`PARTIAL: STRIKESIGHT ROTATION BLOCKED ON <service>`

Use this if one service is blocked and tell AutoBox which service.

`DEFER: STRIKESIGHT PUBLIC BETA`

Use this if StrikeSight should stay local/unlaunched for now while Profit After Fees / AI utility distribution remains the priority.

## What AutoBox should do immediately after each reply

### If `ROTATED: STRIKESIGHT KEYS READY`

Proceed with the next approved StrikeSight monetization step:

1. If data-provider approval also exists, integrate MarketData.app or Polygon real options data behind an `OptionsDataProvider` interface.
2. If domain approval also exists, buy `getstrikesight.com` only under the approved cap and do not route traffic until the data smoke is credible.
3. Run a paid-beta-ready Hunt smoke using real chain strikes plus fixture-backed regression tests.
4. Prepare one beta-facing scanner demo artifact or weekly-scan content loop.

### If `PARTIAL: ...`

Hold public deploy and paid credentials. Create a narrow service-specific fix packet and do not add new secrets until the named service is resolved.

### If `DEFER: STRIKESIGHT PUBLIC BETA`

Stop spending StrikeSight cycles except for safe maintenance. Rotate back to the active Profit After Fees / AI Feature Cost Calculator acquisition loop, especially Google Ads status, manual post URLs, or builder feedback.

## Recommendation

Ask Travis for `ROTATED: STRIKESIGHT KEYS READY` before any StrikeSight deploy or paid provider integration.

This is the highest-leverage non-spend move because it unlocks the real revenue path: credible scanner beta -> real options data -> paid users, without carrying avoidable secret-exposure risk into launch.

## Budget impact

No spend required for this step. Current cash balance remains `$188.75`.
