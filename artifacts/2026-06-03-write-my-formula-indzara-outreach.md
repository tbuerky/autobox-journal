# Write My Formula Indzara outreach - 2026-06-03

## Task
Sent one researched no-attachment first-touch email to Indzara at `support@indzara.com` from delegated Workspace mailbox `Mara Ellis <mara@theshepherdstack.com>`.

## Why this task
- The active owner-facing gates remain the Fluent Forms manual reCAPTCHA and the Write My Formula paid-search pause/export approval.
- Someka's marketplace/app-template link-exchange fulfillment is now complete, so a single new marketplace/app-template fit-check was a stronger revenue motion than another passive page or gate recheck.
- Indzara is a spreadsheet-template vendor whose users plausibly customize templates and hit one-formula adaptation problems that Write My Formula can help with.

## Live validation
- Indzara home page: `https://indzara.com/`
  - Shows Excel, Google Sheets, and Power BI templates across HR, small business, project management, stock market, data visualization, calendars, school, and personal finance.
  - Claims 150+ templates, 1.5 million+ downloads, and 13,000+ premium customers.
  - Shows support portal, tutorials, free templates, premium templates, and template support positioning.
- Indzara about page: `https://indzara.com/about/`
  - Identifies Dinesh Natarajan Mohan as owner.
  - Lists `support@indzara.com` for feedback.
- Indzara contact page: `https://indzara.com/contact-us/`
  - Points users to the support portal and asks for template-specific context on queries.
- Write My Formula live page: `https://writemyformula.com/`
  - Confirmed `2 guest tries left`.
  - Confirmed founding access copy: `$9` for `500 runs per month in this browser`.

## Copy and send
- Luke reviewed the outreach draft and tightened the ask into a concise fit-read email.
- Final copy avoided customer, partnership, affiliate, listing, link-exchange, sponsorship, support-SLA, endorsement, conversion, accuracy, guarantee, official Microsoft/Google affiliation, browser-local/no-data-leaves, human-review, same-day/PDF, instant, one-click/automatic fix, pay-before-answer, attachment, and payment-link claims.
- Created:
  - `workspace/sheetpilot-workbench/outreach/indzara-send-control.md`
  - `workspace/sheetpilot-workbench/outreach/indzara-first-email.eml`
  - `workspace/sheetpilot-workbench/luke-indzara-outreach.md`
- Sent exactly one email to `support@indzara.com`.
- Delegated Gmail id/thread id: `19e8c244b220a144`.

## Verification
- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated Gmail search for `(indzara OR support@indzara.com OR dinesh) newer_than:365d` returned `0` results before send.
- `.venv/bin/python scripts/gmail_dwd.py send workspace/sheetpilot-workbench/outreach/indzara-first-email.eml` dry-run parsed expected sender, recipient, and subject.
- Delegated send returned Gmail id/thread `19e8c244b220a144`.
- Delegated readback verified sender, recipient, subject, body, and no attachment content.
- `node --test tests/*.test.js` passed `108/108`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- `config/OPEN_GATES.md` remains unchanged because the active gates are still the Fluent Forms manual reCAPTCHA and Write My Formula paid-search approval gate.

## Budget
Current cash balance remains `-$24.07`.
