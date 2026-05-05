# Public journal hero "Waiting on" block — rendering fix

**Date:** 2026-05-05
**Surface:** `https://autobox.theshepherdstack.com` (and `http://165.227.204.19/autobox/`)
**Bet:** AutoBox public journal — Travis's canonical truth-source for the autonomy experiment

## Problem

The hero "Waiting on" block on the public journal rendered the OPEN_GATES.md entries with literal markdown backticks intact. Live HTML before this run:

```html
<ul class="hero-gates">
  <li class="hero-gate">
    <span class="hero-gate-action">`TESTING COMPLETE:</span>
    <span class="hero-gate-label">STRIKEREWIND` — Travis does full round of testing; reply to unblock marketing/launch post and Polygon subscribe</span>
  </li>
  <li class="hero-gate">
    <span class="hero-gate-action">`LAUNCH POSTURE:</span>
    <span class="hero-gate-label">STRIKEREWIND PRE-LAUNCH DATA COPY`</span>
  </li>
</ul>
```

Two distinct rendering bugs:

1. **Literal backticks bleeding through.** OPEN_GATES.md uses backticks around each gate (`` `ACTION: LABEL` ``) so the file renders entries as code when viewed as raw markdown. The build script's `read_open_gates` parser at `scripts/build_run_journal.py:1038` did not strip them, so they landed in the rendered HTML's `<span>` text.

2. **Em-dash explanation polluting the label span.** The `TESTING COMPLETE` line carried a trailing ` — Travis does full round of testing; reply to unblock marketing/launch post and Polygon subscribe` explanation after the closing backtick. OPEN_GATES.md's own maintenance contract explicitly says:

   > DO NOT add explanatory text inline with gates — keep gates clean, one per line. Use HANDOFF.md for context on why a gate was raised or closed.

   The contract was violated; the explanation made it onto the public hero.

## Why this matters

The journal is the public face of the experiment. Travis links it from `theshepherdstack.com`. The hero's whole job is to show, at a glance, "what is AutoBox waiting on right now?" Rendering the entries with raw markdown formatting and append-only commentary makes the surface look unprofessional — like a draft someone forgot to clean up — on the highest-traffic page of the project.

This is a customer-facing-quality bug per the wakeup prompt and `RULES.md` rule 14/15 ("never ship internal-facing copy, experiment notes, SEO scaffolding labels, or process language on a public page"). Backticks are markdown scaffolding. The em-dash explanation is a note-to-self. Both belong on the inside; the public hero should show only the action and label.

## Fix

Two surgical changes:

### 1. Parser hardening — `scripts/build_run_journal.py:1067-1080`

Inserted a backtick-aware preprocessor in `read_open_gates`:

