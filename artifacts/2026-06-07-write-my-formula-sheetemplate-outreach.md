# Write My Formula Sheetemplate Outreach

## Summary

Sent exactly one no-attachment first-touch email to Sheetemplate at `support@sheetemplate.com` from delegated Workspace mailbox `Mara Ellis <mara@theshepherdstack.com>`.

Artifact files:
- `workspace/sheetpilot-workbench/outreach/sheetemplate-send-control.md`
- `workspace/sheetpilot-workbench/outreach/sheetemplate-first-email.eml`

Delegated Gmail id/thread: `19ea12b3a3d89419`

## Why This Task

The current owner gates remain paid-search spend control and a manual reCAPTCHA submit. The consulting/support-service outreach lane is still wait-locked until `2026-06-07 16:20 UTC`, but the marketplace/app-template wait from Indzara had cleared on `2026-06-06 06:20 UTC`.

The strongest non-gated revenue motion was therefore one researched first-touch to another spreadsheet-template seller whose customers plausibly hit one-formula repair problems after editing templates.

## Evidence

- Sheetemplate's live site says it offers spreadsheet/Google templates for small business owners and asks customers with file or technical issues to contact support.
- The live support route lists `support@sheetemplate.com`.
- The live Write My Formula homepage confirms `2 guest tries` and the `$9` / `500 runs per month in this browser` access wording used in the email.
- Delegated Gmail profile returned `mara@theshepherdstack.com`.
- Delegated Gmail search for Sheetemplate in the Mara mailbox over the last 365 days returned `resultSizeEstimate: 0`.

## Copy Guardrails

Luke reviewed the buyer-facing email and recommended a shorter, direct fit-check. Final copy corrected the pricing line to avoid a `$9/month` implication and used the live wording: `Founding access is $9 for 500 runs per month in this browser.`

The email avoided partnership, listing, link-exchange, endorsement, customer, affiliate, support-replacement, accuracy, speed, guarantee, Microsoft/Google affiliation, browser-local/no-data-leaves, human-review, same-day/PDF, instant, automatic-fix, payment-link, and attachment claims.

## Verification

- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated Gmail search returned no prior Sheetemplate thread.
- Delegated dry-run parsed expected sender, recipient, and subject.
- Local `.eml` checks verified expected sender, recipient, subject, live URL, live price wording, no Stripe payment link, no attachment wording, and explicit no-partnership framing.
- Delegated send returned id/thread `19ea12b3a3d89419`.
- Delegated readback verified sender, recipient, subject, body, and `SENT` label.
- `node --test tests/*.test.js` passed `143/143`.

## Boundaries

No ad settings, bids, budgets, checkout/payment infrastructure, DNS/account/legal/bank settings, reCAPTCHA form submissions, public posts, bulk sends, destructive production changes, or spend occurred.

Current cash balance remains `-$24.07`.
