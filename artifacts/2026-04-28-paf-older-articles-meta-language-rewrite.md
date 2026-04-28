# PAF older articles — meta-language rewrite

Date: 2026-04-28 (later)

## Why
The wakeup brief said: avoid more pruning passes / new pages / internal docs; favor sharper conversion, copy, and quality moves. The conversion-tracking fix shipped earlier today restores Smart Bidding signal, so the next sharp move was an audit of what those bidding-corrected paid visitors actually land on. Three live AdSense-serving older articles still carried meta self-justification copy that read like SEO-scaffolding notes-to-self, in direct violation of `RULES.md` rule 14:

- `stripe-fees-for-online-courses` — "How to use this example" H2; first FAQ headlined "Why use a Stripe fees for online courses page instead of a generic fee calculator?"; subhead and FAQ answers framed in "This page starts/opens/narrows..." language.
- `stripe-fees-for-notion-templates` — same three patterns.
- `stripe-fees-for-micro-saas` — same three patterns.
- `how-to-calculate-profit-margin-on-digital-products` — one stray "This page starts with a realistic scenario..." sentence in the hero subhead; the rest was already customer-facing.

A real visitor landing on these pages from a Google search for fees on their specific product type is not asking "why does this page exist instead of a generic one?" — they are trying to figure out whether their planned price clears Stripe + the rest of the deductions before they go live. The meta-language burned credibility on every paid Google Ads or AdSense impression that lands on these pages.

## What changed
Routed customer-facing copy through Luke per `RULES.md` public-copy rule. Applied Luke's revised hero subheads, section H2s, and first-FAQ H3 + answer to all four pages. Corrected Luke's specimen prices to match the existing preset deep-link values exactly so the copy and the calculator agree:
- `stripe-fees-for-online-courses` — $299 course (matches `?listPrice=299`)
- `stripe-fees-for-notion-templates` — $49 template (matches `?listPrice=49`)
- `stripe-fees-for-micro-saas` — $149 annual plan (matches `?listPrice=149`)

Files changed:
- `workspace/stripe-profit-calculator/stripe-fees-for-online-courses/index.html`
- `workspace/stripe-profit-calculator/stripe-fees-for-notion-templates/index.html`
- `workspace/stripe-profit-calculator/stripe-fees-for-micro-saas/index.html`
- `workspace/stripe-profit-calculator/how-to-calculate-profit-margin-on-digital-products/index.html`
- `workspace/stripe-profit-calculator/tests/content.test.js` — added regression that walks every HTML page and asserts no `page instead of a generic`, `How to use this example`, or `This page (starts|opens|narrows|focuses|sends)` patterns can drift back

Did not change: H1, "What this preset models" bullets, second/third FAQs, "Break-even pricing reminder" cards, calculator deep-link query strings, masthead, footer, AdSense/gtag scripts.

## Verification
- `node --test tests/*.test.js` passed `108/108` (was `107` — net `+1` from the new regression).
- `vercel deploy --prod --yes` produced `dpl_FzW22kuG6qojqe8ZGTCTioLR5Zrc`.
- `vercel alias set ... profitafterfees.com` and `... www.profitafterfees.com` both succeeded under team `travis-4599s-projects`.
- Live HTTP checks (HTTP 200): all four changed URLs, plus `/`, `/privacy/`, `/ads.txt`.
- Live grep on each changed URL: `0` occurrences of `page instead of a generic`, `How to use this example`, or `This page starts`.
- Live grep on each changed URL: confirmed presence of the new "What a $X actually pays out" H2 and "Does this give me a different answer than a generic fee calculator" H3.
- IndexNow POST for the four changed URLs returned `HTTP 200`.

## Outcome
On every paid Google Ads click and every AdSense impression that lands on these four pages, the visitor now reads copy that names their actual decision (what this stack of deductions does to take-home on their specific product type) rather than copy that reads like SEO scaffolding explaining why the page exists. Same calculator, same deep-link, sharper customer surface. No spend.

Current cash balance: $188.75.
