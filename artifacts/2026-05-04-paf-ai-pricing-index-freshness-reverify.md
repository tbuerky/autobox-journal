# PAF AI Model Pricing Index — freshness re-verify (2026-05-04)

## Summary
All 6 published rates on `/ai-model-pricing-index/` match the live provider sources exactly. No price corrections needed. Bumped "Last verified May 1, 2026" → "Last verified May 4, 2026" so the freshness signal the page advertises ("AI pricing changes often — sometimes mid-quarter, sometimes overnight") matches actual verification cadence. Fixed one pre-existing failing regression test left over from yesterday's Luke scrub. Tests `78/78` pass. Deployed `dpl_9Rjmi2cxZQejG1e32ncmxiW26yGe`. Live verified.

## Why now
- Live, passive PAF earner that advertises a freshness contract on the page itself.
- 3 days since last verify (2026-05-01) — past reasonable cadence given the page's own copy.
- All StrikeRewind moves are gated behind `TESTING COMPLETE: STRIKEREWIND` (Travis-only); freshness work on a live PAF page is the highest-leverage autonomous move.
- Bounded: 6 rates against 2 source pages.

## Rates verified (all match)

| Model | Page shows | Live provider | Status |
|---|---|---|---|
| Claude Sonnet 4.6 | $3.00 / $15.00 | $3 / $15 (claude.com docs) | ✓ match |
| Claude Haiku 4.5 | $1.00 / $5.00 | $1 / $5 | ✓ match |
| Claude Opus 4.7 | $5.00 / $25.00 | $5 / $25 | ✓ match |
| Gemini 2.5 Flash | $0.30 (text/image/video) / $2.50 | $0.30 / $2.50 | ✓ match |
| Gemini 2.5 Flash-Lite | $0.10 (text/image/video) / $0.40 | $0.10 / $0.40 | ✓ match |
| Gemini 2.5 Pro | $1.25 (≤200k) / $10.00 (≤200k) | $1.25 / $10.00 (≤200k) | ✓ match |

Sources: `https://platform.claude.com/docs/en/docs/about-claude/pricing` (claude.com/pricing now redirects to consumer plans only — docs page is the system of record for API rates) and `https://ai.google.dev/gemini-api/docs/pricing`.

Note for next re-verify: the live Anthropic source now also publishes Opus 4.5/4.6, Sonnet 4.5, Haiku 3.5 — page editorial choice keeps to "latest production model in each family" so these are deliberately omitted, consistent with prior runs.

## Edits applied
1. `workspace/stripe-profit-calculator/ai-model-pricing-index/index.html:66` — date bumped to May 4, 2026.
2. `workspace/stripe-profit-calculator/tests/content.test.js:982` — regression literal updated to match new date.
3. `workspace/stripe-profit-calculator/tests/content.test.js:761` — pre-existing failing assertion fixed: `"See your real margin after the checkout stack takes its cut"` → `"See your real margin after fees, VAT, affiliates, and refunds"`. Yesterday's Luke scrub changed the H1 text on `/profit-margin-calculator/` but the regression test was not updated alongside the deploy. The live page already had the new H1; the test was stale and was the only failure on `node --test tests/content.test.js`. Fix is one regex update; not fixing it would let other regressions hide behind a test suite that already returns red.

## Verification
- `node --test tests/content.test.js` → `78/78 pass` (was `77 pass / 1 fail` before edit 3).
- `vercel deploy --prod --yes` (token `VERCEL_TOKEN_TSS`, project `stripe-profit-calculator`).
- Deployment `dpl_9Rjmi2cxZQejG1e32ncmxiW26yGe`, status `READY`, target `production`. Aliased to `profitafterfees.com`.
- `curl -s https://profitafterfees.com/ai-model-pricing-index/ | grep -c "Last verified May 4, 2026"` → `1`.
- `... | grep -c "Last verified May 1, 2026"` → `0`.
- 6 model row mentions live; 12 rate cell entries live (6 input + 6 output as expected).

## Deliberately did NOT
- Route through Cove/Luke — content correctness work, no design or copy judgment.
- Add the Opus 4.6 / Opus 4.5 / Sonnet 4.5 / Haiku 3.5 rows now visible on the Anthropic source — page editorial principle is one row per family, latest model only; widening would dilute scannability.
- Change the Gemini 2.5 Pro >200k tier disclosure — out of scope for re-verify; potential future enhancement if Pro becomes a higher-traffic linked source.
- Touch any other PAF page — bounded re-verify, not a sweep.
- Raise a new gate — no owner action required.

## State files
- `TODO.md` — `[DONE]` line at top.
- `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` — appended.
- `OPEN_GATES.md` — unchanged. `TESTING COMPLETE: STRIKEREWIND` remains.
- `BUDGET.md` — unchanged. Balance `$162.45`. Render starter still accruing ≈ $0.23/day.

## What this unblocks
Freshness contract on `/ai-model-pricing-index/` is honored against today's actual provider rates. The next visitor reading "Last verified May 4, 2026" sees a date matching reality, not a 3-day-old claim. Side effect: PAF test suite is now green again, which means the next deploy can use `npm test` as a real gate instead of working around a known stale failure.
