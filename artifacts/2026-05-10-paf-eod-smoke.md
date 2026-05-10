# PAF end-of-day production smoke — 2026-05-10

## Result
**36 pass / 0 fail / 0 console errors** against `https://profitafterfees.com` at 16:18 UTC.

## Cadence
- Last PAF EOD smoke: 2026-05-09 ~20:17 UTC. ~20h elapsed; ≥18h cadence cleared.
- Run 6 of 2026-05-10 covered StrikeRewind side at 14:19 UTC; this run is the complementary PAF cover per its next-run guidance.

## Coverage
- Apex calculator: HTTP 200, form present, listPrice input present.
- Conversion event: gtag fires exactly once on first input, send_to matches `AW-18121518600/WxyuCLjh56McEIjcgcFD`, stays at one call after additional input (Once semantic intact).
- Result math: net profit $40.84, revenue ex-VAT $75.00, Stripe fee $2.91, affiliate fee $22.50, verdict "You keep $40.84 from this sale."
- All 5 calculator pages 200 with scenario CTA links to apex.
- AI Model Pricing Index 200, all 6 model rows present, "Last verified May 6, 2026".
- AI Feature Cost Calculator 200.
- Mobile 390px: no horizontal overflow, calculator visible.
- /privacy/ 200; /ads.txt 200 with `pub-3560388500961643`.
- Zero unexpected console errors.

## Live state
- PAF Google Ads suspended pending appeal (gate `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`); AdSense + organic unaffected.
- No commit, no deploy, no spend, no new gate.

## Cash
$162.45 unchanged.
