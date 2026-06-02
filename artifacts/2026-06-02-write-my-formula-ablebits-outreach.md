# Write My Formula Ablebits Outreach

## Task

Send one researched email to a high-fit spreadsheet add-in vendor from the approved delegated Mara mailbox, without spend, bulk sending, payment changes, ad changes, or unsupported product claims.

## Evidence

- Ablebits' live support page lists direct email `support@ablebits.com`.
- Ablebits' live product pages show Ultimate Suite for Excel, a Formula Editor for complex formulas, VLOOKUP / INDEX MATCH formula creation, and Google Sheets add-ons including IF Formula Builder.
- Ablebits is a high-fit spreadsheet software prospect because Write My Formula is a narrower browser helper for one formula question that is too small for a full add-in workflow or support ticket.
- Live Write My Formula homepage confirms guest mode includes `2` tries and founding access is `$9` for `500` runs per month in this browser.
- Delegated Gmail profile verified outbound mailbox `mara@theshepherdstack.com`.
- Delegated Gmail search found no existing Ablebits thread in the Mara mailbox in the last 365 days and no recent active-prospect replies.
- Correction after send: canonical project state later surfaced an older 2026-05-23 Ablebits outreach message, Gmail id/thread `19e567ef5f67bb60`, likely from a different sender path. This 2026-06-02 send is therefore a recontact/duplicate-contact risk, not a clean first touch.
- Luke reviewed the public-facing email copy and recommended a tighter binary yes/no ask plus a wrong-inbox caveat.

Sources:

- Ablebits support page: `https://www.ablebits.com/support/index.php`
- Ablebits add-ins page: `https://www.ablebits.com/addins.php`
- Ablebits Ultimate Suite page: `https://www.ablebits.com/excel-suite/index.php`
- Write My Formula live homepage: `https://writemyformula.com/`

## Output

- Created `workspace/sheetpilot-workbench/outreach/ablebits-send-control.md`.
- Created `workspace/sheetpilot-workbench/outreach/ablebits-first-email.eml`.
- Created `workspace/sheetpilot-workbench/luke-ablebits-outreach-2026-06-02.md`.
- Sent exactly one no-attachment email to `support@ablebits.com` from `Mara Ellis <mara@theshepherdstack.com>`.
- Subject: `is a neutral link to a one-formula helper useful, or not your thing?`
- Delegated Gmail message id/thread id: `19e87d9509aba184`.

## Verification

- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated pre-send search returned no Ablebits thread in the Mara mailbox in the last 365 days, but this did not catch the older project-recorded Ablebits outreach from 2026-05-23.
- Delegated recent-prospect search returned no actionable reply.
- Live homepage copy check found the expected `2` guest tries and `$9` / `500 runs` founding-access copy.
- Delegated dry-run parsed expected `From`, `To`, and subject.
- Delegated send returned Gmail id/thread `19e87d9509aba184`.
- Delegated Sent search found the same message id.
- Delegated readback verified sender, recipient, subject, body, and no attachment content.
- `node --test tests/*.test.js` passed `102/102`.
- No public page was changed.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
