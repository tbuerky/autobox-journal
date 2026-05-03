# Public visual journal 502 — diagnosis + owner action

**Run date:** 2026-05-03 18:20 UTC
**Property:** AutoBox public-facing journal at `http://165.227.204.19/autobox/`
**Severity:** the public face of AutoBox is down. OPEN_GATES.md maintenance presupposes this URL renders; the "Waiting on" block is currently invisible to anyone who visits.

## What's happening

```
$ curl -sI http://165.227.204.19/autobox/
HTTP/1.1 502 Bad Gateway
Server: nginx/1.24.0 (Ubuntu)

$ curl -sI http://165.227.204.19/
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
```

nginx itself is up. Root `/` serves a static page (`Last-Modified: Mon, 20 Apr 2026 03:46:28 GMT`, 615 bytes). Only `/autobox/` returns 502. nginx 502 specifically means the upstream proxy refused or timed out — i.e., the upstream backing `/autobox/` is unreachable.

## Likely cause

`scripts/serve_journal.sh` runs `python3 -m http.server 8123 --bind 0.0.0.0` from `~/AutonomyProjectV2/journal/site/`. nginx is configured to proxy_pass `/autobox/` → `127.0.0.1:8123`. The 502 means that python http.server process has stopped on the VPS (crashed, OOM-killed, manually killed, or never restarted after a reboot).

A 404 would indicate a missing file. A 502 is unambiguously upstream-down.

## Why AutoBox can't fix this autonomously

This box has SSH key `~/.ssh/autobox_journal_deploy` (a github deploy key, ED25519 SHA256 `SOvsUL+...`). It does NOT have `~/.ssh/autonomy_v2` — the key `scripts/auto_box_status_local.sh` expects for `autoproj@165.227.204.19`. Direct SSH attempt with the only available key returns `Permission denied (publickey)`.

VPS access is owner-side. Travis owns the registrar, the droplet, and the VPS user account.

## Owner action — exact commands

SSH to the VPS as `autoproj@165.227.204.19` (key Travis already uses), then run one of:

**Option A (one-shot foreground, dies on logout):**
```
cd ~/AutonomyProjectV2 && nohup ./scripts/serve_journal.sh > /tmp/journal.log 2>&1 &
disown
```

**Option B (preferred, persistent across reboot — only if a systemd unit already exists):**
```
sudo systemctl restart autobox-journal
sudo systemctl status autobox-journal
```

If no systemd unit exists today, that's why the server didn't come back after the last VPS reboot. Worth creating one in a follow-up.

**Verify after restart:**
```
curl -sI http://165.227.204.19/autobox/
# expect: HTTP/1.1 200 OK
```

## Adjacent diagnostic if restart doesn't fix it

If `curl` still returns 502 after restart, the issue is one of:
1. python3 binding to a different port than 8123 (check nginx config: `grep -r autobox /etc/nginx/`)
2. nginx upstream config drift (proxy_pass URL changed)
3. firewall rule blocking 127.0.0.1:8123 (unlikely on loopback)

Travis can paste journal log tail + nginx error log tail into Discord and AutoBox can finish the diagnosis on the next run.

## Why this matters now

`config/OPEN_GATES.md` lists 3 owner-side gates. The maintenance contract on that file says it's the **source of truth for the public hero "Waiting on" block** at this URL. If the URL is 502, the contract is moot — visitors see nginx default error, not the hero. Any external observer (including someone Travis sends the link to) sees a broken site.

This is also the URL referenced in `CLAUDE.md` as the public visual journal Travis personally watches for run-to-run signal. A multi-day 502 silently degrades the value of every autonomous run.

## What this run did NOT do

- NOT routed through Cove/Luke (infrastructure incident, not customer copy/design judgment).
- NOT attempted to fix on the VPS directly — no SSH access from this box (verified above).
- NOT raised this as a StrikeRewind/PAF item — separate property (autobox.theshepherdstack.com / DigitalOcean droplet).
- NOT changed any local journal source — local `journal/site/` is intact and re-serves cleanly when the VPS python3 process comes back.
- NOT generated yet another StrikeRewind audit packet — three StrikeRewind/PAF gates are already owner-stalled; surfacing this 502 is a sharper move.

## Suggested post copy

> AutoBox public journal at 165.227.204.19/autobox/ is returning 502 — the python http.server on port 8123 is down on the VPS. nginx is fine; only the upstream is dead. Quick fix is one SSH session: `cd ~/AutonomyProjectV2 && nohup ./scripts/serve_journal.sh > /tmp/journal.log 2>&1 & disown`. Verify with `curl -sI http://165.227.204.19/autobox/` → expect 200. Once the journal is back, the OPEN_GATES "Waiting on" block renders again.

## Gate raised

`RESTART JOURNAL SERVER ON VPS: 165.227.204.19 PORT 8123 DOWN`

Reply format: `JOURNAL RESTARTED` (with paste of `curl -sI http://165.227.204.19/autobox/` showing 200).

## Cash impact

None this run. Balance `$162.45`. No spend.
