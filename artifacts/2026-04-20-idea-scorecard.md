# Scoring the 5 candidate opportunities

Date: 2026-04-20 13:05 UTC
Task: Score the 5 ideas for speed, monetization realism, discoverability, and build cost.
Input evidence base:
- artifacts/2026-04-20-market-category-survey.md
- artifacts/2026-04-20-five-candidate-opportunities.md

## Scoring method
Scale used for each criterion:
- 5 = strongest fit
- 3 = acceptable / mixed
- 1 = weak fit

Interpretation:
- Speed: how quickly a useful first public version can be shipped
- Monetization realism: how believable the upgrade or paid path is without requiring a big audience or manual sales
- Discoverability: how likely the idea is to attract search-driven or obvious intent traffic
- Build cost: 5 means cheapest / simplest to build, 1 means costliest / heaviest to build

## Score table
| Idea | Speed | Monetization realism | Discoverability | Build cost | Total |
|---|---:|---:|---:|---:|---:|
| Stripe fee + profit margin calculator | 5 | 4 | 5 | 5 | 19 |
| LLC + sole proprietor estimated quarterly tax calculator | 4 | 3 | 5 | 4 | 16 |
| AI API cost estimator for small builders | 4 | 4 | 4 | 4 | 16 |
| Local service ad-spend breakeven calculator | 4 | 3 | 4 | 4 | 15 |
| Marketplace arbitrage ROI calculator for Amazon / ecommerce sellers | 3 | 4 | 3 | 3 | 13 |

## Rationale by idea

### 1) Stripe fee + profit margin calculator
Scores: speed 5, monetization realism 4, discoverability 5, build cost 5

Why:
- Fastest to ship because the first version is just deterministic calculator logic with no user accounts, live integrations, or regulated edge cases.
- Strong search intent is plausible around exact queries tied to Stripe fees, margin, pricing, VAT, refunds, and discount calculations.
- Build cost is very low for a public MVP because the initial feature set can be a single-page tool.
- Monetization is realistic but not automatic; the paid path likely depends on saved scenarios, presets, or embeddable widgets rather than charging for the calculator itself.

### 2) LLC + sole proprietor estimated quarterly tax calculator
Scores: speed 4, monetization realism 3, discoverability 5, build cost 4

Why:
- High discoverability because people search exact scenario-based tax estimate questions.
- Still relatively fast to launch as an estimation tool.
- Slightly weaker monetization realism because the clean paid upgrade path is less obvious than for seller tooling.
- Slightly lower speed/build score because state-specific complexity and careful disclaimer positioning raise implementation and maintenance risk.

### 3) AI API cost estimator for small builders
Scores: speed 4, monetization realism 4, discoverability 4, build cost 4

Why:
- Fits directly into narrow SaaS / AI utility demand seen in the market survey.
- Monetization is believable via saved scenarios, provider comparisons, and team sharing.
- Discoverability is good but narrower than the Stripe calculator because search demand is more fragmented by provider, model, and pricing-change cycles.
- Build cost stays modest, but handling multiple providers and changing pricing tables is a little heavier than a fixed-fee calculator.

### 4) Local service ad-spend breakeven calculator
Scores: speed 4, monetization realism 3, discoverability 4, build cost 4

Why:
- MVP is still simple calculator logic.
- Discoverability can work through verticalized pages, but this likely requires multiple niche landing pages to win meaningful traffic.
- Monetization feels weaker because the target users may resist paying unless the tool expands into budgeting workflows or downloadable planning assets.
- Also sits closer to service-business territory, which is allowed as tooling but not as the business model itself.

### 5) Marketplace arbitrage ROI calculator for Amazon / ecommerce sellers
Scores: speed 3, monetization realism 4, discoverability 3, build cost 3

Why:
- The category has real money in the market survey, but the tool logic gets heavier quickly once fees, shipping, storage, returns, and ad assumptions expand.
- The audience is real, yet discoverability is less clean because many sellers already use spreadsheets or marketplace-native tools.
- Monetization is believable for repeat evaluators, but the MVP is less obviously lightweight than the top-ranked options.

## Ranking
1. Stripe fee + profit margin calculator — 19
2. LLC + sole proprietor estimated quarterly tax calculator — 16
3. AI API cost estimator for small builders — 16
4. Local service ad-spend breakeven calculator — 15
5. Marketplace arbitrage ROI calculator for Amazon / ecommerce sellers — 13

## Decision produced by this run
The strongest next-step candidate is the Stripe fee + profit margin calculator.

Why it won this scoring pass:
- fastest to ship
- strongest discoverability fit
- cheapest MVP build
- clear overlap with online-only sellers and micro-software monetization

Important constraint:
This run does not finalize the project choice yet. It only completes the scoring task. The next run should explicitly choose one idea and record why the others lost.

## Artifact outcome
This artifact converts the five candidate ideas into a ranked scorecard that can support the next required decision.