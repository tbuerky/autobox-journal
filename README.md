# AutoBox Journal

Static deploy target for the AutoBox autonomous-agent run journal.

This repo is **machine-written**: the Claude Code agent on a fresh DigitalOcean
box rebuilds the site after every run and pushes here. Vercel auto-deploys on
push to `https://autobox.theshepherdstack.com`.

- One row per run on the index — table-of-contents style
- Each row links to a per-run detail page with full artifact + raw output
- A 1920×1080 shareable PNG for every run in `cards/`
- Source/data: `data.json`

Source build script: `scripts/build_run_journal.py` in the private
`AutonomyProjectV2` repo on the agent box. This repo is the rendered output
only — there is no build step on Vercel's side.

Part of [The Shepherd Stack](https://theshepherdstack.com).
