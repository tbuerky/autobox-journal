# Write My Formula Google Ads Spend Triage

## Task

Account for Travis's 2026-06-01 clarification that the Write My Formula Google Ads broadening import was applied and accidentally spent about `$60`, then decide the next revenue-preserving paid-search move.

## Evidence

- Travis clarified in `config/HANDOFF.md` that the old broadening-import gate is resolved and the broad search terms accidentally spent about `$60`.
- The staged broadening import included broad-match versions of `fix my excel formula`, `excel formula not working`, `spreadsheet formula help`, `excel formula help`, `google sheets formula help`, and related terms.
- The staged negative list blocked some obvious drift themes, but it was small relative to the breadth of the broad-match expansion.
- `npm run analytics:summary -- --since=7d` returned `0` tracked sessions, `0` analytics events, `0` formula events, `0` checkout clicks, `0` paid-success page views, and `0` paid Stripe sessions. It found `20` recent Stripe checkout sessions, all unpaid/expired.
- Current public product QA is strong enough for sale/outreach, but paid search has not yet produced tracked revenue or product-use signal in the local funnel summary.

Live/current validation:

- Google Ads Help says broad match is designed to reach related queries beyond exact/phrase and works best with Smart Bidding. It also says search terms reports show actual queries that triggered ads, though low-activity terms may be omitted for privacy.
- Google Ads Help's broad-match recommendation guidance says additional budget may be suggested for broad match, and advertisers can explicitly keep budget unchanged instead of accepting higher budget.
- Current competitor evidence still supports the category: AI Excel/spreadsheet formula generators are live commercial products, so the issue is not category absence. The problem is uncontrolled query quality and lack of tracked paid funnel proof.

Sources:

- Google Ads Help, keyword matching options: `https://support.google.com/google-ads/answer/7478529`
- Google Ads Help, search terms report: `https://support.google.com/google-ads/answer/2472708`
- Google Ads Help, broad match with Smart Bidding: `https://support.google.com/google-ads/answer/10195720`
- ExcelFormula Pro current market check: `https://excelformula.pro/`

## Decision

Do not spend another dollar broadening Write My Formula paid search until the account search-term report and first-party funnel agree that clicks are buyer-intent formula-help traffic.

The highest-leverage next move is a permission-gated control action:

`APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

## Immediate Action After Approval

1. Pause the broad-match additions from the 2026-05-24 import or pause the broadened campaign/ad groups if that is the fastest safe control.
2. Export/search-review the Google Ads search terms for the accidental spend window, including query, match type, ad group, cost, clicks, conversions, and final URL where visible.
3. Classify each query as:
   - `keep`: formula repair/generation intent with plausible willingness to use the app.
   - `negative`: homework, tutorial, template, course, job, salary, certification, programming, or broad spreadsheet learning intent.
   - `landing-gap`: relevant query but missing a tightly matching page or ad group.
4. Keep or rebuild only exact/phrase terms that produced relevant searches or product events.
5. Do not raise budget, loosen bid caps, or add more broad match unless search terms show relevant clicks plus at least one real `formula_submit`, `checkout_click`, or paid Stripe session.

## Budget

Record the reported approximate spend now so the experiment budget reflects the damage:

- Prior balance: `$35.93`
- New reported approximate expense: `-$60.00`
- New current balance: `-$24.07`

This is approximate pending the exact Google Ads invoice/dashboard total.

## Gates

Open gates after this run:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or additional spend occurred in this run.
