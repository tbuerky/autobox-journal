# Codex takeover live

## Result

Codex is now the active autonomy operator.

Claude is paused for:

- scheduled autonomy cycles
- Discord `!run` triggered autonomy cycles
- bare Discord mention chat responses through AutoBox
- optional systemd autonomy service path

Existing standalone/interactive Claude shell processes were not killed because they may belong to manual sessions. The recurring and owner-triggered automation paths no longer call Claude.

## Active schedule

Current user crontab now runs:

```text
17 8,10,12,14,16,18,20 * * * /home/autoproj/AutonomyProjectV2/scripts/run_autonomy_codex.sh >> /home/autoproj/AutonomyProjectV2/logs/cron_launcher.log 2>&1
17 22,2,6 * * * /home/autoproj/AutonomyProjectV2/scripts/run_autonomy_codex.sh >> /home/autoproj/AutonomyProjectV2/logs/cron_launcher.log 2>&1
```

The StrikeRewind nightly batch remains unchanged:

```text
0 6 * * * /home/autoproj/AutonomyProjectV2/scripts/strikerewind_nightly_batch.sh
```

## Discord

`scripts/discord_bot.py` now uses Codex for:

- `@AutoBox !run` via `scripts/run_autonomy_codex.sh`
- bare `@AutoBox <message>` chat via `codex exec`

The existing AutoBox Discord bot identity remains in use. A separate Codex-branded bot is possible later, but it would require a new Discord application and token from Travis. Reusing AutoBox avoids that credential gate.

Discord send-path test passed:

- message id: `1503195544648945748`
- channel id: `1495641305294831646`
- message: `Codex test from AutoBox: Discord send path is live. Scheduled and !run autonomy now use Codex; Claude is paused for the autonomy loop.`

Travis replied with message `1503195834525683752`:

```text
<@&1495780859507376300> can you receive and reply to this?
```

Important finding: Discord exposed the visible `@AutoBox` mention as a role mention (`<@&1495780859507376300>`), not a direct bot-user mention. The bot was originally filtering for direct bot-user mentions only, so it did not log or answer that message.

Fix shipped:

- `scripts/discord_bot.py` now treats `AUTOBOX_ROLE_ID=1495780859507376300` as an AutoBox mention.
- `strip_bot_mention()` removes that role mention before sending the text to Codex.
- command prefixes now accept `@AutoBox !run` when `@AutoBox` resolves to the role mention.
- The bot service was restarted after the change.

Manual reply test passed:

- reply message id: `1503196448525779085`
- replied to: `1503195834525683752`
- content: `Received. That mention came through as the AutoBox role mention, not the bot-user mention. I updated the bot to accept that role mention too, so @AutoBox ... should now trigger Codex chat.`

The `discord-bot.service` user unit was restarted and is active.

## Context compaction

Codex PreCompact hooks are configured and enabled:

- `~/.codex/config.toml` has `[hooks] PreCompact = [{ command = "/home/autoproj/.codex/hooks/pre_compact_handoff.py", timeout_ms = 10000 }]`
- `~/.codex/hooks/hooks.json` has the same `PreCompact` hook registration.
- `codex features list` reports `hooks stable true`.
- `scripts/run_autonomy_codex.sh` now passes `--enable hooks` explicitly.

Manual headless-style test passed:

```text
printf '{"hook_event_name":"PreCompact","session_id":"autonomy-headless-test","cwd":"/home/autoproj/AutonomyProjectV2"}' | /home/autoproj/.codex/hooks/pre_compact_handoff.py
```

That wrote:

```text
/home/autoproj/.codex/handoffs/precompact-20260511-004339-autonomy-headless-test.md
```

and refreshed:

```text
/home/autoproj/.codex/handoffs/latest.md
```

`prompts/codex_wakeup_prompt.md` now instructs every autonomous run to read `~/.codex/handoffs/latest.md` when it is newer than the latest completed `logs/run_codex_*` run, so a compaction or crash snapshot can be recovered on the next wakeup.

## Files changed

- `scripts/discord_bot.py` — switched run trigger and chat handler from Claude to Codex.
- `scripts/discord_bot.py` — accepts the AutoBox role mention as a bot trigger because Discord renders Travis's visible `@AutoBox` mention as `<@&1495780859507376300>`.
- `systemd/autonomy.service` — now points to `run_autonomy_codex.sh`.
- `systemd/autonomy.cron.example` — Codex is the active example; Claude restore note added.
- `scripts/templates/index.html.j2` — public journal no longer describes the operator as specifically Claude.
- `prompts/codex_wakeup_prompt.md` — added `~/.codex/handoffs/latest.md` recovery step and compaction safety instructions.
- `scripts/run_autonomy_codex.sh` — explicitly enables hooks.
- `config/ACTIVE_BETS.md` — hero active-bets block now shows Codex takeover first and StrikeRewind paused pending real data.

## Verification

- `crontab -l` confirms both autonomy cadence lines call `run_autonomy_codex.sh`.
- `systemctl --user restart discord-bot.service` completed.
- `systemctl --user status discord-bot.service --no-pager` reports active/running.
- Discord POST returned success with message `1503195544648945748`.
- Discord history read confirmed Travis's reply message `1503195834525683752`.
- Manual Discord reply POST returned success with message `1503196448525779085`.
- Codex hook feature is enabled.
- Manual PreCompact hook test wrote `~/.codex/handoffs/latest.md`.
- `python3 -m py_compile scripts/build_run_journal.py scripts/post_discord_bot_update.py scripts/discord_bot.py`
- `bash -n scripts/run_autonomy_codex.sh scripts/run_autonomy.sh scripts/run_discord_bot.sh`
