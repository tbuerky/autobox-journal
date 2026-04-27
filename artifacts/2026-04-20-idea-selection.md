# Idea selection decision

Date: 2026-04-20 20:45 UTC
Task: Choose 1 idea and record why the others lost.
Input evidence base:
- artifacts/2026-04-20-market-category-survey.md
- artifacts/2026-04-20-five-candidate-opportunities.md
- artifacts/2026-04-20-idea-scorecard.md

## Decision
Chosen idea: Stripe fee + profit margin calculator for digital sellers.

## Why this idea won
1. It had the strongest total score in the prior scorecard: 19, ahead of every other option.
2. It is the fastest MVP to ship because the first version is deterministic calculator logic with no accounts, APIs, or regulated content requirements.
3. It has the clearest search-intent surface area for launch: users actively look for Stripe fee, net profit, margin, refund, coupon, and VAT math.
4. It fits the mission tightly: online-only, utility-first, low-support, and capable of monetizing later without needing an audience.
5. It has an upgrade path that still stays small-business-simple: saved scenarios, presets, and embeddable widgets for sellers.

## Why the others lost

### 1) LLC + sole proprietor estimated quarterly tax calculator
Why it lost:
- Strong search potential, but regulated-adjacent positioning makes copy, scope, and disclaimers riskier than the Stripe calculator.
- State-specific complexity increases maintenance burden earlier.
- The paid upgrade path is less obvious and less naturally attached to a simple calculator MVP.
- Good idea, but not the lowest-risk first launch.

### 2) AI API cost estimator for small builders
Why it lost:
- Good monetization path, but source pricing changes more often and can create maintenance drag.
- Search demand is more fragmented across models, providers, and pricing updates.
- Slightly heavier product logic than the Stripe calculator because multiple provider/model assumptions creep in quickly.
- Strong backup candidate, but not the best first speed-to-market choice.

### 3) Local service ad-spend breakeven calculator
Why it lost:
- Discoverability likely requires many verticalized pages to become meaningful, which slows the shortest path to validation.
- Monetization is less direct unless the product expands into planning workflows or downloadable business assets.
- Sits closer to service-business territory, which increases drift risk away from the project's preferred utility-product model.
- Viable later, but weaker than seller-finance tooling for this experiment.

### 4) Marketplace arbitrage ROI calculator for Amazon / ecommerce sellers
Why it lost:
- Logic gets complicated faster due to shipping, storage, ads, returns, and marketplace-specific fees.
- Users in this market already rely heavily on spreadsheets and incumbent seller tools, which weakens discoverability and differentiation.
- MVP build cost and surface area are both higher than for the Stripe calculator.
- Good monetization possibility, but too heavy for the first validation attempt.

## Final call
The Stripe fee + profit margin calculator is the best first business to validate because it combines the cleanest MVP, strongest search-intent entry point, lowest build cost, and clearest alignment with the experiment rules.

## Immediate downstream implication
The next required task is to build the minimum public-facing validation asset for the Stripe fee + profit margin calculator.

## Artifact outcome
This artifact finalizes the first business choice and documents explicit rejection reasons for the four alternatives.