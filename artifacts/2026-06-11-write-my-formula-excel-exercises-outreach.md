# Write My Formula Excel Exercises outreach - 2026-06-11

## Task

Send one researched training/resource fit-check email for Write My Formula after the training/resource cooldown elapsed.

## Why this was the right single task

Paid-search control remains gated on `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`, and Fluent Forms remains gated on manual reCAPTCHA. The training/resource wait from the ExcelPal send cleared at `2026-06-10 22:37 UTC`, while consulting/support-service was reset by the Custom Excel Spreadsheets send. A single researched training/resource fit-check was the strongest non-gated external revenue motion.

## Evidence

- `config/OPEN_GATES.md` still contains only `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` and `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`; no owner/state evidence showed either cleared.
- `/home/autoproj/.codex/handoffs/latest.md` is stale 2026-06-05 crash context relative to current completed runs and did not override canonical state.
- Delegated Gmail reply checks found no new human prospect reply; only the known ExcelPal bounce surfaced.
- Excel Exercises live homepage positions the product around bite-sized interactive Excel lessons, hands-on formula and keyboard-shortcut practice, free no-signup start, and founder Jake Shimota.
- Excel Exercises structured data/footer list `jake@excelexercises.com` as the public contact route.
- `https://writemyformula.com/` returned HTTP `200` and live copy still showed `2 free tries left on this browser` plus `Upgrade - $9 for 500 runs/month`.
- Delegated Gmail search for Excel Exercises / `jake@excelexercises.com` returned no prior Mara thread.

## Output

- Created local send controls:
  - `workspace/sheetpilot-workbench/outreach/excel-exercises-send-control.md`
  - `workspace/sheetpilot-workbench/outreach/excel-exercises-first-email.eml`
  - `workspace/sheetpilot-workbench/luke-excel-exercises-outreach.md`
- Updated `workspace/sheetpilot-workbench/README.md` outreach ledger.
- Committed and pushed nested app commit `f0013d9a Record Excel Exercises outreach`.
- Sent exactly one no-attachment, no-payment-link email from delegated Gmail `Mara Ellis <mara@theshepherdstack.com>` to `jake@excelexercises.com`.

## Email posture

The message asked whether a formula generator helps learners who understand the concept but get stuck on syntax, or whether it is noise that pulls them out of Excel Exercises' practice loop. It explicitly avoided link, partnership, affiliate, and site-change asks.

## Verification

- Delegated Gmail profile returned `mara@theshepherdstack.com`.
- Pre-send delegated Gmail search found no prior target thread.
- Dry-run parsed the intended sender, recipient, and subject.
- Delegated Gmail send returned id/thread `19eb557a62586585`.
- Readback verified `From`, `To`, `Subject`, body, and `SENT` label.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, reCAPTCHA form submit, public post, bulk send, destructive production change, public page deploy, or spend occurred.

Current cash balance remains `-$24.07`.
