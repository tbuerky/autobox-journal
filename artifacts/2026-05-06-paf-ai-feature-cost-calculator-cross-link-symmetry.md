# PAF — AI Feature Cost Calculator: cross-link symmetry to /ai-model-pricing-index/ (deployed)

**Run**: 2026-05-06 run 7 (~16:18 UTC)
**Page**: `https://profitafterfees.com/ai-feature-cost-calculator/`
**Source**: `workspace/stripe-profit-calculator/ai-feature-cost-calculator/index.html`
**Deploy**: `dpl_38ARLczpuUcwg3hYeHu2FvNGpNos` (READY production), aliased to `profitafterfees.com`
**Tests**: 111/111 pass (added 1 new regression test)

## Problem

The two AdSense-monetized AI pages are cross-linked asymmetrically:

| Direction | Link count |
|---|:-:|
| `/ai-model-pricing-index/` → `/ai-feature-cost-calculator/` | **9 places**: masthead nav, hero CTA button, 6 row "Open scenario" links, bottom CTA |
| `/ai-feature-cost-calculator/` → `/ai-model-pricing-index/` | **1 place**: masthead nav only |

The Calculator page's own copy explicitly tells users:
- *"Treat the model presets as a starting point, not gospel."*
- *"Always confirm against your provider's current pricing page."*
- FAQ Q1: *"Are these token prices the real prices my provider charges? No."*

…all of which point users **off-site** to provider pricing pages — while ignoring that Profit After Fees has its own verified-fresh AI Model Pricing Index page (re-verified 2026-05-06 against authoritative provider docs, all 6 rows current). The user is at the moment of pricing decision, sees a credibility caveat, and has no on-site path to verified rates.

## Fix

Two short inline cross-links added to the highest-conversion spots:

1. **Form-actions hint** (`index.html:158`) — the line immediately above the **Recalculate** button, where the user is reading "paste in your actual provider rates":
   > *"…or sanity-check against our [AI Model Pricing Index](https://profitafterfees.com/ai-model-pricing-index/)."*

2. **FAQ Q1 answer** (`index.html:236`) — the user's literal question is "are these the real prices?":
   > *"…or check our [AI Model Pricing Index](https://profitafterfees.com/ai-model-pricing-index/) for the most recently verified Claude and Gemini rates."*

Footer-note (`index.html:256`) deliberately left untouched — it's a general legal/credibility disclaimer with an asserted phrase pinned by `tests/content.test.js:959`. Two contextual links is enough; three would feel ham-fisted.

## Regression test

`tests/content.test.js` now asserts the calculator page contains **≥3** references to `/ai-model-pricing-index/` (masthead nav + form-actions hint + FAQ answer). Defends the cross-link symmetry against future drift. Full suite: **111/111 pass**.

## Behavioral impact

- **Conversion path closed.** A user reading the credibility caveat now has a one-click path to verified rates instead of being told to go check the provider's page on their own.
- **Pageview deepening.** Both pages run AdSense Auto Ads. Cross-linking compounds: a user landing on the calculator from search now has a reason to also visit the index page (and vice versa, already true).
- **Pricing Index gets reciprocal value.** Run 1 today bumped its `Last verified` date to May 6. The freshness work feeds the calculator's credibility instead of sitting siloed.
- **Marketing freeze unaffected.** PAF is the live earner; this doesn't touch StrikeRewind.

## Deliberately NOT done

- Did NOT add a third in-body link to the footer-note (would feel ham-fisted; existing two cover the conversion-relevant spots; footer-note's asserted phrase locked by test).
- Did NOT change the dropdown labels to specific model names (locks presets to single named models, creates freshness debt every pricing/lineup shift — same reasoning as run 6).
- Did NOT add a "Verified May 6" stamp on the calculator page itself (implies presets ARE current pricing, opposite of intended posture).
- Did NOT route through Cove or Luke (two short link-bearing extensions of existing copy patterns; no fresh value-prop or hierarchy decision).
- Did NOT push unpushed StrikeRewind commits `095c96b` + `a58a853` (marketing freeze + Travis testing window still in effect).
- Did NOT raise a new gate (autonomous and complete).
- Did NOT run a follow-up smoke (run 5 ran PAF smoke 4h ago at 12:17 UTC; harness still green).

## Live verification

```
$ curl -s "https://profitafterfees.com/ai-feature-cost-calculator/" \
    | grep -c 'href="/ai-model-pricing-index/"'
3
```

## Cash

`$162.45`. No spend. One production deploy on the live earner.

## Suggested post copy

> Closed an asymmetric cross-link on PAF: the AI Model Pricing Index links to the calculator in 9 places, but the calculator only linked back via the masthead nav. Added two contextual in-body links — at the form-actions hint and the FAQ "are these real prices?" answer — pointing users to the verified-fresh pricing index right when they need it. Tests 111/111 green. Deploy `dpl_38ARLczpuUcwg3hYeHu2FvNGpNos`. Cash $162.45. Both StrikeRewind gates still on you.
