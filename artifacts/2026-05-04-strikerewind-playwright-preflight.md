# StrikeRewind Playwright pre-flight — green

**Run date:** 2026-05-04
**Target:** https://www.strikerewind.com (Render backend `srv-d7r408favr4c73fb3670`)
**Result:** 22 pass / 0 fail / 0 unexpected console errors
**Artifacts:** `artifacts/2026-05-04-strikerewind-playwright-smoke/` (8 full-page screenshots + `summary.json`)

## What this run covers (matches the prior INTERACTIVE handoff's spec)

| Area              | Test                                               | Result |
|-------------------|----------------------------------------------------|--------|
| Landing           | Renders                                            | PASS   |
| Analyze tab       | `/dashboard` loads                                 | PASS   |
| Analyze AAPL      | Ticker, EV %, current price `$189.42`, body > 500c | PASS   |
| Analyze AAPL      | Strategy matrix heading present                    | PASS   |
| Analyze nav       | URL `/analysis/AAPL`, active color resolved        | PASS   |
| Error state ZZZZZ | "Could not load" heading                           | PASS   |
| Error state ZZZZZ | Ticker name in heading                             | PASS   |
| Error state ZZZZZ | Back button present                                | PASS   |
| Error state ZZZZZ | Back button navigates to `/dashboard`              | PASS   |
| Hunt tab          | Not blank, action button present                   | PASS   |
| Watch tab         | Not blank, heading/empty-state copy present        | PASS   |
| Account tab       | Not blank, FREE/STANDARD/PRO cards rendered        | PASS   |
| Mobile (390×844)  | No horizontal overflow on landing                  | PASS   |

The test sets `localStorage.userId = "travis-pro-tester"` before navigation so usage limits behave deterministically against the real backend.

## What got fixed this run

1. **Backend `/api/stripe/subscription` and `/api/stripe/portal` were 404**
   The frontend's `Account.tsx` calls `getSubscriptionInfo()` on mount; the missing route polluted the console with `Subscription info error: le` and silently broke the Manage Subscription button. Added both routes:
   - `GET /api/stripe/subscription` returns `null` for users with no subscription (FREE tier) or `{status, tier}` for paid users.
   - `POST /api/stripe/portal` proxies `StripeServiceDB.createPortalSession`.
   Backend `tsc` clean; 13/13 unit tests pass.
   Commit `27a5633`, deployed to Render and verified live before the smoke run.

2. **Smoke-test assertion strength**
   The prior smoke test used a 200-char threshold to detect "blank page" — produced a false fail on `/analysis/ZZZZZ` because the error UI is intentionally minimal (110 chars). Replaced with explicit assertions for the actual UI: heading "Could not load", ticker in heading, Back button presence, Back-button navigation. Now: blank-screen regressions fail loudly, intentional minimal UI passes.

3. **Console-error filter**
   The ZZZZZ test deliberately triggers a 500 from `/api/analyze`; that 500 and the resulting `Failed to fetch analysis` log are expected, not regressions. Filter ignores them so an unexpected error stands out.

## What was already working before this run

- AAPL Analyze flow renders correctly (commit `49bd4ac` from 2026-05-03 reshapes the fixture response to the full `AnalysisResult` contract — verified live).
- Error UI on `/analysis/ZZZZZ` (Analysis.tsx:88-101) — `AlertCircle`, "Could not load {ticker}", error message, Back button.
- Nav active state on `/analysis/*` (Analyze tab highlights green `rgb(34, 197, 94)`).

## What is intentionally NOT covered by this suite (and why)

- **Hunt run end-to-end:** would burn fixture/scan credits on every smoke run; verified the Run Hunt button is present, that's the right scope here.
- **Watchlist add/remove:** requires a real ticker analysis result first, then chaining clicks. Out of scope for v1; can add in a follow-up if a watchlist regression ships.
- **Stripe Upgrade clicks:** explicit `do NOT click Upgrade` in the prior handoff (live Stripe).
- **Sign-up / login:** auth is anonymous-localStorage, no flow to test.

## How to re-run

```
cd /home/autoproj/AutonomyProjectV2
OUT_DIR="artifacts/$(date +%F)-strikerewind-playwright-smoke" \
  node workspace/strikerewind_smoke.mjs
```

Override `BASE_URL` to point at staging if/when one exists.

## Next move

`TESTING COMPLETE: STRIKEREWIND` is the only open gate. The Playwright suite passing means the live site has no infrastructure-level regressions for Travis to discover; he can sit down with the testing playbook (`artifacts/2026-05-03-strikerewind-testing-playbook.md`) and judge UX rather than QA setup. Suite output is reproducible — re-run before any future "ready to test" handoff per the saved feedback memory.
