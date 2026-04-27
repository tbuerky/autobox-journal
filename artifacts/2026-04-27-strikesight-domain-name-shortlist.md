# StrikeSight domain/name shortlist

Date: 2026-04-27 06:17 UTC

## Recommendation

Keep the product name: **StrikeSight**.

Buy, only with explicit approval: **getstrikesight.com**

Approval line:

`APPROVED: BUY GETSTRIKESIGHT.COM, MAX $15`

Why this is the best move:
- The repo, product language, and owner memory already use StrikeSight. Renaming now would create more work without improving the scanner.
- `strikesight.com` is already registered, so the cleanest low-friction domain that preserves the brand is `getstrikesight.com`.
- The product is still pre-paid-beta because real options-chain data is approval-gated, but a clean domain helps the first beta/demo link feel real once the data provider is wired.
- Estimated cost is about **$11.08** for a standard non-premium `.com` at Porkbun, based on the public price page checked during this run. Use a hard cap of **$15** to avoid accidental premium/upsell pricing.

## Availability checks performed

Verisign `.com` RDAP checks, 2026-04-27:

| Domain | Status | Notes |
|---|---:|---|
| strikesight.com | Taken | Best exact-match domain unavailable. |
| getstrikesight.com | Appears available | Recommended. Keeps the current brand and reads like a product URL. |
| usestrikesight.com | Appears available | Acceptable fallback, slightly more SaaS-template sounding. |
| tradestrikesight.com | Appears available | Overstates trade execution; avoid for now because the product is a scanner, not an autotrader. |
| strikesighthq.com | Appears available | Acceptable fallback, but less natural than `get...`. |
| scanstrikes.com | Appears available | Good descriptive fallback if Travis wants a more literal utility name. |
| weeklystrikes.com | Appears available | Useful for a content/newsletter angle, weaker for the scanner app. |
| optionsedgefinder.com | Appears available | Descriptive but long and generic. |
| profitableoptionscanner.com | Appears available | Too long/spammy; avoid. |
| optionshunt.com | Taken | Exact Hunt-language domain unavailable. |
| optionscanner.com | Taken | Generic exact-match unavailable. |
| optionhunt.com | Taken | Unavailable. |
| strikehunter.com | Taken | Unavailable. |
| strikehunt.com | Taken | Unavailable. |
| alphastrikes.com | Taken | Unavailable. |
| tradingscanner.com | Taken | Unavailable. |
| optionscout.com | Taken | Unavailable. |
| strikefinder.com | Taken | Unavailable. |
| strikescan.com | Taken | Unavailable. |

Non-`.com` checks for `strikesight.app`, `strikesight.io`, and `strikesight.co` were attempted, but the RDAP endpoints used from the sandbox failed DNS resolution. I am not recommending those today because `.com` is cheap, familiar, and enough for a private beta.

## Options considered

1. **Keep StrikeSight + getstrikesight.com** — best balance of continuity, trust, and low implementation cost.
2. **Rename to ScanStrikes + scanstrikes.com** — more literal, but throws away the existing StrikeSight repo/product name and feels narrower.
3. **Use weeklystrikes.com for a weekly scan/content loop** — useful later if the content motion becomes the main wedge, but weaker for the app itself.
4. **Wait and do nothing** — acceptable if Travis does not want another approval gate, but the domain decision will return before beta sharing.

## What happens after approval

If Travis replies `APPROVED: BUY GETSTRIKESIGHT.COM, MAX $15`:
1. Buy only `getstrikesight.com` if checkout price is `$15` or less.
2. Record the exact expense in `config/BUDGET.md`.
3. Point the domain at the deployment target only after the app is safe to expose.
4. Keep `StrikeSight` as the app name in public copy.
5. Do not imply real-money trading, guaranteed profitability, or broker execution.

## What not to do yet

- Do not buy any domain without explicit approval.
- Do not rebrand the repo/product away from StrikeSight unless Travis asks.
- Do not launch public beta copy until real options-chain data and credential cleanup are handled.
- Do not use language that suggests automated trading or guaranteed profitable signals.

## Current budget impact

No spend occurred in this run.

Current cash balance remains **$188.75**.

If approved and purchased at the observed Porkbun `.com` price of `$11.08`, projected balance would be **$177.67**.
