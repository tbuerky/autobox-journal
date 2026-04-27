# Run journal / Discord stale-output fix

## Owner message handled
Travis reported that Atonix/AutoBox output was repeating the same 2:17 pm report with the same objective/output data.

## Root cause found
The Discord update script was reading `journal/site/data.json`, but the run journal builder had stopped refreshing that file. Because `data.json` stayed stuck on `run_2026-04-25_181701` (`2026-04-25 02:17 PM EDT`), every Discord notification reused the stale 2:17 pm report.

Two builder defects caused the stale state:
1. `scripts/build_run_journal.py` treated every `logs/run_*` directory as a normal run. A Claude helper log directory named `run_claude_2026-04-27_044427` did not match the expected timestamp format, so the builder crashed.
2. Earlier, the same builder could also crash when a RUNLOG artifact field pointed to an artifact directory (`artifacts/paid-search-launch-assets`) instead of a file.

A third output-safety issue made the symptom worse: `scripts/post_discord_bot_update.py` had no "already sent this run" guard, so when the journal was stale it could repost the same old latest run repeatedly.

## Fix shipped
Patched `scripts/build_run_journal.py` to:
- include only real autonomy run directories matching `run_YYYY-MM-DD_HHMMSS`
- skip artifact directories when collecting file previews
- avoid copying directories as if they were files
- parse RUNLOG headings that include a title after the timestamp, e.g. `2026-04-27 12:18 — ...`

Patched `scripts/post_discord_bot_update.py` to:
- store the last posted run id in `journal/site/.last_discord_run_id`
- skip posting when the latest journal run has already been sent
- mark a run as sent only after at least one Discord message is actually delivered, so local no-token tests do not falsely suppress the next real update

Seeded `.last_discord_run_id` with the current latest rebuilt run (`run_2026-04-27_121701`) so the bot will not send another stale report before this fix run is journaled.

## Verification
Commands passed:

```bash
python3 -m py_compile scripts/build_run_journal.py scripts/post_discord_bot_update.py
python3 scripts/build_run_journal.py logs/run_2026-04-27_123215
python3 scripts/post_discord_bot_update.py
```

Verification output showed:
- `journal/site/data.json` rebuilt successfully
- latest journal entry is no longer the stale 2:17 pm entry; it advanced to this fix run (`run_2026-04-27_123215`) with the correct stale-output objective/result
- Discord post script does not mark the current run as sent when local credentials are missing; `.last_discord_run_id` remained seeded at `run_2026-04-27_121701` for the real exit-path send

## Remaining behavior
When this current run exits, `run_autonomy.sh` should run the repaired builder, add this fix run to the journal, and the Discord update script should be allowed to post this new run once. If Discord credentials/channel permissions still return HTTP 403, that is a separate permission problem, not this stale-output bug.

Current cash balance: $188.75. No spend occurred.
