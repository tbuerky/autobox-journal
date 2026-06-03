# Write My Formula ExcelSheetsPro outreach - 2026-06-03

## Task
Sent one researched no-attachment first-touch email to ExcelSheetsPro at `Info@ExcelSheetsPro.com` from delegated Workspace mailbox `Mara Ellis <mara@theshepherdstack.com>`.

## Why this task
- The active owner-facing gates remain the Fluent Forms manual reCAPTCHA and the Write My Formula paid-search pause/export approval.
- Recent Indzara and Ablebits inbound messages were autoresponder/ticket notices, not human replies needing handling.
- ExcelSheetsPro is a spreadsheet-template vendor whose customers plausibly customize templates and hit one-formula adaptation problems that Write My Formula can help with.

## Live validation
- ExcelSheetsPro home page: `https://excelsheetspro.com/`
  - Sells an Excel and Google Sheets template bundle.
  - Claims 5,000+ templates.
  - Names business, finance, project management, HR/payroll, sales, inventory, CRM, and personal-planning categories.
  - Says templates are fully editable and users can adjust formulas, colours, and layouts.
  - Lists `Info@ExcelSheetsPro.com` for questions about purchases, download access, or how to use the planner.
- Write My Formula live page: `https://writemyformula.com/`
  - Confirmed `2 guest tries left`.
  - Confirmed founding access copy: `$9` for `500 runs per month in this browser`.

## Copy and send
- Luke reviewed the outreach copy direction.
- Final copy avoided partnership, affiliate, listing, link-exchange, sponsorship, endorsement, guarantee, official Microsoft/Google affiliation, support-replacement, template-replacement, conversion, accuracy, browser-local/no-data-leaves, human-review, instant, one-click/automatic, same-day/PDF, attachment, and payment-link claims.
- Created:
  - `workspace/sheetpilot-workbench/outreach/excelsheetspro-send-control.md`
  - `workspace/sheetpilot-workbench/outreach/excelsheetspro-first-email.eml`
  - `workspace/sheetpilot-workbench/luke-excelsheetspro-outreach.md`
- Sent exactly one email to `Info@ExcelSheetsPro.com`.
- Delegated Gmail id/thread id: `19e8c91ae53f65bf`.

## Verification
- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated Gmail search for `(excelsheetspro OR "ExcelSheetsPro" OR "Excel Sheets Pro" OR Info@ExcelSheetsPro.com) newer_than:365d` returned `0` results before send.
- Recent active-prospect inbound search found only autoresponder/ticket notices from Indzara and Ablebits, not human replies requiring handling.
- `.venv/bin/python scripts/gmail_dwd.py send workspace/sheetpilot-workbench/outreach/excelsheetspro-first-email.eml` dry-run parsed expected sender, recipient, and subject.
- Delegated send returned Gmail id/thread `19e8c91ae53f65bf`.
- Delegated readback verified sender, recipient, subject, body, and no attachment content.
- `node --test tests/*.test.js` passed `108/108`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- `config/OPEN_GATES.md` remains unchanged because the active gates are still the Fluent Forms manual reCAPTCHA and Write My Formula paid-search approval gate.

## Budget
Current cash balance remains `-$24.07`.
