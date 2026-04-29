# StrikeSight tier naming — pick + reasoning

## Owner question (2026-04-29 17:58 UTC, Discord)
> what tier naming did you pick and why?

## Pick
**Free / Pro / Ultra** at **$0 / $29 / $99**.

## Why this beats Free / Standard / Pro (currently in code)

**1. "Pro" lands harder than "Standard" for this audience.**
Buyer is a retail credit-spread trader, $25k–$250k account, 1–10 years experience. "Standard" reads soft — it's the name SaaS uses when there's a tier *below* Pro that the company doesn't want to call "Basic". For a serious trader handing over money on a tool that affects real positions, "Pro" is the upgrade word that signals confidence. "Standard" is the upgrade word that signals "fine".

**2. "Ultra" telegraphs an unambiguous top tier.**
The Ultra tier ships API access, team seats, 5yr history, IV rank/earnings filters, and a weekly curated spread report. That is qualitatively different from Pro — not just more of the same. "Ultra" makes the difference visible at the pricing block without needing a paragraph. "Premium" reads like $30/mo in this market; "Ultra" leaves no doubt it's the top.

**3. $29 / $99 makes the price gap real.**
$9.99 / $29.99 is a casual-user pricing model. $9.99 anchors the buyer to "what's a reasonable monthly app subscription" — that frame is wrong. The buyer is choosing whether to risk this tool against $25–$250k of capital. They are not comparing it to Spotify. $29 is the entry credibility floor; $99 is the obvious top. The 3.4× gap is wide enough that the tiers differentiate themselves without explaining.

**4. Free-tier promise on the landing page already aligns with $29 Pro, not $9.99 Standard.**
Luke's landing copy ships "top 5 Hunt results/day, 2 ticker lookups/day, 1 year of history, no card required." That's a credible loss leader against $29 Pro (you give up *most* of the product). Against $9.99 Standard, it reads as a near-equivalent free tier — kills conversion.

**5. Matches the locked product-defining session spec from 2026-04-28.**
The current Free/Standard/Pro shape predates the priority shift. Account.tsx has not been updated since the new spec was set. Free/Pro/Ultra is what got chosen when the product was deliberately scoped to a serious trader audience.

## What I considered and rejected

- **Free / Pro / Premium** — "Premium" is overused; in this market it usually means $30, not $99. Confuses pricing.
- **Free / Pro / Elite** — "Elite" reads marketing-y, especially in finance. Buyers who use spreadsheets to backtest don't trust "Elite".
- **Free / Trader / Pro** — Cute, but "Trader" doesn't signal where it sits vs Pro. Order is ambiguous.
- **Keep Free / Standard / Pro** — Cheaper to ship (the Stripe products already exist), but it sells a casual-user product to a serious-trader audience and undermines the landing page's positioning. Cost of being wrong here is conversion, which is the only thing that matters now.

## What's needed from Travis to ship

In Stripe Dashboard, either:
- **Option A (cheaper):** Rename current `Standard` ($9.99) → `Pro` and reprice to $29; rename current `Pro` ($29.99) → `Ultra` and reprice to $99. Existing price IDs are reused, env stays the same after I rename them.
- **Option B (cleaner):** Create new `Pro ($29)` and `Ultra ($99)` products. Reply with the new price IDs. I'll repoint env (`STRIPE_STANDARD_PRICE_ID` → `STRIPE_PRO_PRICE_ID`, `STRIPE_PRO_PRICE_ID` → `STRIPE_ULTRA_PRICE_ID`) and archive the old products.

Either way, then reply: `TIER MODEL: FREE/PRO/ULTRA APPROVED`.

## What AutoBox does autonomously after approval
1. Repoint env var names in `backend/.env.local`, `backend/.env.example`, and the `.env` consumer in `stripeService.ts`.
2. Update `Account.tsx` tier card array — names, prices, feature lists matching HANDOFF spec exactly (Pro: unlimited Hunt, all indices, 3yr Ticker Analysis, Watchlist 25 tickers, daily digest, basic alerts. Ultra: + 5yr, IV rank, earnings filters, API, weekly curated report, team seats).
3. Add a pricing block to `LandingPage.tsx` (3-card row, Cove tokens, no animation).
4. Build, fixture-test, push commit on `autobox/strikesight-scanner-mvp`.

Estimated time after approval: 1 autonomous run.

## Suggested post copy:
Pick: **Free / Pro / Ultra at $0 / $29 / $99.**

Why:
• "Pro" lands harder than "Standard" for a credit-spread trader audience. Standard is the upgrade word that signals "fine"; Pro signals confidence.
• "Ultra" telegraphs the obvious top tier without explanation. Premium reads like $30 in this market; Ultra leaves no doubt.
• $29 / $99 makes the gap real. $9.99 anchors the buyer to "monthly app subscription" — wrong frame. They're risking $25–250k of capital, not comparing this to Spotify.
• Free-tier on the landing page (top 5 Hunt/day, 2 lookups/day, 1yr) reads as a credible loss leader against $29 Pro. Against $9.99 Standard it kills conversion.
• Matches the locked product-defining spec from Apr 28; current code predates the priority shift.

To ship, in Stripe Dashboard rename `Standard ($9.99)` → `Pro` at $29 and `Pro ($29.99)` → `Ultra` at $99 (reuses existing price IDs), then reply `TIER MODEL: FREE/PRO/ULTRA APPROVED`. I'll repoint env, update Account.tsx + landing pricing block, and ship in one run.
