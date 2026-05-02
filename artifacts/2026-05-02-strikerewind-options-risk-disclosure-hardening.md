# StrikeRewind — pre-deploy options-risk disclosure hardening

**Date:** 2026-05-02
**Branch:** `autobox/strikerewind-rename`
**Commit:** `711abe8`
**Files changed:** `frontend/src/pages/LandingPage.tsx` (+1/-1), `frontend/src/pages/Terms.tsx` (+3/-0)

## Why now
StrikeRewind is queued to deploy the moment `CARD ADDED: RENDER WORKSPACE`
clears. The landing page publishes specific Win%/EV% percentages
(82.4% / 79.6% / 76.1% / +3.1% / +2.4% / +2.0% in the example output
panel) computed from a backtest engine that does not model:

- broker commissions
- bid-ask spread
- slippage
- taxes
- forward-looking regime change

For weekly options on retail accounts, bid-ask spread alone can
routinely consume 5–10% of premium. A modeled `+2.0% EV` setup can be
inverted in real-world execution. A user who trades what Hunt surfaces
and loses money has a legitimate "I relied on your number" complaint
unless the page acknowledges this gap.

A `grep` of the entire `frontend/src` tree before this run returned
zero matches for `options.*risk|substantial risk|slippage|bid-ask|
commissions|hypothetical|Standardized Options`. Nowhere did the site
acknowledge any of it. That is the disclosure gap closed by this run.

## What changed

### Landing page methodology disclaimer
`LandingPage.tsx:161-163`. One paragraph, customer-facing tone.

Before:
> Backtest of historical price data, not a forecast. Past results do
> not guarantee future spreads behave the same way.

After:
> Backtest of historical price data, not a forecast. Past results do
> not guarantee future spreads behave the same way. EV% is gross of
> broker commissions, bid-ask spread, slippage, and taxes — your
> real-world outcomes will differ from the modeled ones. Options
> trading involves substantial risk of loss and is not suitable for
> every investor.

Two new sentences appended to the existing disclaimer. Same place on
the page, same className, same tone. Buyer reading the methodology
block now has the information they need to interpret the published
EV% honestly.

### Terms section 3 (Disclaimer of investment advice)
`Terms.tsx:57-59`. New paragraph appended to the existing two-paragraph
section. Adds:

> Options trading involves substantial risk of loss and is not suitable
> for every investor. Before trading options, you should review the
> Options Clearing Corporation's "Characteristics and Risks of
> Standardized Options" disclosure document, which your broker is
> required to provide. Win rate and expected value figures published by
> the service are derived from a historical backtest and have inherent
> limitations: they do not include broker commissions, bid-ask spread,
> slippage, taxes, or other transaction costs, and they cannot account
> for events that have not yet occurred. Actual trading results will
> differ from modeled results.

Document referenced by name without URL — brokers are required by SEC
Rule 9b-1 to provide it as part of options-account approval, and a
hardcoded URL would risk silent link rot.

## What I deliberately did NOT do
- **Did NOT route through Luke.** Same page just took two Luke passes
  on 2026-05-01 (FAQ block commit `ec20bef`, methodology block commit
  `8410703`). Adding regulatory boilerplate is correctness work, not
  voice work — same-week third Luke pass would burn quota for negligible
  gain.
- **Did NOT add a legal-disclaimer banner or modal.** Inline disclosure
  in the methodology block + Terms is the right surface. A modal would
  read defensively and degrade the conversion path on the highest-
  intent visitor (someone reading the methodology has already chosen
  to engage seriously).
- **Did NOT hardcode the OCC URL.** Document name is the canonical
  reference; URLs to OCC documents have churned across redesigns over
  the past few years. Naming the document by its full title is sufficient
  for any user to locate it.
- **Did NOT touch Footer.tsx.** It still uses legacy `bg-[#0a0a0a]` /
  `border-[#1a1a1a]` / `text-neutral-*` tokens (the rest of the customer-
  facing surfaces moved to Cove tokens in commit `9fec19b`). Real
  inconsistency, but small visual one — flag for next adjacent run, not
  this one.
- **Did NOT add an "I understand the risks" checkbox to sign-up.**
  Friction on the activation path. Disclosure on the landing surface +
  Terms acceptance at sign-up is the standard pattern.

## Verification
- `npm run build` (frontend): pass — 1921 modules, JS `352.86 → 353.69
  kB / +0.83 kB`, CSS `23.30 kB` unchanged
- `npx tsx --test` (backend): `12/12` pass (3 huntFixtureMode +
  9 spreadResultsService)
- Public-copy hygiene per `RULES.md` rule 14/15: re-read both edited
  blocks. No AI-smell phrases (`leverage|empower|comprehensive|robust|
  dive into|unlock|elevate|best-in-class|seamless|experiment|launch|
  v2|draft`), no internal labels, no SEO scaffolding, no notes-to-self,
  no stale dates. Reads as part of the product.

## Outcome
Commit `711abe8` pushed to `autobox/strikerewind-rename`. No deploy
fires this run — Render is still gated on `CARD ADDED: RENDER
WORKSPACE`. When deploy unblocks, both edits ship automatically with
the rest of the branch. No new owner-blocking gate raised.

## What this unblocks
On deploy day, the landing page no longer ships a credibility/legal
gap. Any user who reads the methodology block sees that EV% does not
include execution costs — preempting the "your tool said +3% but I
lost money on every trade" failure mode that would surface on day 1
of real traffic. Terms section 3 references the standard industry
options-risk disclosure document, which is the language plaintiff
attorneys, the SEC, FINRA, and arbitration panels all expect.

## Cash balance
`$162.45` (no change — no spend this run).

## Next adjacent autonomous-runnable options if Render gate stays open
- (a) Footer.tsx Cove-token alignment (legacy `bg-[#0a0a0a]` /
  `border-[#1a1a1a]` / `text-neutral-*`); inconsistent with the rest
  of the customer-facing surfaces
- (b) Bing Webmaster Tools verification packet — mirrors the GSC packet
  shipped earlier today; ~30% of US search traffic is non-Google for
  some demographics, and Bing feeds DuckDuckGo + Edge defaults
- (c) Pre-deploy end-to-end smoke-test plan (specific URLs to hit,
  specific assertions, specific failure modes) so the next autonomous
  run after deploy executes deterministically
- (d) PAF body-copy AI-smell sweep on the 5 calculator pages (last
  touched 2026-04-25)
