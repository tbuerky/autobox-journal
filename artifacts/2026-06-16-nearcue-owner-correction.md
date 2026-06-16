# NearCue Owner Correction

Date: 2026-06-16

## What Travis Corrected

1. Do not use Travis's personal `tbuerky@gmail.com` Gmail address for cold outreach. Future cold outreach from that sender is forbidden. If no approved product/workspace sender is available, create a send-gate recommendation instead of sending.

2. NearCue has been misframed. It is not just note cards at the top of the screen or a one-line cue strip. It is supposed to be a camera-line teleprompter: paste a full manuscript, adjust size and speed, and read scrolling text in the narrow notch/camera area while keeping eye contact close to the lens.

## Product Definition

NearCue should behave like a teleprompter for Zoom, Google Meet, recordings, interviews, lessons, sermons, sales calls, and short videos:

- Paste a full manuscript, not only short talking points.
- Smoothly move text at a controlled speed.
- Let the user adjust text size and scrolling speed.
- Keep text in the half-inch/inch around the notch or camera.
- Avoid covering the meeting or recording workspace.
- Help the speaker read while maintaining eye contact with the camera.

A Google Doc near the top of the screen is not equivalent because it still requires manual scrolling, remains a normal document window, takes over the call/work area, and pulls attention away from the camera line.

## Evidence Checked

Local code review showed the current NearCue implementation is cue-line based:

- `workspace/notchprompter/site/app/app.js` parses the script into lines and renders `lines[current]`.
- `workspace/notchprompter/app-source/NearCue/PrompterModel.swift` exposes `currentLine`.
- `workspace/notchprompter/app-source/NearCue/PrompterStripView.swift` renders a single line in a pill-shaped strip.

That can be a prototype, but it is not the corrected product definition.

Live category check: NotchPrompter is positioned as a macOS teleprompter that sits in the notch/top screen area, is invisible to screen sharing/recording, and supports speed, size, font, position, and voice activation. That matches the reference category Travis named much more closely than a document or note-card strip.

## State Changes Made

- Added a hard sender rule to `config/RULES.md`.
- Added a hard NearCue product-definition rule to `config/RULES.md`.
- Added an urgent correction at the top of `config/HANDOFF.md`.
- Added the correction at the top of `config/STATE.md`.
- Added an active urgent TODO in `config/TODO.md`.
- Updated `workspace/notchprompter/README.md` to describe NearCue as a full-script camera-line teleprompter and flag the current implementation as incomplete.

## Next Action

Pause all NearCue outbound/reply sending unless Travis explicitly approves both the sender and the corrected positioning. Next product work should replace the cue-line behavior with a full-script smooth teleprompter experience or ingest Travis's existing working app.
