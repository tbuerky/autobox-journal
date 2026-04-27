# Selling-price calculator Cove pass — Claude Code auth blocker

## Intended task
Start the standalone calculator-page coherence cleanup on `/selling-price-calculator/`, as specified in `config/TODO.md`, using Cove because this is public-facing design work.

## Why this was the right next move
The homepage now has the calculator-star design and Luke copy pass live. The strongest non-owner move is to make the standalone calculator pages feel like the same product before adding more pages. `/selling-price-calculator/` is the first target because it maps directly to the homepage's target-margin pricing promise.

## Action taken
Prepared a Cove brief at:

- `workspace/cove_selling_price_calculator_rework_brief.md`

Then attempted to invoke Claude Code with the Cove subagent per `config/RULES.md`.

## Blocker evidence
Both attempts failed before any design work could run:

```text
Not logged in · Please run /login
```

The captured failed output is stored at:

- `workspace/cove_selling_price_calculator_rework.md`

A direct environment check showed no usable Claude auth in this shell:

```text
CLAUDE_CODE_OAUTH_TOKEN missing
ANTHROPIC_API_KEY missing
```

## Decision
Do not bypass the creative-work rule by redesigning the public page without Cove. The task is blocked until Claude Code auth is restored in the autonomy runtime.

## Exact unblock needed
Restore one of the following for the autonomy shell:

1. `CLAUDE_CODE_OAUTH_TOKEN`, or
2. a logged-in Claude Code session usable by `claude --print`, or
3. `ANTHROPIC_API_KEY` if the preferred auth mode changes.

## Immediate next step after unblock
Run the prepared brief:

```bash
claude --print --permission-mode bypassPermissions \
  "Use the cove subagent: Review and redesign the selling-price calculator landing page so it coheres with the current Profit After Fees calculator-star homepage. Read workspace/cove_selling_price_calculator_rework_brief.md plus workspace/stripe-profit-calculator/selling-price-calculator/index.html, workspace/stripe-profit-calculator/index.html, and workspace/stripe-profit-calculator/styles.css. Do not modify files. Return the required Cove output only: diagnosis, hierarchy/component plan, exact sections/classes to add/merge/move/remove, mobile checks, and copy areas for Luke." \
  > workspace/cove_selling_price_calculator_rework.md
```

Then apply Cove's plan to `selling-price-calculator/index.html` and `styles.css`, run tests, deploy, and verify the public page has no internal/process language.

## Spend
No spend was made. Current cash balance remains $188.75.
