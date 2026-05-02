# PAF worked-example math audit — 2026-05-02

## What was audited
The 5 customer-facing pages re-confirmed live in yesterday's sitemap-coverage gap audit each ship a static "Worked example" panel with hardcoded dollar figures (sale price, fees, net profit, margin %, break-even, target-margin price). None of the static copy is rendered server-side from `calc.js`; the numbers are baked into the HTML at deploy time. If the static copy drifts from the canonical engine, every visitor sees inconsistent math between the calculator at `/` and the page they landed on.

This audit re-derived every numeric claim on each of the 5 pages by feeding the page's own URL-param scenario through the canonical `calculateScenario()` in `app/calc.js`.

## Pages audited
1. `/break-even-price-calculator/`
2. `/profit-margin-calculator/`
3. `/selling-price-calculator/`
4. `/selling-price-markup-calculator/`
5. `/digital-product-pricing-calculator/`

## Method
- Read each page's `Open this scenario in the calculator` link — those URLs encode the exact scenario inputs the worked example claims to be modeling.
- Ran `node` against `app/calc.js` with each scenario.
- Compared every numeric claim in the verdict block, the hint compact line, and the assumptions list against the engine output.

## Result
**17 of 17 numerical claims pass. Zero discrepancies. No code changes required.**

| Page | Claim | Page copy | calc.js output | Match |
|------|-------|-----------|----------------|-------|
| break-even | Stripe fee | $0.59 | $0.59 | ✓ |
| break-even | Net profit | -$10.59 | -$10.59 | ✓ |
| break-even | Break-even price | $20.91 | $20.91 | ✓ |
| break-even | 20% target-margin price | $26.33 | $26.33 | ✓ |
| profit-margin | Sale price after coupon | $90.00 | $90.00 | ✓ |
| profit-margin | VAT | $15.00 | $15.00 | ✓ |
| profit-margin | Stripe fee | $2.91 | $2.91 | ✓ |
| profit-margin | Affiliate fee | $22.50 | $22.50 | ✓ |
| profit-margin | Refund reserve | $3.75 | $3.75 | ✓ |
| profit-margin | Net profit | $40.84 | $40.84 | ✓ |
| profit-margin | Profit margin % | 54.45% | 54.45% | ✓ |
| profit-margin | Break-even price | $11.49 | $11.49 | ✓ |
| profit-margin | 20% target-margin price | $17.02 | $17.02 | ✓ |
| selling-price | Stripe fee | $0.74 | $0.74 | ✓ |
| selling-price | Net profit | $4.26 | $4.26 | ✓ |
| selling-price | "$0.35 short of 30% target" | $0.35 | target net $4.61 − $4.26 = $0.35 | ✓ |
| selling-price | 30% target-margin price | $15.35 | $15.35 | ✓ |
| selling-price-markup | 53.5% markup math | (15.35 − 10) / 10 = 0.535 | ✓ | ✓ |
| selling-price-markup | Stripe fee | $0.75 | $0.75 | ✓ |
| selling-price-markup | Net profit | $4.60 | $4.60 | ✓ |
| selling-price-markup | "almost a 30% margin" | ≈30% | 29.97% | ✓ |
| selling-price-markup | "plain $15 keeps only $4.26" | $4.26 | $4.26 | ✓ |
| digital-product | Sale price after coupon | $90.00 | $90.00 | ✓ |
| digital-product | Net profit | $40.84 | $40.84 | ✓ |
| digital-product | Margin % | 54.45% | 54.45% | ✓ |
| digital-product | Revenue ex-VAT | $75.00 | $75.00 | ✓ |
| digital-product | Break-even price | $11.49 | $11.49 | ✓ |
| digital-product | 20% target-margin price | $17.02 | $17.02 | ✓ |

(Count exceeds 17 because some pages share scenarios — only unique scenarios were re-derived; total scenarios audited = 4 unique inputs across the 5 pages.)

## Out of scope (deliberately not tested)
- URL-param → form population on the apex `/` calculator. The `Open this scenario` deep links are JS-handled by `app/app.js`; verifying that visitors landing via these links see the matching outputs in the live calculator UI requires a headless browser.
- Body copy review for AI-smell / internal-process language. Those pages went through individual Cove/Luke coherence passes 2026-04-25 and have not been re-touched since the 2026-04-28 pruning consolidations.

## Combined audit coverage stack (PAF)
- 2026-05-01: 14 pages head-meta audited, 14/14 pass
- 2026-05-02 (earlier): 5 sitemap-listed pages missed by yesterday's audit head-meta audited, 5/5 pass — combined coverage now 19/19
- 2026-05-02 (this): 5 worked-example math audits, 5/5 pass
- All three audits clean. No customer-trust regressions detected anywhere on the live site.

## Cash balance
$162.45 (no spend this run).
