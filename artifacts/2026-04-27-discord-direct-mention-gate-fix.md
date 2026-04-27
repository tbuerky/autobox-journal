# Discord direct-mention gate fix

Date: 2026-04-27 14:20 UTC

## Owner input handled
Travis reported two follow-ups:
1. Whether AutoBox had actually been working or whether everything was bad.
2. AutoBox was triggering/responding to every message in the Discord thread and should only respond to direct mentions.

## Answer on the stale-report incident
AutoBox was doing real work. The bad part was the owner-visible reporting path: the journal data had stopped advancing, so Discord kept showing stale run data. The previous fix repaired `build_run_journal.py` and added Discord last-run dedupe.

## Fix shipped now
Changed `scripts/discord_bot.py` so ordinary thread messages are ignored unless they directly mention the bot.

Specific changes:
- Removed the automatic `AutoBox bot online...` channel message from `on_ready`, so restarts do not create unsolicited chatter.
- Changed `on_message` to return unless the message is in the configured target and directly mentions the bot.
- Removed bare `!command` handling in target/outside channels unless the message also directly mentions the bot.
- Added command prefixes that support direct-mention commands such as `@AutoBox !run` and `@AutoBox !status`.
- Updated help text to say ordinary thread messages and bare `!` commands are ignored.
- Restarted the systemd-managed Discord bot process; only one `discord_bot.py` process remains running.

## Verification
- `./.venv-discord/bin/python -m py_compile scripts/discord_bot.py` passed.
- Local function checks confirmed:
  - target thread messages are recognized,
  - ordinary messages without the bot mention are not direct mentions,
  - messages mentioning the bot ID are direct mentions,
  - messages mentioning another user are ignored,
  - direct-mention command prefixes include `@bot !` and `@bot ` forms.
- Process check after restart showed a single running Discord bot process under user systemd.

## Remaining note
Scheduled cron runs still happen independently on their normal cadence. This fix targets Discord message-trigger/response behavior, not the scheduled autonomous run loop.

## Spend
No spend. Current cash balance remains `$188.75`.
