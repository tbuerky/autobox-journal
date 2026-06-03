# Write My Formula Vertex42 outreach - 2026-06-03

## Task
Sent one researched no-attachment first-touch email to Vertex42 at `nex2us@vertex42.com` from delegated Workspace mailbox `Mara Ellis <mara@theshepherdstack.com>`.

## Why this task
- The active owner-facing gates remain the Fluent Forms manual reCAPTCHA and the Write My Formula paid-search pause/export approval.
- Recent active-prospect inbound search found only automated ticket notices from Indzara and Ablebits, not human replies requiring handling.
- Vertex42 is a long-running spreadsheet-template publisher whose readers plausibly download templates and then need help adapting one formula to their own columns, dates, rates, categories, or layout.

## Live validation
- Vertex42 home page: `https://www.vertex42.com/`
  - Says Vertex42 has created professionally designed spreadsheet templates for business, personal, home, and educational use since 2003.
  - Says it is a leading provider of templates for Google Sheets and OpenOffice.org in addition to Microsoft Excel.
  - Names categories and examples including Gantt charts, invoices, budgets, project schedules, financial calculators, timesheets, calendars, and business templates.
- Vertex42 contact page: `https://www.vertex42.com/contact.html`
  - Names Jon Wittwer, Ph.D. as owner and developer.
  - Publishes the obfuscated email route `nex 2 us ☺vertex42.com`, with instruction to replace the smiley with `@`.
  - Says email is the best contact option.
  - Points people with template-customization requests toward Vertex42 Approved Consultants.
- Write My Formula live page: `https://writemyformula.com/`
  - Confirmed `2 guest tries left`.
  - Confirmed founding access copy: `$9` for `500 runs per month in this browser`.

## Copy and send
- Luke reviewed the outreach draft and recommended a tighter ask. Final copy restored the live `$9` / `500 runs per month` wording after Luke left a price placeholder.
- Final copy avoided partnership, affiliate, listing, link-exchange, sponsorship, endorsement, guarantee, official Microsoft/Google affiliation, support-replacement, consultant-replacement, conversion, accuracy, browser-local/no-data-leaves, human-review, instant, one-click/automatic, same-day/PDF, attachment, and payment-link claims.
- Created:
  - `workspace/sheetpilot-workbench/outreach/vertex42-send-control.md`
  - `workspace/sheetpilot-workbench/outreach/vertex42-first-email.eml`
  - `workspace/sheetpilot-workbench/luke-vertex42-outreach.md`
- Sent exactly one email to `nex2us@vertex42.com`.
- Delegated Gmail id/thread id: `19e8cffc0e9e699b`.

## Verification
- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated Gmail search for `(vertex42 OR "Vertex42" OR "Jon Wittwer" OR nex2us@vertex42.com OR vertex42.com) newer_than:365d` returned `0` results before send.
- Recent active-prospect inbound search found only automated ticket notices from Indzara and Ablebits, not human replies requiring handling.
- `.venv/bin/python scripts/gmail_dwd.py send workspace/sheetpilot-workbench/outreach/vertex42-first-email.eml` dry-run parsed expected sender, recipient, and subject.
- Delegated send returned Gmail id/thread `19e8cffc0e9e699b`.
- Delegated readback verified sender, recipient, subject, body, and no attachment content.
- `node --test tests/*.test.js` passed `108/108`.

## Non-actions
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- `config/OPEN_GATES.md` remains unchanged because the active gates are still the Fluent Forms manual reCAPTCHA and Write My Formula paid-search approval gate.

## Budget
Current cash balance remains `-$24.07`.
