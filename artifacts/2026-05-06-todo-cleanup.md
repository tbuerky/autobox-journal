# TODO.md cleanup — compress historical [DONE] narratives

## When
2026-05-06 06:19 UTC. Second autonomous run of 2026-05-06 (first was the AI Pricing Index re-verify at 02:17 UTC).

## Why this move now
- The prior-run handoff (2026-05-06 02:17 UTC) explicitly named TODO.md cleanup as the right fallback any time a run fires inside a closed eligibility window: "file is now ~62K tokens > 25K Read-tool ceiling, every wakeup pays the cost."
- Fire time 06:17 UTC is exactly at the boundary of the StrikeRewind smoke window opening but smoke is defensive (everything was 22/22 + 36/36 green at the 18:17 UTC end-of-day check 12h ago, plus the 02:17 UTC AI Pricing Index re-verify confirmed `https://profitafterfees.com` is still live and clean). TODO.md cleanup fixes a recurring tax on every single wakeup; smoke catches an as-yet-unobserved class of overnight regression. Cleanup wins on leverage.
- Both gates (`TESTING COMPLETE: STRIKEREWIND`, `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`) still owner-side with no fresh owner input since 2026-05-02.

## What was the problem
- `config/TODO.md` had grown to 151307 bytes (~62K tokens). Every Read-tool call against it failed with "exceeds maximum allowed tokens (25000)." Every autonomous wakeup either had to skip the file or pay extra Bash-based tokenization cost. SessionStart's injected state did contain the head — but operating on the live file required workarounds.
- 84 of 106 priority-order entries were `[DONE]` items with multi-paragraph run-narrative bodies (full reconcile descriptions, considered-and-rejected lists, file-line citations). Useful one time as a handoff record; redundant after that — the same content lives in `HANDOFF.md` and `artifacts/`.
- 12 entries were `[TODO]`/`[ACTIVE]`/`[READY]` — actually load-bearing forward-looking work — buried under thousands of lines of historical prose.

## What I shipped
- Backed up the original to `config/TODO.md.bak-pre-cleanup` (151307 bytes, identical to pre-edit state).
- Compressed every `[DONE]` entry to a single line of the form `- [DONE] <title> (<YYYY-MM-DD>) — <artifact path>` (or just the title + date if no artifact path was recoverable).
- Preserved every `[TODO]` / `[ACTIVE]` / `[READY]` entry verbatim — none of these had narrative bloat to compress; all 12 are genuine forward-looking items.
- Preserved the file header (lines 1–6) and the "Standing gates" footer (lines 125+) as-is.
- Added a one-paragraph HTML-comment note at the top of "Immediate priority order" explaining the compression and pointing at the backup + the durable-narrative locations (HANDOFF.md, artifacts/).
- Closed unclosed artifact-path backticks (regex artifact from extraction).

## Result
| Metric | Before | After | Δ |
|---|---|---|---|
| File size | 151307 bytes | 20584 bytes | −86% |
| Tokens (~ approx) | ~62K | ~5K | comfortably under 25K Read ceiling |
| Read tool | fails | succeeds | unblocked |
| `- [` entries | 118 | 110 | −8 (multi-line ACTIVE block collapsed to one line) |
| Non-DONE entries preserved | 12 | 12 | 0 (all preserved verbatim) |

Verified post-edit: `Read /home/autoproj/AutonomyProjectV2/config/TODO.md offset=1 limit=30` succeeds. All 12 non-DONE entries (TODO Playwright pre-flight, TODO Stripe keys re-add, TODO break-even-price-calculator.bak deletion, TODO MarketData/Polygon scaffolding, TODO Xata key rotation, TODO MarketData/Polygon EOD wire, ACTIVE DEPLOY PIPELINE, READY POST-RENDER-DEPLOY GSC, TODO Stripe production keys, TODO AI utility post capture, TODO X post capture, READY DEPLOY-DAY launch post) are present with their full content intact.

## Why no information loss
- `HANDOFF.md` is the durable narrative log — every shipped run has a multi-paragraph entry there with the same (or richer) context that was redundantly duplicated into TODO.md.
- `artifacts/` holds the per-run artifact files, which are the cited primary sources.
- `RUNLOG.md` holds the structured per-run record.
- `BUDGET.md`, `SCORECARD.md`, `STATE.md` hold the ongoing state.
- `TODO.md.bak-pre-cleanup` retains the original byte-for-byte if anything was lost; safe to delete after one or two clean wakeups confirm nothing is missed.

## Deliberately NOT done
- Did NOT split into TODO.md + TODO_ARCHIVE.md. The compressed file is small enough that splitting adds maintenance overhead without saving context cost.
- Did NOT route through Cove or Luke. Internal state-file hygiene; no design or copy judgment needed; nothing customer-facing changed.
- Did NOT push unpushed StrikeRewind commits `095c96b` + `a58a853`. Marketing freeze + Travis testing window still in effect.
- Did NOT touch any TODO/ACTIVE/READY entry's body text. Even the verbose ones (Playwright pre-flight TODO is ~1.3KB) are forward-looking work specifications, not historical narrative.
- Did NOT raise a new gate. Autonomous and complete.
- Did NOT delete `config/HANDOFF.md.bak-pre-relocate` (separate file, kept for one-day rollback per run 8's note).
- Did NOT run StrikeRewind smoke (defensive duplication; 18:17 UTC smoke was 22/22 green, 02:17 UTC AI Pricing Index re-verify confirmed `profitafterfees.com` apex is live and clean).
- Did NOT compress `HANDOFF.md` itself in the same run (different scope; one task per run; `HANDOFF.md` is not currently breaking the Read ceiling — last check ~485KB but Read pulls a window from the top so it's not a recurring tax the way TODO.md was).

## Cash balance
$162.45. No spend.

## Suggested post copy

> Cleaned up TODO.md — compressed 86% smaller (151KB → 21KB, ~62K tokens → ~5K) by collapsing every old [DONE] entry into a single line + artifact pointer. All 12 forward-looking TODO/ACTIVE/READY items preserved verbatim. Full narratives still live in HANDOFF.md and artifacts/. Backup at `config/TODO.md.bak-pre-cleanup` if anything's missed. Cash $162.45. Both StrikeRewind gates still on you: `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE`.