```python
body = line[2:].strip()
if not body:
    continue
# Strip markdown code-formatting backticks. Canonical format is
# `- `ACTION: LABEL`` — backticks make the entry render as code
# when OPEN_GATES.md is viewed as raw markdown but must not
# survive into the rendered HTML on the journal hero. Anything
# after the closing backtick is explanatory text that the file's
# own maintenance contract says belongs in HANDOFF.md; drop it.
m_tick = re.match(r"^`([^`]+)`", body)
if m_tick:
    body = m_tick.group(1).strip()
else:
    body = body.strip("`").strip()
if not body:
    continue
if ":" not in body:
    ...
```

The regex captures the content between the first pair of backticks and ignores everything after. The `else` branch handles future hand-edits that drop the backticks but might still have stray ones (defensive). Empty body after stripping is treated as a no-op gate (skipped).

This means:
- `` - `ACTION: LABEL` `` → `action="ACTION", label="LABEL"`
- `` - `ACTION: LABEL` — explanation `` → `action="ACTION", label="LABEL"` (explanation dropped)
- `` - `ADS STATUS:` `` → `action="ADS STATUS", label=""`
- `- ACTION: LABEL` (no backticks) → `action="ACTION", label="LABEL"`

### 2. State file cleanup — `config/OPEN_GATES.md`

Removed the trailing em-dash explanation from the `TESTING COMPLETE` gate line so the live state file matches its own maintenance contract:

```diff
-- `TESTING COMPLETE: STRIKEREWIND` — Travis does full round of testing; reply to unblock marketing/launch post and Polygon subscribe
+- `TESTING COMPLETE: STRIKEREWIND`
 - `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`
```

Both gates remain open and unchanged in identity — only the inline explanation was stripped.

## Verification

### Parser unit-test coverage

7 inline test cases run via inline `python3` invocation, all pass:

```
PASS [{'action': 'TESTING COMPLETE', 'label': 'STRIKEREWIND'}]
PASS [{'action': 'LAUNCH POSTURE', 'label': 'STRIKEREWIND PRE-LAUNCH DATA COPY'}]
PASS [{'action': 'TESTING COMPLETE', 'label': 'STRIKEREWIND'}]   # drops em-dash explanation
PASS [{'action': 'APPROVED', 'label': 'BUY EXAMPLE.COM, MAX $15'}]   # no-backtick form still works
PASS [{'action': 'ADS STATUS', 'label': ''}]   # backtick + empty label
PASS [{'action': 'ADS STATUS', 'label': ''}]   # no-backtick + empty label
PASS [{'action': 'SUBSCRIBE', 'label': 'POLYGON STARTER, $29/MO'}]
7/7 pass
```

### Live verification on both hero surfaces

`scripts/build_run_journal.py` re-ran end-to-end. Output:

```
[hero] day 16 · 2 open gates · 3 active bets
[curation] 65 beats · 69 maintenance (weight=0)
[journal] 134 runs · 19 with runlog · 115 synthesized from artifact
[git] pushed 5045b7f (auto: rebuild after run_claude_2026-05-05_061701)
[vercel] deploy ok · Aliased: https://autobox-journal.vercel.app [14s]
```

Live hero block on both `http://165.227.204.19/autobox/` and `https://autobox.theshepherdstack.com`:

```html
<ul class="hero-gates">
  <li class="hero-gate">
    <span class="hero-gate-action">TESTING COMPLETE:</span>
    <span class="hero-gate-label">STRIKEREWIND</span>
  </li>
  <li class="hero-gate">
    <span class="hero-gate-action">LAUNCH POSTURE:</span>
    <span class="hero-gate-label">STRIKEREWIND PRE-LAUNCH DATA COPY</span>
  </li>
</ul>
```

Clean. Both surfaces match. Both gates still rendered. Public face of AutoBox no longer carries raw markdown or notes-to-self.

## Deliberately NOT done

- **Did NOT route through Cove.** No design judgment required — the bug was a parser regression rendering markdown formatting as visible text. Mechanical cleanup, not layout work.
- **Did NOT route through Luke.** Same — the gate strings themselves are the source-of-truth labels Travis writes; Luke would not be re-writing them. The fix removed scaffolding artifacts, didn't author copy.
- **Did NOT change the OPEN_GATES.md format docs.** Backticks in the canonical format are intentional for raw-markdown human readability; the parser is the right place to strip them, not the file. The fix is "render-time normalization," not "format change."
- **Did NOT remove the second gate's backticks.** That gate was already format-clean (no em-dash explanation); only the literal-backtick rendering bug applied to it, and the parser now handles that. No edit needed.
- **Did NOT raise a new gate.** The fix is autonomous and complete — Travis has no decision to make. Both pre-existing gates unchanged.
- **Did NOT push the unpushed StrikeRewind commits** (`095c96b`, `a58a853` on `autobox/strikerewind-rename`). Marketing freeze + Travis testing window still in effect; pushing those mid-test would create false test failures.
- **Did NOT touch PAF, AdSense, AI Pricing Index, or StrikeRewind.** Out of scope; this is a journal-rendering fix.
- **Did NOT add `DO NOT EDIT — auto-rendered` warnings to the journal HTML.** The journal is auto-built on every run; that's a pre-existing convention. No new docs needed.

## State

- Two open gates unchanged: `TESTING COMPLETE: STRIKEREWIND`, `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`. Marketing freeze still in effect.
- No new gate raised.
- No spend. Cash balance: $162.45.
- Files changed (autobox project root, no git): `scripts/build_run_journal.py` (+10 lines net), `config/OPEN_GATES.md` (-1 word per gate-1 line).
- Files changed (journal output, auto-pushed): `journal/site/index.html` (rebuild artifact, commit `5045b7f` on the autobox-journal git repo, deployed to Vercel under `the-shepherd-stack`).
