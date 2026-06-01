# Write My Formula TrumpExcel Outreach

Run time: 2026-06-01 10:17-10:25 UTC

## Task

Send one tightly bounded Write My Formula first-touch email to a new training/resource prospect after the training/resource wait cleared.

## Gate Reconciliation

`config/OPEN_GATES.md` still contains:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No owner message, handoff note, budget entry, or state file showed either gate had cleared. `/home/autoproj/.codex/handoffs/latest.md` was older than the latest completed `logs/run_codex_*` directory, so it was not used as override context.

## Choice Rationale

At `2026-06-01 10:17 UTC`, the Write My Formula training/resource wait had cleared. Consulting/support-service remains wait-locked until `2026-06-01 16:20 UTC`, add-in-vendor remains wait-locked until `2026-06-02 22:20 UTC`, marketplace/app-template remains in the Someka link-exchange reply wait, the Google Ads import remains owner/account-gated, and Fluent Forms remains blocked by manual reCAPTCHA.

I considered MyExcelOnline first, but its cleanest public route is a contact form and the email on the course page is protected in rendered output. TrumpExcel was a cleaner one-recipient fit because the live About page exposes `sumitbansal@trumpexcel.com`.

## Live Evidence

- TrumpExcel About page: says millions of people use TrumpExcel and its YouTube channel to learn Excel, invites Excel queries/tutorial suggestions, lists `sumitbansal@trumpexcel.com`, and links `FREE Excel Training` with `12+ Hours of Basic/Advanced videos`.
- TrumpExcel homepage: lists `FREE EXCEL TRAINING`, `EXCEL BASIC TO ADVANCED TRAINING`, `12+ hours of online training`, and `26 Lessons`.
- Write My Formula homepage: live HTTP `200`; shows `2 guest tries left`, founding access at `$9`, and `500 runs per month in this browser`.
- Gmail search: no visible TrumpExcel or MyExcelOnline thread in the last 30 days before send.

## Output

Created:

- `workspace/sheetpilot-workbench/outreach/trumpexcel-send-control.md`
- `workspace/sheetpilot-workbench/outreach/trumpexcel-first-email.eml`
- `workspace/sheetpilot-workbench/luke-trumpexcel-outreach.md`

Sent exactly one no-attachment first-touch email:

- To: `sumitbansal@trumpexcel.com`
- Subject: `honest read on a small Excel formula tool?`
- Gmail id/thread: `19e82b34a5e9f830`
- Gmail labels: `SENT`

## Verification

- `.eml` parsed with expected recipient and subject.
- Attachment count: `0`.
- Gmail dry-run returned expected recipient/subject before send.
- Gmail send returned id/thread `19e82b34a5e9f830`.
- Follow-up Gmail Sent search returned the same id/thread.
- `npm test` passed `97/97`.

## Guardrails

The email did not request a post, link, affiliate setup, partnership, public endorsement, payment, or bulk action. It did not include attachments or payment links. It avoided claims around customer usage, conversion lift, official Microsoft/Google affiliation, browser-local/no-data-leaves behavior, human review, same-day/PDF delivery, instant results, one-click/automatic fixes, or replacing training.

## Next Wait

Do not contact another Write My Formula training/resource prospect before `2026-06-04 10:24 UTC` unless Learn Excel Now, Excel Campus, ProfessionalsExcel, or TrumpExcel replies first.

Consulting/support-service becomes eligible at `2026-06-01 16:20 UTC`. Add-in-vendor remains locked until `2026-06-02 22:20 UTC`.

## Budget

Spend: `$0`. Current cash balance remains `$35.93`.
