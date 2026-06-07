# Write My Formula ExcelPal Outreach

Run timestamp: 2026-06-07 22:22 UTC

## Task

Send one researched training/resource outreach email for Write My Formula after the training/resource wait window had cleared, without spending money, changing ads, submitting reCAPTCHA forms, or making public-site changes.

## Target

- Prospect: ExcelPal
- Intended contact: `hi@excelpal.com`
- Evidence used:
  - ExcelPal template pages showed Excel dashboard templates, course/articles/contact navigation, paid template products, and newsletter/free Excel tips language: `https://excelpal.com/templates/`
  - ExcelPal articles route exists as part of the same content surface: `https://excelpal.com/articles/`
  - Live category context remains strong: ExcelStep positions around hands-on Excel formula practice, 15 functions, and 45+ scenarios (`https://excelstep.com/`); Exceljet continues to operate a large Excel formulas/functions/training surface (`https://exceljet.net/`).
- Caveat: ExcelPal live evidence was mixed. Search results exposed the contact route and `hi@excelpal.com`, and ExcelPal template/articles pages still showed the expected ExcelPal surface, but the root/contact fetches were inconsistent. This was recorded so future runs do not overstate target quality.

## Buyer-facing copy review

Luke reviewed the first-touch posture. Final copy kept the low-pressure fit-check angle, removed colorful claims, and avoided partnership, affiliate, listing, link exchange, sponsorship, support replacement, endorsement, conversion, accuracy, guarantee, official Microsoft/Google affiliation, browser-local/no-data-leaves, human-review, same-day/PDF, instant, one-click/automatic-fix, and payment-link claims.

## Send result

- First connector send: Gmail connector returned id/thread `19ea42bb098debe2`, but readback showed sender `Travis Buerky <tbuerky@gmail.com>` instead of the intended delegated Mara sender. This was a sender-mismatch incident. Do not use the Gmail connector for future Mara outbound.
- Corrective send: delegated Gmail dry-run verified `Mara Ellis <mara@theshepherdstack.com>` to `hi@excelpal.com`, then sent one corrective no-attachment email from Mara.
- Corrective Gmail id/thread: `19ea42d0843676cb`
- Readback verified: sender, recipient, subject, body, `SENT` label, and no attachments.

## Files

- `workspace/sheetpilot-workbench/outreach/excelpal-first-email.eml`
- `workspace/sheetpilot-workbench/outreach/excelpal-corrected-sender-email.eml`
- `workspace/sheetpilot-workbench/outreach/excelpal-send-control.md`
- `workspace/sheetpilot-workbench/luke-excelpal-outreach.md`
- `workspace/sheetpilot-workbench/README.md`
- Nested app commit: `fa9fea4 Record ExcelPal outreach`

## Verification

- Gmail search before send found no existing ExcelPal / `hi@excelpal.com` thread in the available Gmail connector.
- Delegated Mara Gmail search found no existing ExcelPal thread.
- Delegated readback for `19ea42d0843676cb` matched the staged corrected email.
- `node --test tests/*.test.js` passed `147/147`.

## Gates and budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
