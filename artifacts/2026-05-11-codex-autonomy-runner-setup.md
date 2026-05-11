# Codex autonomy runner setup

## Decision

Set Codex up as a drop-in autonomy operator without changing the live cron yet.

Claude currently owns the active cadence through `scripts/run_autonomy.sh`. Codex now has a sibling runner, `scripts/run_autonomy_codex.sh`, that uses the same lock file, writes the same run-log shape, rebuilds the same public journal, and posts through the same Discord update script.

## Why

Travis reframed the experiment on 2026-05-11:

- StrikeRewind is commercially weak without the real data subscription.
- Profit After Fees is passive and paid acquisition is killed.
- The experiment should continue by having Codex research and pursue a new active online business lane.
- The desired behavior is not another passive micro-utility; Codex should try to make, fulfill, validate, or sell something people may pay for.

## Files changed

- `prompts/codex_wakeup_prompt.md` — Codex-specific wakeup protocol and lane-selection policy.
- `scripts/run_autonomy_codex.sh` — non-interactive Codex runner using `codex exec`, `--search`, `--ask-for-approval never`, and `danger-full-access`.
- `scripts/build_run_journal.py` — recognizes `logs/run_codex_YYYY-MM-DD_HHMMSS` directories and displays them as `codex · ...` in the public journal.
- `scripts/build_run_journal.py` — Vercel deploy now passes `VERCEL_TOKEN` explicitly when the environment provides it; this fixes the stale local CLI auth path.
- `systemd/autonomy-codex.service` — one-shot systemd service for a Codex cycle.
- `systemd/autonomy.cron.example` — commented Codex takeover cron lines.
- `config/STATE.md` — current portfolio reframed around Codex lane search, with StrikeRewind paused as primary lane.
- `config/TODO.md` — active first Codex business-run task added.

## Notification path

Codex uses the existing reporting chain:

1. `logs/run_codex_.../output.txt`
2. `scripts/build_run_journal.py`
3. `journal/site/`
4. `scripts/post_discord_bot_update.py`
5. Public site: `https://autobox.theshepherdstack.com`
6. Discord clean control channel

No separate notification system is needed.

## Recommendation: Codex takeover first

Do not let Claude and Codex pursue separate businesses on the same full cadence yet. They would compete for the same small budget, state files, owner attention, and public narrative. The shared `.autonomy.lock` prevents simultaneous runs, but alternating unrelated strategies would still fragment the experiment.

Recommended next step:

`CODEX TAKEOVER: ENABLE CODEX RUNNER FOR 48 HOURS`

Replace the current cron command with `scripts/run_autonomy_codex.sh` for the same cadence. Let Codex run the first market-selection cycle, then several execution cycles. Claude can remain available manually or be re-enabled if Codex fails the reporting loop.

## Alternative

Run an A/B schedule only if the goal is model comparison rather than fastest business progress:

- Codex: daytime runs.
- Claude: overnight monitoring/smoke runs only.

This is lower risk operationally, but it weakens the new-business experiment because each agent wakes up to mixed context and different assumptions.

## Verification

- `python3 -m py_compile scripts/build_run_journal.py scripts/post_discord_bot_update.py`
- `bash -n scripts/run_autonomy_codex.sh scripts/run_autonomy.sh`
- `python3 scripts/build_run_journal.py --no-push --skip-cards`
- Public journal published after sourcing `.env` and deploying `journal/site` with the valid Vercel token.
- Live check: `https://autobox.theshepherdstack.com/data.json` now reports latest run `run_codex_2026-05-11_000000`.
- Live check: `https://autobox.theshepherdstack.com/runs/run_codex_2026-05-11_000000.html` returns HTTP 200.

All passed locally.
