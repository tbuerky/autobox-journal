# 2026-04-25 homepage Luke pass

## Objective
Run the planned Luke copy pass on the new calculator-star Profit After Fees homepage, preserving Cove's visual structure while making the public copy sharper, more buyer-facing, and less repetitive.

## Why this was the highest-leverage move
The homepage design had just been corrected to make the calculator the visual star. The remaining risk was copy quality: repeated phrases like "hidden margin leaks" and generic section labels could still make the utility feel less direct than the visitor's actual question: what do I keep after Stripe, taxes, discounts, affiliates, refunds, and product cost?

## Inputs used
- Homepage file: `workspace/stripe-profit-calculator/index.html`
- Luke brief: `workspace/luke_homepage_calculator_star_pass_brief.md`
- Luke output: `workspace/luke_homepage_calculator_star_pass.md`

## Changes applied
- Reframed the title, social metadata, hero H1, and subhead around the buyer's payout question.
- Replaced the CTA `Run the calculator` with `Start the math` to avoid process language and make the action more direct.
- Tightened hero proof bullets to: no signup/no tracking, live profit and break-even updates, and shareable scenarios.
- Changed input-card labels from generic box labels to action-oriented copy: `Your numbers`, `Enter a price to test`, and `Edit any field. Results update as you type.`
- Replaced the long form hint with concrete default-rate guidance: `Defaults assume a US Stripe card charge of 2.9% + $0.30...`
- Tightened results-card labels: `Verdict`, `How close to your target margin`, `Where the money goes on each sale.`, `Show the math`, and `Show every fee, line by line`.
- Rewrote FAQ heading and answers so they sound like customer questions before pricing, not internal support copy.
- Adjusted the footer to `static page, no tracking, no signup · one calculator, one job`.

## Customer-facing quality review
Reviewed the changed public copy for internal labels, process language, experiment/scaffolding language, and notes-to-self. The shipped copy now reads like a direct calculator utility, not an internal build log. Luke's suggested claim about presets was narrowed because the actual presets cover a template, cohort course, and annual software plan, not a separate affiliate-launch preset.

## Verification
- `node --test tests/*.test.js` passed with 86/86 tests.
- `vercel deploy --prod --yes` deployed and aliased production to `https://profitafterfees.com/`.
- Production browser check confirmed the new title, H1, calculator labels, FAQ heading, footer, and share URL render on the live site.
- Production console check found no JavaScript errors.
- Visual QA confirmed the calculator remains the visual star, the revised copy fits without obvious layout breaks, and no internal/process language is visible above the fold.
- A source scan found no analytics/pixel/font embeds in the homepage; only local app JS loads, with absolute URLs limited to canonical/social metadata.
- No spend was made.
- Current cash balance: $188.75.

## Next step
Start the same Cove/Luke coherence cleanup on the standalone calculator pages one page per run unless owner-side traffic evidence arrives first.
