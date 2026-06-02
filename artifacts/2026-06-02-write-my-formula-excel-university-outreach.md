# Write My Formula Excel University Outreach

## Task

Send one researched first-touch email to a high-fit Excel training/resource prospect without using Travis's personal Gmail and without crossing a manual reCAPTCHA gate.

## Evidence

- Excel University's live contact page lists direct email `support@excelu.com`.
- The same contact page exposes a contact form, but live Firefox browser inspection showed a manual reCAPTCHA, so the form was not submitted.
- Excel University has public training paths for individuals, groups, CPAs, college professors, AI and automation, free resources, books, coaching, and Excel consulting.
- The live Write My Formula homepage confirms guest mode includes `2` tries and founding access is `$9` for `500` runs per month in this browser.
- Delegated Gmail profile verified the outbound mailbox as `mara@theshepherdstack.com`.
- Delegated Gmail search found no existing Excel University / ExcelU thread in the delegated mailbox in the last 365 days.
- Luke reviewed the public-facing message direction; the final copy used his compressed yes/no fit-check structure but corrected the sender to Mara and preserved the live `$9 for 500 runs per month` wording.

Sources:

- Excel University contact page: `https://www.excel-university.com/contact/`
- Write My Formula live homepage: `https://writemyformula.com/`
- MyExcelOnline contact page was evaluated and rejected because the live browser snapshot did not expose the expected contact form: `https://www.myexcelonline.com/contact/`
- Chandoo contact page was evaluated and rejected because it explicitly discourages partnership/advertising-style pitches: `https://chandoo.org/wp/contact/`

## Output

- Created `workspace/sheetpilot-workbench/outreach/excel-university-send-control.md`.
- Created `workspace/sheetpilot-workbench/outreach/excel-university-first-email.eml`.
- Sent exactly one no-attachment email to `support@excelu.com` from `Mara Ellis <mara@theshepherdstack.com>`.
- Subject: `quick fit read on a one-formula helper?`
- Delegated Gmail message id/thread id: `19e876d433106f01`.
- Local ledger commit: `035ee00 Record Excel University outreach`.

## Verification

- `.venv/bin/python scripts/gmail_dwd.py profile` returned `mara@theshepherdstack.com`.
- Delegated pre-send search returned no Excel University / ExcelU threads.
- Delegated dry-run parsed expected `From`, `To`, and subject.
- Delegated send returned Gmail id/thread `19e876d433106f01`.
- Delegated Sent search found the same message id.
- Delegated readback verified sender, recipient, subject, body, and no attachment content.
- No public page was changed.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
