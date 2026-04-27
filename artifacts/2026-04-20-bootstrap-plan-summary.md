# Autonomy Project V2 — Bootstrap Summary

## Goal
Stand up a clean-room autonomous operator on a fresh DigitalOcean Ubuntu box so it can research, choose, build, launch, and attempt to monetize a very small online business with minimal owner context.

## Architecture we implemented
- Host: DigitalOcean droplet `165.227.204.19`
- User: `autoproj` for experiment work, not root
- Project pack: `/home/autoproj/AutonomyProjectV2`
- Hermes home: `/home/autoproj/.hermes-autonomy-v2`
- Model path: GPT-5.4 via OpenAI OAuth inside Hermes
- Run mode: one-task wakeup loop via `scripts/run_autonomy.sh`
- State files: `config/TODO.md`, `config/RUNLOG.md`, `config/HANDOFF.md`, `config/SCORECARD.md`
- Artifact folders: `artifacts/`, `workspace/`

## Guardrails
- No copied main `~/.hermes`
- No copied sessions, memories, or skills from Travis's main install
- No broad Travis-life context
- One task per run, then update state and exit
- Stop on permission gates

## What we completed during bring-up
1. Verified the droplet was reachable and the problem was SSH auth, not networking.
2. Fixed malformed `authorized_keys` entries so both `root` and `autoproj` could log in.
3. Synced the local starter pack to the droplet.
4. Installed Ubuntu base packages, ripgrep, ffmpeg, and Playwright Chromium.
5. Installed clean Hermes into `.hermes-autonomy-v2`.
6. Authenticated and ran the first autonomy loop.
7. Confirmed the first real research artifact landed under `artifacts/`.

## Immediate next phase
- Let the loop complete market-category survey work
- Generate 5 candidate business opportunities with evidence
- Score and pick 1
- Build the minimum validation asset
- Attempt first traffic or outreach motion

## Discord visibility plan
- Add `DISCORD_WEBHOOK_URL` to `/home/autoproj/AutonomyProjectV2/.env`
- After each run, post the latest RUNLOG section and next TODO to Discord
- Keep updates short enough to show visible progress without spam
