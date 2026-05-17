# WordPress Review Pulse Sample Run

Date: 2026-05-17 22:20 UTC

## Decision

Created a fresh active-business validation artifact outside the currently gated Shopify Review Pulse lane: **WordPress Review Pulse**, a one-off WordPress.org plugin review and support-forum teardown for plugin authors.

This is not a second broad research cycle. The current top Review Pulse path is blocked on `SEND: A2REVIEWS FALLBACK FROM REVIEWPULSE MAILBOX`, and the newest operating correction says not to spend another run rechecking a documented sender gate.

## Why This Lane

The parent category is already proven by Shopify/browser-extension review analytics and report products already documented in the workspace. WordPress adds a cleaner public data source: WordPress.org exposes plugin detail pages, review distributions, support topic pages, public author profiles, last-modified dates, and an LLM-friendly Markdown view using `?output_format=md`.

Live evidence checked this run:

- `https://wordpress.org/plugins/ai-engine/?output_format=md`
- `https://wordpress.org/support/plugin/ai-engine/reviews/?output_format=md`
- `https://wordpress.org/support/plugin/ai-engine/?output_format=md`
- Live search result for AI Engine showed `4.9/5` across 830+ reviews.
- Live search result for WPBot showed `4.7/5` across 118 reviews.
- Live search result for StoreSEO on Shopify showed 600+ reviews, reinforcing that review-language extraction remains a proven install-conversion category across app/plugin ecosystems.

## Built

- `workspace/wordpress-review-pulse/wordpress_review_pulse.mjs`
- `workspace/wordpress-review-pulse/README.md`
- `workspace/wordpress-review-pulse/sample-ai-engine-report.md`

The generator fetches the WordPress.org details, reviews, and support pages for a plugin slug using `?output_format=md`, parses rating/review counts, review topic titles, support topic titles, support-page depth, and recurring themes, then writes a buyer-facing Markdown report focused on listing copy, Free-vs-Pro clarity, setup confusion, and public reply drafts.

Sample target:

- `AI Engine - The Chatbot, AI Framework & MCP for WordPress`
- Author parsed: `Jordy Meow`
- Rating parsed: `4.9/5` across `831` reviews
- Support depth parsed: `49` support pages
- First-page support themes included MCP/Claude Desktop setup, Pro pre-sales, upgrade/update questions, chatbot frontend issues, API response problems, settings disappearing, and model-support questions.

## Offer

First price test: `$49` one-off.

Deliverable:

- revised WordPress.org short description
- "Which setup do I need?" docs block
- Free vs Pro clarity block
- support/forum reply drafts
- screenshot-caption rewrites
- one upgrade-page proof strip based on public review language

## Approval Needed

`APPROVED: CONTACT ONE WORDPRESS PLUGIN AUTHOR WITH WORDPRESS REVIEW PULSE SAMPLE`

## If Approved

Contact one plugin author only, preferably a commercial plugin with 100+ reviews and active support traffic. Use the sample report to ask whether a `$49` one-off review/support teardown would be useful. Do not batch-send.

## Guardrails

- No outreach was sent.
- No public page was changed.
- No checkout/payment infrastructure was created.
- No account was created.
- No DNS changed.
- No public post was published.
- No spend occurred.
