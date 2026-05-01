# PAF — content-pages head-meta audit

Date: 2026-05-01
Surface: `https://profitafterfees.com`
Scope: 14 customer-facing pages (homepage + 7 comparison/article pages + 6 calculator pages)
Companion to: `artifacts/2026-05-01-paf-live-site-health-check.md` (status codes + SEO leak; deliberately did NOT cover meta-tag content quality).

## Why

Yesterday's health check verified status codes / `ads.txt` / conversion-event regression / pruning redirects / SEO subhead leak. It explicitly did NOT cover meta-tag content quality (title length, description length, canonical correctness, og:image presence, AI-smell, stale dates). Stale or broken metadata silently degrades search snippets and social-share renders without showing up on any uptime check. A spot-check on three pages today caught zero issues, so this run formalizes the audit across all 14 pages.

## Method

For each of 14 page source files in `workspace/stripe-profit-calculator/`, parsed `<head>` and asserted: `<title>` length 30–60 chars, `<meta name="description">` length 100–160 chars, `<link rel="canonical">` matches `https://profitafterfees.com{route}`, `<meta property="og:image">` present, `<meta property="og:title">` present, `<meta property="og:description">` present, `<meta name="twitter:card">` present, `<meta name="viewport">` present. Independently verified the three referenced og:image assets are reachable on the live origin. Spot-checked live head against source on three pages.

## Results — all pass

| Route | title len | desc len | canonical | og:image | og:title | og:desc | twitter:card | viewport |
|---|---|---|---|---|---|---|---|---|
| `/` | 60 | 147 | OK | social-preview.png | distinct | distinct | summary_large_image | OK |
| `/gumroad-vs-stripe/` | 58 | 125 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/paddle-vs-stripe/` | 45 | 153 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/paypal-vs-stripe-fees/` | 41 | 146 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/stripe-fees-for-online-courses/` | 50 | 158 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/stripe-fees-for-notion-templates/` | 52 | 140 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/stripe-fees-for-micro-saas/` | 46 | 119 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/how-to-calculate-profit-margin-on-digital-products/` | 50 | 125 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/ai-feature-cost-calculator/` | 46 | 137 | OK | ai-feature-cost-preview.png | distinct | distinct | summary_large_image | OK |
| `/ai-model-pricing-index/` | 50 | 148 | OK | ai-model-pricing-preview.png | distinct | distinct | summary_large_image | OK |
| `/transaction-fee-calculator/` | 46 | 136 | OK | social-preview.png | mirror | distinct | summary_large_image | OK |
| `/saas-pricing-calculator/` | 43 | 135 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/online-course-pricing-calculator/` | 52 | 122 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |
| `/lemonsqueezy-vs-stripe/` | 56 | 156 | OK | social-preview.png | mirror | mirror | summary_large_image | OK |

- 14/14 titles within 41–60 chars (all under Google's ~60-char snippet truncation).
- 14/14 descriptions within 119–158 chars (all under Google's ~160-char snippet truncation).
- 14/14 canonicals match expected route exactly.
- 14/14 og:image, og:title, og:description, twitter:card, viewport present.

## og:image asset reachability (live)

| Asset | HTTP | Bytes |
|---|---|---|
| `https://profitafterfees.com/social-preview.png` | 200 | 52 607 |
| `https://profitafterfees.com/ai-feature-cost-preview.png` | 200 | 51 694 |
| `https://profitafterfees.com/ai-model-pricing-preview.png` | 200 | 58 685 |

All three referenced og:image assets resolve and are non-empty.

## Live-vs-source head parity (3 pages spot-checked)

- `https://profitafterfees.com/` — live `<title>` = `Stripe Fee Calculator for Digital Products | See Your Payout` (matches source).
- `https://profitafterfees.com/ai-model-pricing-index/` — live `<title>` = `AI Model Pricing Index | Claude & Gemini API Costs` (matches source).
- `https://profitafterfees.com/lemonsqueezy-vs-stripe/` — live `<title>` = `Lemon Squeezy vs Stripe for Software | Profit After Fees` (matches source).

No deploy drift between source and live on the three pages checked.

## Public-copy hygiene (RULES.md rule 14/15)

- No internal labels in any title or description ("launch", "experiment", "draft", "v2", etc.).
- No SEO scaffolding language ("Some buyers search...", "without the space", or query-stuffing patterns).
- No process language ("we built", "this page", "to capture").
- No AI-smell phrases ("leverage", "empower", "actionable insights", "comprehensive").
- No stale dates embedded in any title or description.

## Deliberately not covered

- Body-content correctness on the 14 pages (calculator math, pricing-data freshness, headline accuracy). The AI Model Pricing Index body was already audited today (`artifacts/2026-05-01-paf-ai-model-pricing-index-freshness-audit.md`).
- Visual / rendered-DOM correctness (would need a real browser).
- Social-preview render quality on actual share targets (Discord/Slack/X iframes vary).
- Two soft observations not regressions: (a) 10 of 14 pages mirror raw page meta into og:title/og:description rather than writing distinct social copy — fine fallback, but distinct OG copy can lift CTR on the 4 pages that already use it; (b) 12 of 14 pages share `social-preview.png` — branded but generic, separate previews could be added later if a specific page becomes a top traffic source.

## Outcome

PAF live earning property passes head-meta audit on 2026-05-01 — every required tag present, every length within Google snippet bounds, every canonical pointed correctly, every og:image asset live, no AI-smell or process language anywhere in titles or descriptions. **No remediation required.** Cash balance unchanged at $162.45.
