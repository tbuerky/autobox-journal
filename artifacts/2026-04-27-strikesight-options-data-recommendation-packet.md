# StrikeSight options-data provider recommendation — MarketData.app vs Polygon.io

Owner-facing approval packet. No spend has been made. This is a recommendation only.

## What StrikeSight needs before paid beta
StrikeSight today pulls historical OHLCV from `yahoo-finance2` and *simulates* credit spreads from that price history. For a paid beta the scanner has to quote spreads people can actually execute, so the missing input is **real options chain data**: per-expiration strikes with bid/ask/last, open interest, volume, implied volatility, and ideally Greeks. Yahoo is also rate-limiting the scanner under load, which is why a deterministic dev fixture was added on 2026-04-27.

Required capabilities:
- US equity options chains (OPRA), all listed strikes/expirations
- Bid, ask, last, IV, OI, volume; Greeks preferred
- Reasonable freshness for an end-of-day / next-day scanner (real-time tick is *not* required for the current product; 15-minute or end-of-day is acceptable for V1)
- Rate limits and pricing that survive a few hundred tickers per scan
- Terms that allow displaying derived analytics to paying users

## Two contenders

### MarketData.app
- Built specifically for retail/indie quant tools; options endpoints are the headline product (`/v1/options/chain`, `/v1/options/expirations`, `/v1/options/strikes`, `/v1/options/quotes`).
- Returns full chain in one call per expiration, with bid/ask/IV/OI/Greeks already computed.
- "Trader" tier is the typical small-tool plan. **Approximate price as last seen publicly: ~$60/month** for a healthy daily request budget. Verify on https://www.marketdata.app/pricing/ before purchase — pricing pages move.
- Documentation and SDKs are hobbyist-friendly; minimal contract overhead.
- Trade-off: smaller company, less institutional brand, occasional latency on snapshot calls during market open.

### Polygon.io
- Mature data infra; multiple options tiers.
  - Options Starter — delayed (~15 min) snapshots, end-of-day chains. **Approximate price ~$29/month.**
  - Options Developer — real-time, full chain access, streaming WebSocket. **Approximate price ~$79/month.**
  - Options Advanced — full unlimited. **~$199/month.**
- Verify on https://polygon.io/pricing before purchase.
- Strong historical depth (good for backtests later); WebSocket option useful if StrikeSight ever moves to intraday alerts.
- Trade-off: chains are returned as paginated lists of contracts, so building a usable per-expiration chain takes more API calls than MarketData.app's single-call chain endpoint. Slightly more integration time.

## Side-by-side

| Dimension | MarketData.app (Trader) | Polygon.io (Options Starter) | Polygon.io (Options Developer) |
|---|---|---|---|
| Approx monthly cost | ~$60 | ~$29 | ~$79 |
| Real-time vs delayed | Real-time / on-demand snapshots | 15-min delayed | Real-time |
| Full chain in one call | Yes (`/options/chain`) | No, contract-list + per-contract quote | No, contract-list + per-contract quote |
| Greeks included | Yes | Computed by you from IV | Computed by you from IV |
| Integration effort from current Yahoo-only code | Low (1 service, ~half a day) | Medium (multi-call orchestration + caching) | Medium |
| Historical options backtest data | Limited | Limited | Limited (Advanced needed for full history) |
| Risk if cancelled after 1 month | $60 sunk | $29 sunk | $79 sunk |
| Fits StrikeSight V1 product (end-of-day scan) | Strong | Strong if 15-min delay is acceptable | Overspec'd for V1 |

## Recommendation
**Subscribe to MarketData.app at the Trader tier (≈ $60/month) for one month**, integrate it behind a thin `optionsDataProvider` interface in `backend/src/services/`, and ship the first paid-beta scanner output that quotes real bid/ask/IV/OI per leg.

Why MarketData.app over Polygon for V1:
1. **Single-call chain endpoint** matches how the scanner already wants to consume data — enumerate expirations, pull a chain per expiration, simulate spreads against real strikes. Polygon's contract-by-contract model adds a day of orchestration and rate-limit care.
2. **Lower cancellation risk** than Polygon Developer ($79) and far better fit than Polygon Starter ($29), whose 15-min delay is fine for the scanner but whose multi-call shape makes integration slower than MarketData.app, eating the $30/mo savings.
3. **End-of-day scanner doesn't need WebSocket / real-time tick streaming**, which is Polygon's main structural advantage.

If StrikeSight later wants intraday alerts, real-time stream, or deep historical options backtesting, switch to Polygon. Don't pay for that today.

## Cost impact on experiment budget
- Current cash balance: **$188.75**
- Recommended spend: **~$60.00 / month** (verify exact price on the MarketData.app pricing page at purchase time; do not exceed **$65** without coming back for a fresh approval)
- Balance after first month: **~$128.75**
- This is the largest single recurring expense the experiment has taken on. Review after 30 days against beta signups / paid conversions; cancel if no signal.

## Approval line needed
Reply with exactly:

`APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, MAX $65/MO`

or, if you'd rather start cheaper at the cost of a slower integration:

`APPROVED: SUBSCRIBE POLYGON OPTIONS STARTER, MAX $35/MO`

or:

`DECLINED: KEEP STRIKESIGHT ON YAHOO-ONLY FOR NOW`

## What happens immediately after approval
On `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER ...`:
1. You purchase the subscription on https://www.marketdata.app/ and paste the API key into a place AutoBox can read it (e.g. `config/PRIVATE_CREDENTIALS.md` under a clearly-labeled `MARKETDATA_API_KEY=` entry). Do **not** paste it in Discord.
2. AutoBox adds `MARKETDATA_API_KEY` to `backend/.env.example`, builds a `marketDataOptionsProvider` service behind an `OptionsDataProvider` interface, wires it into `analysisEngine.ts` / `newAnalysisEngine.ts`, and keeps the Yahoo path for historical OHLCV.
3. AutoBox replaces the synthetic strike grid with real chain strikes from the next nearest expiration set, returns real bid/ask/IV/OI in the `/api/hunt` response, and ships a regression test that hits a recorded fixture to keep CI offline-safe.
4. AutoBox updates `BUDGET.md` with the actual charged amount and a 30-day review reminder.
5. AutoBox prepares one paid-beta-ready Hunt smoke run with a narrow ticker universe and reports back with at least 5 real-data spread suggestions before any owner-side beta outreach.

On `APPROVED: SUBSCRIBE POLYGON OPTIONS STARTER ...`: same steps, but the integration accepts a 15-minute snapshot delay and adds chain-pagination handling.

On `DECLINED ...`: AutoBox stops asking, deprioritizes StrikeSight paid-beta work, and rotates back to Profit After Fees / AI utility distribution and quality control.

## Verification before purchase (owner side)
Before you click subscribe, please confirm on the live pricing pages:
- MarketData.app Trader monthly price is still ≤ $65 and includes options chain access.
- Polygon Options Starter / Developer prices and real-time vs delayed terms still match the table above.
If either provider has changed materially, ping AutoBox and the comparison will be re-scored before you spend.

Current cash balance: $188.75. No spend has been made for this packet.
