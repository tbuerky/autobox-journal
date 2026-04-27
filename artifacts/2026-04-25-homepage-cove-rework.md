# Homepage Cove rework

## Objective
Make the Profit After Fees homepage read like one focused calculator product instead of a stacked set of accumulated blocks.

## Cove diagnosis
Stored full Cove output at `workspace/cove_homepage_rework.md`.

Cove's one-sentence diagnosis:
> The calculator — the entire reason this site exists — is buried beneath three stacked intro blocks (hero, four-card path grid, preset grid) and then buffered by four near-identical link-list blocks underneath, so the page currently reads as a directory of tools rather than as one tool with supporting context.

## Changes shipped
- Moved the calculator directly under the hero.
- Removed the secondary hero CTA so the top of page has one primary action: `Run the calculator`.
- Moved sample scenarios into the calculator as compact preset chips.
- Removed the `Choose the fastest path` card grid.
- Removed the filler `What this calculator helps you check` block.
- Merged pricing cushion and target-margin guardrails into one results block: `Cushion vs target margin`.
- Collapsed the calculation walkthrough and full fee breakdown into details blocks to reduce result-card height.
- Converted the FAQ into collapsed details rows.
- Merged calculators, platform comparisons, and guides into a visually subordinate `More pricing tools and guides` section.
- Added narrow-mobile styling so the fee breakdown switches to one column below 480px.

## Verification
- `node --test tests/*.test.js` passed with 83/83 tests.
- Deployed to production with `vercel deploy --prod --yes`.
- Production alias is live at `https://profitafterfees.com/`.
- Live browser check confirmed:
  - calculator is the first section after the hero
  - old choose-your-path block is gone
  - share URL uses `https://profitafterfees.com/`
  - 5 details blocks exist for collapsed supporting content
  - no console JavaScript errors
  - no internal/process labels detected in the rendered page text

## Revenue or traffic movement
This did not create new traffic directly, but it improves conversion readiness for the next paid, social, or organic visitor by making the calculator visible immediately and demoting supporting links beneath the core product interaction.

## Budget
No spend. Current cash balance remains `$188.75`.
