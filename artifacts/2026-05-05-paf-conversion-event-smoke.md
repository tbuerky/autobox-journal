# PAF conversion-event smoke — guard the only Google Ads signal (2026-05-05)

## Summary
Extended `workspace/paf_smoke.mjs` with three live-runtime assertions that defend the once-per-page Google Ads conversion fire in `app/app.js:fireConversionOnce`. The Search campaign extended through 2026-05-18 relies on this single signal to learn which paid clicks turned into real interactions; before today the smoke covered calculator math but had zero coverage on the conversion path. Smoke runs **36/36 pass / 0 fail / 0 console errors** against live `https://profitafterfees.com`.

## Why now
- Active paid spend: PAF Search campaign extended to 2026-05-18, accruing ~$1.50 max CPC.
- The conversion event was the bug we shipped a fix for on 2026-04-28 (unconditional `gtag('event', 'conversion', ...)` in `<head>` → moved inside `form.addEventListener('input', ...)` with one-shot guard). No live-surface test catches a regression of that fix.
- StrikeRewind moves are gated behind `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` (both Travis-side); a quality-control move on the live PAF revenue path is the highest-leverage autonomous option that doesn't pile more work onto the public AutoBox journal hero (which the prior two runs already cleaned up).
- Bounded: 3 new assertions, 1 file edited, no source-tree change to PAF, no deploy required.

## What changed

`workspace/paf_smoke.mjs` (+38 lines):

1. **Spy install** right after the `#calculator-form` present check, before the first user-interaction. `window.gtag` is replaced with a wrapper that pushes call args to `window.__gtagCalls` and forwards to the real GTM gtag. `networkidle` above guarantees the inline GTM gtag stub has already been defined, so the spy supersedes it.

2. **Assertion: gtag fired exactly once after submit.** After the existing submit click + math assertions, count entries in `__gtagCalls` matching `(c[0] === 'event' && c[1] === 'conversion')`. Must be exactly 1.

3. **Assertion: send_to matches `AW-18121518600/WxyuCLjh56McEIjcgcFD`.** The exact conversion id Google Ads expects. Catches a refactor that swaps the id silently.

4. **Assertion: stays at one call after additional input (Once semantic).** Programmatically dispatches an `input` event on `listPrice`, waits 250ms, re-counts conversion calls. Must still be exactly 1. Catches a regression that re-introduces the unconditional fire pattern.

No edits to `app/app.js` itself, no PAF deploy. The page in production already passes the new assertions.

## Verification

Run:
```
cd workspace && OUT_DIR="../artifacts/2026-05-05-paf-conversion-event-smoke" node paf_smoke.mjs
```

Output (live PAF):
```
PASS  Conversion: gtag fired exactly once after submit — 1 conversion calls
PASS  Conversion: send_to matches AW-18121518600/WxyuCLjh56McEIjcgcFD — AW-18121518600/WxyuCLjh56McEIjcgcFD
PASS  Conversion: stays at one call after additional input (Once semantic) — total conversion calls: 1
...
36 pass / 0 fail / 0 console errors
```

Run output saved to `artifacts/2026-05-05-paf-conversion-event-smoke/summary.json`.

## Behavioral impact

- The next time PAF source changes (Luke copy scrub, Cove layout pass, app.js refactor), running the smoke before deploy catches a conversion-tracking regression that would otherwise silently waste paid Search spend.
- Live-runtime check confirms the 2026-04-28 fix is still working as of today: exactly one `gtag('event', 'conversion', { send_to: 'AW-18121518600/WxyuCLjh56McEIjcgcFD' })` call per page session, regardless of how many input events the visitor produces.
- No effect on StrikeRewind (out of scope), AdSense (separate property), or AI Pricing Index (already covered by smoke).

## Deliberately did NOT

- **Add a parallel unit test in `tests/`** — the regression scenario is "deploy ships and conversion silently breaks." A unit test against a mocked DOM would be lower-fidelity than the live-runtime spy. The smoke runs in `~10s` and now covers both math and conversion in one shot — that's the right shape.
- **Route through Cove/Luke** — test infrastructure work, not customer-facing copy or design.
- **Touch `app/app.js`** — the conversion logic is correct; the test was missing.
- **Trigger a PAF deploy** — no source-tree change to the deployed PAF bundle.
- **Raise a new gate** — fix is autonomous and complete.
- **Push StrikeRewind unpushed commits `095c96b` (PriceDataProvider) + `a58a853`** — marketing freeze + Travis testing window still in effect.
- **Run the smoke headed / capture video** — extra noise; the screenshots already exist at `artifacts/2026-05-05-paf-conversion-event-smoke/01-apex-desktop.png` etc. for next-run diff.

## State files

- `TODO.md` — new `[DONE]` row at top of "Immediate priority order".
- `RUNLOG.md` — appended.
- `HANDOFF.md` — appended.
- `SCORECARD.md` — appended.
- `OPEN_GATES.md` — unchanged. `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` both held; no fresh owner input.
- `BUDGET.md` — unchanged. Balance `$162.45`. Render starter still accruing ≈ $0.23/day.

## What this unblocks

Future PAF deploys can rely on `npm test && node workspace/paf_smoke.mjs` as a real two-stage gate (source-tree + live-runtime, with Google Ads conversion tracking included). The single Google Ads conversion signal that the running Search campaign through 2026-05-18 depends on is now defended.
