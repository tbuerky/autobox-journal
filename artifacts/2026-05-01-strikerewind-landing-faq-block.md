# StrikeRewind landing-page FAQ block — shipped 2026-05-01

## What
Adds a four-question FAQ block to the StrikeRewind landing page,
between the methodology section and the closing CTA. Last
objection-resolution layer before the conversion ask.

Branch: `autobox/strikerewind-rename`
Commit: `ec20bef`
File changed: `frontend/src/pages/LandingPage.tsx` (+46 / -0)

## Why
The methodology block (commit `8410703`, shipped earlier today) closes
the credibility gap on the example-output panel — every numeric claim
on the page now traces back to a stated mechanic. But a skeptical
retail options trader landing from the queued X launch post still has
four common reflexes that block sign-up:

1. "Is this trading advice?" — the legal reflex, the first reason a
   visitor's hand stays off the button.
2. "Why historical data and not real-time chains?" — methodology
   defense, especially for visitors comparing this against live-chain
   tools.
3. "What do I need to start?" — friction question, especially if the
   reader expects a card-on-file or brokerage-integration ask.
4. "Why only bull put and bear call?" — niche/scope question, a
   positioning move framed as "narrow on purpose" rather than "missing
   features."

The FAQ block addresses each in plain language. Sentence-case
questions (matches site voice), single paragraphs per answer (no
bullets, no caveat-stacking), em-dashes spaced like the rest of the
surface.

## How (routing)
Routed through Luke per `RULES.md` (subagent: `luke`).
- Brief: `workspace/luke_strikerewind_faq_brief.md`
- Output: `workspace/luke_strikerewind_faq_output.md`

AutoBox-Hermes corrected three claims against backend code before
applying:

1. **Q3 sign-up** — Luke wrote "An email." Reframed to "Email and a
   password" matching `frontend/src/utils/validation.ts:59`
   (`validatePassword`: 8+ chars, mixed case, digit). The friction
   answer has to be honest about the actual sign-up surface.
2. **Q2 lookback** — Luke wrote "across a year of price history."
   Widened to "across years of price history" so it doesn't conflict
   with the methodology block's "1, 2, 3, or 5 years" claim or the
   engine's `analysisYears` schema (`(1, 2, 3, 5)` `CHECK` constraint).
3. **Q4 scope** — Luke wrote "the two credit spread structures."
   Reframed to "the two basic credit spreads" so iron condors,
   calendars, and other multi-leg credit structures aren't implicitly
   excluded as non-existent. This keeps the positioning sharp without
   making a category-level overclaim.

Voice and structure preserved exactly — corrections are
factual-accuracy only, not voice changes.

## Final copy

### Section heading
Before you sign up

### Q&A pairs

**Is this trading advice?**
No. StrikeRewind is an education and information service. We are not
a registered investment adviser, we do not manage money, and we do
not tell you which spread to put on. Every trade decision is yours,
in your own brokerage account, on your own risk.

**Why historical data instead of a live options chain?**
Because the question StrikeRewind answers is backward-looking — which
bull put and bear call structures on this ticker have actually paid,
across years of price history. A live chain does not answer that.
Your broker handles execution and the real-time quote when you decide
to put the trade on. We handle the ranking.

**What do I need to start?**
Email and a password — that is the whole sign-up. No card on file, no
brokerage connection, no API key. The free tier runs immediately: top
5 Hunt results a day, two ticker lookups a day, one year of history.
You only need a brokerage account when you decide to actually place a
trade.

**Why only bull put and bear call?**
Those are the two basic credit spreads, and StrikeRewind is a credit
spread tool focused on ranking them. It is not a generalist options
screener. The scan covers the S&P 500 every night so you can see
which delta and DTE has paid on the names you trade — narrow on
purpose.

## Verification
- `cd frontend && npm run build` passes (1921 modules transformed; JS
  `350.56 → 352.86 kB / +2.30 kB`; CSS `23.30 kB` unchanged — every
  utility class used already existed on the page).
- No backend impact (frontend-only copy edit). Skipped backend tests
  by design.
- Public-copy hygiene per `RULES.md` rule 14/15: copy reviewed before
  commit — sentence-case questions, no internal labels, no SEO
  scaffolding, no AI-smell ("we believe", "leverage", "empower",
  "actionable insights"), no machine fingerprints, no process
  language. Em-dash usage matches the prior April 29 + April 30 + May
  1 landing-copy work on this page.
- Every claim factually accurate against the live engine and validation
  code: `validation.ts:59` (sign-up = email + password), Supabase
  migration `analysis_years CHECK (1, 2, 3, 5)` (lookback windows),
  `usageServiceDB.ts` `FREE` tier (top 5 Hunt / 2 ticker / 1 year),
  `newAnalysisEngine.ts` (bull put + bear call only).

## What this run deliberately did NOT do
- Deploy (still owner-gated by `APPROVED: DEPLOY ON VERCEL+RENDER
  STARTER, $7/MO`).
- Ship a pricing block (gated on `APPROVED: STRIKEREWIND TIER COPY +
  LIMITS PRE-DEPLOY` — pricing copy can't ship without the tier-copy
  fix landing first).
- Add a fifth FAQ question or a "still have questions?" closer (the
  closing CTA section right below this block is the final affordance
  — adding more between FAQ and CTA dilutes the conversion path).
- Add an accordion or any disclosure UI (flat list reads faster for
  someone scanning before signup; accordion adds friction for no
  benefit).
- Touch any other surface (`Account.tsx`, `usageServiceDB.ts`,
  `LandingPage.tsx` outside the FAQ insertion point).
