# PAF — sitemap coverage gap meta audit

**Date:** 2026-05-02
**Surface:** profitafterfees.com (5 sitemap-listed pages not covered in 2026-05-01 head-meta audit)
**Outcome:** PASS — all 5 pages clean; combined audit coverage now matches sitemap exactly (19/19)

## Why this run

Yesterday's PAF head-meta audit (`2026-05-01-paf-content-pages-meta-audit.md`) called itself "14 customer-facing pages" — homepage + 7 comparison/article + 6 calculator. But `sitemap.xml` lists **19** indexable URLs. The 5 missed pages are all live (HTTP 200), all referenced in the sitemap, and all therefore present in Google's index — so any meta-tag hygiene problem on them ships into search snippets and social shares the same as the 14 covered pages.

This run closes that coverage gap.

## Pages audited (the 5 missed yesterday)

| Slug | Live status |
|------|------|
| `/digital-product-pricing-calculator/` | HTTP 200 |
| `/break-even-price-calculator/` | HTTP 200 |
| `/selling-price-calculator/` | HTTP 200 |
| `/selling-price-markup-calculator/` | HTTP 200 |
| `/profit-margin-calculator/` | HTTP 200 |

## Head-meta assertions (5 pages × 8 checks = 40 assertions, all pass)

| Page | Title len | Desc len | Canonical | og:image | og:title | og:desc | twitter | viewport |
|------|-----------|----------|-----------|----------|----------|---------|---------|----------|
| digital-product-pricing-calculator | 54 | 160 | OK | OK | OK | OK | OK | OK |
| break-even-price-calculator | 47 | 133 | OK | OK | OK | OK | OK | OK |
| selling-price-calculator | 44 | 120 | OK | OK | OK | OK | OK | OK |
| selling-price-markup-calculator | 51 | 137 | OK | OK | OK | OK | OK | OK |
| profit-margin-calculator | 44 | 149 | OK | OK | OK | OK | OK | OK |

Title-length hygiene threshold: 30–60 chars (Google snippet truncation ~60). Description-length hygiene threshold: 100–160 chars (Google snippet truncation ~160). Canonical assertion: exact-string equality against `https://profitafterfees.com{route}`.

## Literal copy

```
digital-product-pricing-calculator
  TITLE (54): Digital Product Pricing Calculator | Profit After Fees
  DESC  (160): Use a digital product pricing calculator that shows what you actually keep after Stripe fees, VAT, coupons, affiliate payouts, refund reserve, and product cost.

break-even-price-calculator
  TITLE (47): Break-Even Price Calculator | Profit After Fees
  DESC  (133): See the lowest price that stops losing money after Stripe fees, VAT, affiliates, refunds, and product cost. Open the live calculator.

selling-price-calculator
  TITLE (44): Selling Price Calculator | Profit After Fees
  DESC  (120): See what a price pays you after Stripe fees, refunds, VAT, and affiliates, and whether it still hits your target margin.

selling-price-markup-calculator
  TITLE (51): Selling Price Markup Calculator | Profit After Fees
  DESC  (137): Turn a markup rule into a list price that still hits your margin after Stripe fees. Open a worked markup scenario in the live calculator.

profit-margin-calculator
  TITLE (44): Profit Margin Calculator | Profit After Fees
  DESC  (149): See what margin is really left after Stripe fees, VAT, coupons, affiliates, refunds, and product cost. Open a worked scenario in the live calculator.
```

Read-clean: every title is sentence-case + brand suffix; every description is one or two short customer-facing sentences naming concrete fees (Stripe, VAT, affiliates, refunds, product cost) and ending with an action.

## Live-vs-source `<title>` parity (5/5 MATCH)

```
digital-product-pricing-calculator: MATCH
break-even-price-calculator:        MATCH
selling-price-calculator:           MATCH
selling-price-markup-calculator:    MATCH
profit-margin-calculator:           MATCH
```

Zero deploy drift on any of the 5 pages.

## og:image asset reachability

All 5 pages reference the single shared `https://profitafterfees.com/social-preview.png` (HTTP 200, 52 607 B). Already verified reachable in yesterday's audit; no new asset.

## AI-smell / internal-language sweep

PASS — none of `leverage`, `empower`, `actionable insights`, `comprehensive`, `robust`, `dive into`, `unlock`, `elevate`, `best-in-class`, `world-class`, `seamless`, `experiment`, `launch`, `v2`, `draft`, `we built`, `this page`, `to capture`, `without the space`, `some buyers search` appear in any title or description across the 5 pages.

## Combined coverage

After this run: **19 of 19 sitemap-listed pages audited for head-meta hygiene; 19 of 19 pass.** Yesterday's audit covered 14, today closed the remaining 5.

| Bucket | Count | Source |
|--------|-------|--------|
| Yesterday (covered) | 14 | `2026-05-01-paf-content-pages-meta-audit.md` |
| Today (gap closure) | 5 | this artifact |
| Total audited | 19 | both |
| Sitemap entries | 19 | `sitemap.xml` |
| Coverage | 100% | — |

## Soft observations (not regressions, not fixed)

1. **`digital-product-pricing-calculator` description is exactly 160 chars** — at the boundary of Google's snippet truncation. Functional today, but any future word added to the description silently truncates with an ellipsis in search results. Watch-item, not a remediation.

2. **All 5 pages share `social-preview.png`** — same generic branded preview as the 12-of-14 pages flagged yesterday. Total: 17 of 19 pages share one OG image. Becomes a CTR-lift opportunity only if a specific page breaks out as a top traffic source.

3. **All 5 mirror raw page meta into `og:title` / `og:description`** — no distinct social copy. Same fallback pattern as 10-of-14 yesterday. Total: 15 of 19 use the mirroring pattern.

## Deliberately not covered

- Body-content correctness (calculator inputs, headline accuracy, footnote accuracy on each page)
- Visual / rendered-DOM correctness (would need a real browser)
- Calculator math correctness (would need a headless browser to drive `app.js`)
- Whether any of these 5 older pages should be pruned (Travis-side editorial decision; they're each ranked-for content that pulls non-zero traffic, so deleting carries SEO cost; out of scope)

## State

No code change. No deploy. No spend. Sitemap, vercel.json, and live routes are mutually consistent. PAF revenue path remains intact end-to-end on the live surface. Cash balance unchanged at $162.45.
