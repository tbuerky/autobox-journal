# 2026-04-26 Portfolio Operating Plan: PAF + AI Utility + StrikeSight

## Purpose
Keep AutoBox autonomous across three concurrent profit attempts without drifting into passive polishing.

## Portfolio order of operations
1. **Profit After Fees** = live cash/ads-monitoring asset.
   - Primary action: monitor Google Ads, AdSense, Ad Manager.
   - Stop-loss: Google Ads must be paused by $50 total spend.
   - Do not add more generic pages unless all higher-evidence moves are blocked.

2. **StrikeSight** = active build bet.
   - Core product is the scanner, not single-ticker lookup.
   - Preserve the market-scan value: scan S&P tickers over a selected period and return exact strikes/expirations that were historically profitable.
   - Work branch: `/home/autoproj/projects/StrikeSight`, branch `autobox/strikesight-scanner-mvp`.
   - First autonomous milestone: build/startup fixed, scanner path preserved, no Stripe/Sentry/data-provider secret required to run dev.
   - Revenue thesis: paid beta or weekly scanner report once real options data can make outputs credible.

3. **AI Feature Cost Calculator / Model Pricing Index** = distribution/content bet.
   - Strongest wedge: AI Feature Margin Roast / Graveyard, not generic directory sprawl.
   - Use when StrikeSight is blocked by owner/data-provider decisions or when a quick distribution post can be packaged.

## Scheduling rule
- If Google Ads/AdSense/Ad Manager evidence is available, handle PAF monitoring first.
- Otherwise spend the main build block on StrikeSight until the scanner MVP is demonstrable.
- Use AI calculator only for no-spend distribution/content loops or when StrikeSight hits an owner gate.

## StrikeSight near-term tasks
1. Fix TypeScript build and local startup.
2. Make Stripe lazy/optional so non-payment routes run.
3. Make Sentry optional/SDK-compatible.
4. Disable large background scheduler unless explicitly enabled.
5. Preserve scanner/Hunt as hero flow.
6. Tighten product copy around historical scanner + modeled assumptions.
7. Prepare domain/name check before public launch.
8. Evaluate MarketData.app vs Polygon for real options chains before paid launch.

## Owner gates
- No domain purchases without explicit approval.
- No paid data subscription without explicit approval.
- No public posting under Travis/account identity without approval.
- No real-money trading/autotrading.

## Public content direction
Faceless content should come from scans:
- Weekly StrikeSight scan: top opportunities.
- Trade roasts: looks good but is bad / looks bad but is good.
- Unknown ticker discoveries from the S&P scan.

## Current balance
$188.75 before any new spend or reported Google Ads spend.
