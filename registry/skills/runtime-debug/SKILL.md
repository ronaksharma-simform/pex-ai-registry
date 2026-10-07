---
name: runtime-debug
description: Starts the project in its dev container, detects the tech stack, then reviews server/dev-server console logs and applies fixes for breaking changes — repeating build → run → read logs → fix until the app boots clean.
stage: development
triggers:
  - runtime debug
  - debug runtime
  - fix breaking changes
  - fix runtime errors
  - app won't start
  - fix startup errors
  - fix console errors
  - make it run
prerequisites: []
output_format: md
version: 0
---

# Runtime Debug Skill

## Overview

Runs the project inside its isolated dev container, reads the console logs it
produces, and fixes the breaking changes that stop it from booting — then does
it again, until the logs are clean. This is a runtime counterpart to
`systematic-debugging`: instead of debugging a single reported bug, it drives
the whole app to a running state.

The dev container is started for you via the container management service
(`provision` + `bootstrap`) before this skill runs, so dependencies are
installed and dev servers are (attempting to) start. Server and dev-server
output is captured to `/tmp/container.log` inside the container.

## The Cycle (repeat until clean)

1. **RUN** — Make sure the app is actually running. If the logs are empty or
   no dev server is listening, start it via shell:
   `nohup npm run dev > /tmp/container.log 2>&1 &` (adjust command per stack),
   wait a few seconds, then read the log.
2. **IDENTIFY STACK** — Read `package.json` (or `requirements.txt`, `go.mod`,
   `Cargo.toml`, …) with `git_read_file`/`execute` to learn the frameworks,
   scripts, and package manager. The project context also carries a `techStack`.
3. **OBSERVE** — Read the latest logs (`tail -n 500 /tmp/container.log`). A
   Vite/webpack dev server prints CLIENT build/compile errors here too
   (missing imports, TypeScript errors, failed HMR), so this covers both server
   and client breakage that prevents boot.
4. **FIX (root cause)** — For each breaking error: find the root cause, read the
   offending file with `git_read_file`, apply the minimal fix with
   `git_write_file`. Fix the shared cause once, not each symptom.
5. **VERIFY** — Re-run the relevant check (`shell_run_build` / `shell_run_tests`
   / restart the dev server) and re-read the log. Did the error clear? Did a new
   one surface?
6. **REPEAT** — Continue the cycle for every remaining breaking error.

## 3-Fix Escalation (borrowed from systematic-debugging)

Track attempts per distinct issue. After **3 failed fixes** for the same issue,
STOP fixing it, mark it as an unresolved / likely-architectural problem, and
report it with what was tried — do not loop forever on one error.

## Stop Conditions

- The app builds and the dev server starts with **no error-level log lines** → success.
- All remaining errors have hit the 3-fix escalation cap → report and stop.

## What Counts as a "Breaking Change"

Prioritise errors that stop the app from running:

- `Cannot find module` / unresolved imports / bad paths
- TypeScript / compile errors that fail the build
- `SyntaxError`, `ReferenceError`, `TypeError` thrown at startup
- Port/bind failures, missing env vars, failed DB/connection init
- Crashed dev server (`ELIFECYCLE`, non-zero exit, stack trace on boot)

Ignore non-breaking noise (deprecation warnings, lint style, info logs) unless
nothing else is failing.

## Committing Fixes

When a git workspace is active, commit each coherent fix with a conventional
commit message (`fix(<scope>): <description>`). Follow the mandatory git
workflow already described in the agent's tool instructions.

## Output

Save a Runtime Debug Report with `save_markdown`:

- Detected tech stack (frontend / backend / package manager / run commands)
- Timeline of errors found → fixes applied (file + one-line cause + fix)
- Verification evidence (build/test/restart output showing the error cleared)
- Final status: **RUNNING CLEAN** or list of **unresolved issues** (with the
  3-fix escalation notes)
