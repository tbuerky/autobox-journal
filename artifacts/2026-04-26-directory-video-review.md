# Owner video review — Claude Code built me a $273/day online directory

Video reviewed: https://youtu.be/I_wbc5ND79o?si=BQYC0z7v6wjdxZDU
Date: 2026-04-26 08:19 UTC

## Source evidence available

- YouTube page was reachable in browser, but playback/transcript access was blocked by YouTube bot-sign-in protection.
- `youtube-transcript-api` was installed in a local venv and retried, but YouTube blocked transcript retrieval from this cloud IP.
- The video description and chapter list were visible and enough to evaluate the operating lessons.
- Visible description says Greg Isenberg interviews Frey Chu about using Claude Code to build AI-coded directories and, especially, how to get valuable data.
- The described live walkthrough: a luxury restroom trailer directory built in four days for under $250.
- Visible key points: data is the moat; directories help users save time, save money, or make money; monetization can be lead generation, vertical SaaS, agency services, ads, debit cards, affiliate, or marketplace models; directories still work when users are in decision mode.

## What is useful for Autonomy Project V2

1. The data moat point is the strongest takeaway.
   A directory only becomes useful when it has information users cannot get quickly from a generic search result. For this project, that means the next useful asset should not be another generic article. It should package decision data: costs, prices, comparisons, thresholds, and scenario links.

2. The boring-niche thesis fits the current direction.
   Profit After Fees and the AI Feature Cost Calculator are both boring utility plays. That is good. The video supports staying in narrow, practical, decision-support utilities rather than chasing broad creator/audience plays.

3. The directory format is useful only if paired with a narrow commercial decision.
   The relevant pattern is not "build a directory because directories are hot." The relevant pattern is "collect structured data around a buying/pricing decision and turn it into pages/tools that help a user choose."

4. The AI Feature Cost Calculator has a natural data-asset extension.
   A model/API pricing index would make the calculator more trustworthy and more discoverable: model name, provider, input token cost, output token cost, cached-token cost where available, notes, last checked date, and a prefilled calculator scenario link.

5. Distribution improves if the asset contains data people can cite.
   A post that says "free calculator" is weaker than a post that says "I built a calculator plus a current model-pricing table so builders can compare GPT/Claude/Gemini costs before shipping an AI feature."

## What is not applicable now

1. Do not pivot into a broad local-business directory.
   Funeral homes, senior living, gas prices, and restroom trailers may be valid examples, but starting a separate scraped local directory would require niche selection, scraping spend, data QA, legal caution, and a new monetization path. That is too much surface area before the current live assets have first user evidence.

2. Do not spend on Outscraper or data vendors yet.
   The video example spent under $250, but this project has $188.75 cash remaining and no evidence yet that a paid data directory would outperform the already-live utilities. Any paid scrape would require explicit approval and a tighter business case.

3. Do not treat the $273/day headline as proof.
   The useful lesson is the process: narrow data, cleaning, enrichment, verification, and monetization path. The headline revenue claim should not drive spend or a pivot without independent validation.

4. Do not build a big searchable directory before proving demand.
   The current highest-leverage version is a small, manually curated data asset attached to an existing calculator, not a multi-week database product.

## Concrete next action recommended

Build a no-spend `AI model pricing index` companion asset for the live AI Feature Cost Calculator.

Recommended scope for the next run:

- Create a small manually curated table for 8-12 common AI models/providers.
- Include input token price, output token price, provider link/source, last checked date, and a direct "calculate this model" link into `/ai-feature-cost-calculator/`.
- Add one short customer-facing intro: "Compare model costs before you ship an AI feature."
- Link it from the AI calculator page, not the main Profit After Fees homepage unless it becomes a stronger standalone asset.
- Keep it free and no-login.
- Do not scrape, buy data, or use paid APIs.

Why this is the best next move:

- It applies the video's strongest lesson — data is the moat — without pivoting into an unrelated directory business.
- It improves the parallel AI calculator's usefulness before asking Travis to post again.
- It creates a more citeable public asset for AI/SaaS builders, which can make the existing distribution packet stronger.
- It avoids spending money and avoids legal/quality risk from scraping local-business data.
- It is small enough to ship and verify in one run.

## Approval gates

No approval is needed for a manually curated, source-linked pricing table.

Approval would be needed later if:

- Travis wants to buy a standalone domain for the AI calculator/index.
- The project wants to use paid scraping/data vendors.
- The project wants to create payment infrastructure.
- The project wants to publish under Travis's real identity.

## Recommendation summary

Do not copy the video by starting a new broad directory. Copy the operating principle: build a narrow data moat around a decision users already need to make. For Autonomy right now, that means turning the AI Feature Cost Calculator into a small data-backed AI model pricing utility before another owner-side distribution ask.

Current cash balance: $188.75.
