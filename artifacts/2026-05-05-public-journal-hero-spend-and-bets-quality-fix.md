# Public journal hero — spend summary + active-bets customer-facing-quality fix

**Date:** 2026-05-05 (4th autonomous run of the day)
**Surface:** `https://autobox.theshepherdstack.com` (Travis links from `theshepherdstack.com`)
**Scope:** journal-build pipeline only — no StrikeRewind / PAF / AdSense / AI Pricing Index changes

## Two regressions found on the live public hero

Curl-probe of the live page during reconcile surfaced two customer-facing-quality issues, in addition to the gate-rendering fix that shipped earlier today:

### 1. Raw ledger note bleeding into the hero spend summary

The hero rendered:

> Started: $200.00, **5 spend ($0.00 on Day 14 — google ads dashboard shows $43.62 total spend apr 26–may 3 ($39.20 perf max + $4.42 search). only $15.05 invoiced so far (per travis). ledger will update when google bills the remainder.)**

Two distinct bugs in `build_hero_context()` at `scripts/build_run_journal.py:1118-1137`:

- **Spend count was wrong** — the loop treated every non-`starting_budget` ledger row as a "spend", so `recurring_started` (no money out yet, just the Render starter pre-approval) and `note` (zero-dollar status commentary) were both counted. PAF has 3 actual expenses; the hero said 5.
- **Last spend resolved to a `note` row** — the "most recent spend" pick fell through to the latest ledger row regardless of type, so the most recent row (a 2026-05-03 `note` recording Google Ads invoicing context) became `last_spend`. Its `note` field was then pasted verbatim into the public hero string with `f" — {note.lower()}"`, exporting raw scaffolding language ("(per travis)", "ledger will update when google bills the remainder") onto the public hero. Direct violation of `RULES.md` rule 14.

There was also a structural pre-condition: `parse_budget()` returned only `ledger[-5:]`, which truncates the very first 2026-04-21 expense ($11.25 PAF domain) — even after fixing the type filter, the count would still be wrong without widening the slice.

### 2. Stale brand + internal git detail in Active bets

The "Active bets" block rendered:

> Profit After Fees · live · paid traffic running
> **StrikeSight scanner · scanner-mvp branch · no real options data yet**
> AI Feature Cost calculator · live under PAF

`STATE.md` line 9 (since 2026-04-28): "App brand is now StrikeRewind everywhere customer-visible." The hero still showed the old brand name and leaked an internal git branch label.

## Fix

Three surgical changes:

1. **`scripts/build_run_journal.py:254`** — `parse_budget()` returns the full ledger instead of `ledger[-5:]`, so the spend tally sees every expense.

2. **`scripts/build_run_journal.py:1118-1137`** — `build_hero_context()`:
   - Filter changed from `e["type"] != "starting_budget"` to `e["type"] == "expense"`. Skips `recurring_started`, `note`, and any future `revenue` entries.
   - Removed the `f" — {note.lower()}"` line entirely. The hero never pastes raw ledger note text again.
   - Reworded summary: `Started: $200.00, {N} expenses, last {amount} on Day {D}` (or `{N} expense` singular).

3. **`config/ACTIVE_BETS.md:8`** — `StrikeSight scanner · scanner-mvp branch · no real options data yet` → `StrikeRewind · pre-launch testing`.

## Verification

Before deploy, in-process test against live state files:

```
ledger rows: 6
types: ['expense', 'note', 'recurring_started', 'starting_budget']
spend_summary: 'Started: $200.00, 3 expenses, last $15.05 on Day 9'
active_bets: [
  {'name': 'Profit After Fees', 'tags': ['live', 'paid traffic running']},
  {'name': 'StrikeRewind', 'tags': ['pre-launch testing']},
  {'name': 'AI Feature Cost calculator', 'tags': ['live under PAF']}
]
```

Build re-ran end-to-end:

```
[hero] day 16 · 2 open gates · 3 active bets
[curation] 65 beats · 70 maintenance
[journal] 135 runs · 19 with runlog · 116 synthesized from artifact
[git] pushed 9ef6cdb (auto: rebuild after run_claude_2026-05-05_081701)
[vercel] deploy ok · Aliased: https://autobox-journal.vercel.app [15s]
```

Live `curl https://autobox.theshepherdstack.com/`:

> Day 16 · $162.45 cash · **Started: $200.00, 3 expenses, last $15.05 on Day 9** · Active bets · Profit After Fees · live · paid traffic running · **StrikeRewind · pre-launch testing** · AI Feature Cost calculator · live under PAF

Clean. No ledger-note bleed-through. No stale brand. No "scanner-mvp branch" leak.

## Why this was the move (4th autonomous run today)

3rd run's handoff steered toward an internal `OptionsDataProvider` planning packet for the 4th run. The wakeup prompt explicitly counter-weights "internal-only docs" against "quality-control" public-facing moves. Curl-probing the live public surface during reconcile (same operator move that surfaced the gate-rendering bug earlier today) found two more regressions — both autonomous, bounded, and on the highest-traffic AutoBox page.

`OptionsDataProvider` planning packet remains the right move on the next autonomous run if no gate moves and no fresh owner input arrives.

## Deliberately NOT done

- NOT routed through Cove — render-time logic fix and a one-line state-file edit, no design judgment.
- NOT routed through Luke — "pre-launch testing" replaces internal scaffolding with a public-honest 2-word tag; not generative copy authoring. Travis can hand-edit ACTIVE_BETS.md any time.
- NOT removed the 2026-05-03 `note` row from `BUDGET.md` — it's a legitimate internal annotation about Google Ads invoicing lag; the public hero just shouldn't render it.
- NOT changed `compute_narrative_weight()` (which also iterates `recent_entries` with the same wider filter) — its inflation effect is internal-only on beat ranking; not customer-visible quality regression.
- NOT pushed unpushed StrikeRewind commits (`095c96b`, `a58a853` on `autobox/strikerewind-rename`) — marketing freeze + Travis testing window still in effect.
- NOT raised a new gate — fix is autonomous and complete; both existing owner-side gates unchanged.
- NOT touched StrikeRewind / PAF / AdSense / AI Pricing Index — out of scope.

## State files updated

- `TODO.md` — DONE row prepended to "Immediate priority order".
- `RUNLOG.md` — appended.
- `HANDOFF.md` — appended.
- `SCORECARD.md` — row added.
- `OPEN_GATES.md` — unchanged (both gates held).
- `BUDGET.md` — unchanged (no spend).
- `config/ACTIVE_BETS.md` — line 8 updated.

Cash balance: `$162.45`. Render starter accruing toward end-of-cycle invoice. Acted on fresh owner input: no — autonomous public-surface QC.
