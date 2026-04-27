# Publish-ready launch packet for the Stripe calculator

Date: 2026-04-21
Task: Create a publish-ready launch packet using the new preset links and search-intent positioning.

## What shipped
A workspace-local launch packet was created under `workspace/stripe-profit-calculator/launch/` with:
- `launch-packet.md` containing positioning, preset links, three launch post variants, CTA copy, and a day-one distribution checklist
- `forum-answers.md` containing reusable reply templates for common pricing questions
- `search-cluster.md` containing a tiny sitemap and tightly scoped supporting content plan

## Why this is publish-ready
The packet turns the current calculator into a deployable promotion bundle rather than a standalone page:
- Preset scenario URLs are already assembled for Notion templates, cohort courses, and micro-SaaS pricing.
- Copy is written so a future publish step only needs a live `BASE_URL` substituted.
- Search expansion stays constrained to pages that map directly to the existing calculator and presets.

## Files created
- `workspace/stripe-profit-calculator/launch/launch-packet.md`
- `workspace/stripe-profit-calculator/launch/forum-answers.md`
- `workspace/stripe-profit-calculator/launch/search-cluster.md`

## Verification
- Confirmed preset query strings directly from `workspace/stripe-profit-calculator/app/scenarios.js` using a Node command.
- Verified all launch packet files were written inside the current workspace and artifacts directories only.
- Checked that the packet content matches the current page positioning in `workspace/stripe-profit-calculator/index.html`.

## Current limitation
No external publish or traffic step was attempted in this run. The packet is prepared for a later launch once a live URL is chosen.

## Next likely step
Use the approved TSS GitHub/Vercel accounts to publish the calculator and replace `BASE_URL` in the launch packet with the actual deployed URL.
