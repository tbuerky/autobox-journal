# AI utility social preview cards

## Objective
Make the AI Feature Cost Calculator and AI Model Pricing Index more click-worthy when Travis shares them with AI/SaaS builders. This is a traffic/conversion move: the public link preview should sell the exact builder problem before a user clicks.

## Shipped
- Added dedicated large-card social metadata to `https://profitafterfees.com/ai-feature-cost-calculator/`.
- Added dedicated large-card social metadata to `https://profitafterfees.com/ai-model-pricing-index/`.
- Created two 1200×630 PNG preview images:
  - `https://profitafterfees.com/ai-feature-cost-preview.png`
  - `https://profitafterfees.com/ai-model-pricing-preview.png`
- Added a regression test so both AI pages keep dedicated `summary_large_image` cards and image metadata.
- Added `.vercelignore` so local helper/venv/internal folders do not get uploaded with production deployments.

## Public-facing copy/design review
Cove/Luke were routed through Claude Code because this changed public-facing copy/design. Their initial guidance was adjusted before shipping:
- Avoided unverified claims like “every model,” “weekly,” or “12 models tracked.”
- Used current page facts only: Claude/Gemini rows and calculator margin modeling.
- Reworked both preview images after visual QA found text overflow and process-like phrasing.
- Final visual QA found no obvious overflow, no internal/process labels, and no CAPTCHA or rendering issues.

## Verification
- `node --test tests/*.test.js` passed: 110/110.
- Production deploy completed and re-aliased `https://profitafterfees.com`.
- Live checks returned HTTP 200 for both pages and both PNGs.
- Live metadata checks confirmed:
  - `summary_large_image`
  - page-specific preview PNG URLs
  - `AI Feature Cost Calculator — Claude & Gemini Margins`
  - `Claude vs Gemini Pricing — Side by Side`
- Discord update delivered as message `1497999618196111410`.

## Revenue / traffic movement
No direct traffic or revenue landed inside the sandbox. This improves the next distribution action by making the AI utility links present as polished, builder-specific assets instead of generic Profit After Fees pages when shared on X, Reddit, Discord, LinkedIn, or Slack.

## Budget
No spend. Current cash balance remains `$188.75`.
