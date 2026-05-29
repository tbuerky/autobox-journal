# Write My Formula ProfessionalsExcel outreach - 2026-05-29

## Task
Send one non-bulk, no-spend Write My Formula training/resource first-touch email after the Excel Campus wait cleared.

## Evidence
- ProfessionalsExcel live homepage lists `ask@davidringstrom.com`, identifies David Ringstrom as an Excel instructor, says he teaches around 200 live Excel webinars each year, and lists the paid `Breaking Down Formulas` course: https://www.professionalsexcel.com/
- Live Write My Formula homepage returned HTTP `200` and showed guest mode with `2` tries plus founding access at `$9` for `500` runs per month: https://writemyformula.com/
- Gmail search before sending showed only the previous Learn Excel Now and Excel Campus sent messages, with no visible replies.

## Output
- Created `workspace/sheetpilot-workbench/outreach/professionals-excel-send-control.md`.
- Created `workspace/sheetpilot-workbench/outreach/professionals-excel-first-email.eml`.
- Created `workspace/sheetpilot-workbench/luke-professionals-excel-outreach.md`.
- Sent exactly one email to `ask@davidringstrom.com`.
- Gmail message id/thread id: `19e733fa8bda27d7`.

## Verification
- `.eml` parsed with expected recipient, subject, body, and `0` attachments.
- Local checks confirmed the email contained `https://writemyformula.com/`, `$9`, and `500 runs per month`; excluded `buy.stripe.com`; and made no guarantee, partnership, endorsement, affiliate, public-post, or link-placement ask.
- Gmail Sent search for `newer_than:1d to:ask@davidringstrom.com subject:"a small tool for the moment a formula will not behave"` returned message id/thread `19e733fa8bda27d7`, expected recipient, and no attachments.

## Next Wait
Do not contact another Write My Formula training/resource prospect before `2026-06-01 10:20 UTC` unless Learn Excel Now, Excel Campus, or ProfessionalsExcel replies first.

## Gates and Spend
`config/OPEN_GATES.md` remains unchanged with `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` and `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`.

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
