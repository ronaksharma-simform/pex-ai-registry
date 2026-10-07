---
name: browser-test-executor
description: >-
  ATTENDED ONLY — requires a human with the PexAI Chrome extension installed and connected,
  and is unusable during autonomous Task execution. Reachable only through the operator-driven
  /api/browser-test surface. To make a Task's success depend on a page actually rendering, do
  NOT use this: declare a `browser` acceptance criterion instead (E8-4, #124), which drives
  headless Chromium with no extension and halts the Task on failure.
stage: qa
triggers: []
prerequisites:
  - development
output_format: md
version: 0
---

# Browser Test Executor

Automated browser testing agent that verifies implemented features in a real browser.

## ⚠️ Not for autonomous Task execution — read this first

This skill drives a **visible browser tab over a WebSocket bridge to the PexAI Chrome
extension**. It needs an attended session: a human, with that extension installed and
connected. There is no headless mode. Its `browser_navigate`/`browser_click` tools come from
`browserTestMcpServer`, which is wired only for the operator-driven `/api/browser-test` flow —
they are **not** in a Task-executing agent's toolset.

An agent that finds this skill while running a Task and tries to use it will discover the tools
missing and waste the run improvising (observed: ~200k tokens spent hand-installing Playwright
into a temp directory, then self-reporting a PASS that nothing verified). Hence `triggers: []`
— it is deliberately not routable from a natural-language request, and the intent classifier no
longer lists it.

**If you want a Task's success to depend on what a screen actually does, declare a `browser`
acceptance criterion** (`shared/types/acceptanceCriteria.ts`, E8-4 / #124): a page path plus an
optional selector. `core/checkRunner.ts` boots the app, drives real headless Chromium, attaches
a screenshot plus the page's own console errors as evidence, and halts the Task through the same
`verification_failed` path as every other failed check. That mechanism is the supported one and
needs no extension.

This skill is on #70's frozen list and is kept for the attended flow, which still works.

## What It Does

1. **Receives task context** — knows exactly what was built (task prompt, result summary, files changed, acceptance criteria)
2. **Navigates the app** — opens the running application in a visible browser tab via the Chrome extension
3. **Interacts with the UI** — clicks buttons, fills forms, follows navigation flows
4. **Verifies functionality** — checks that elements exist, text content matches, no console errors
5. **Captures screenshots** — takes visual proof at each test step
6. **Auto-fixes failures** — if a test fails due to a code issue, reads the source, fixes it, commits, and re-tests (up to 3 retries)
7. **Reports results** — saves a markdown test report with pass/fail counts, screenshots, and any fixes applied

## Prerequisites

- Chrome extension "PexAI Browser Tester" must be installed and connected
- A dev container must be running with the application deployed
- The task to test must be in "completed" status

## Tools Used

- `browser_navigate` — Navigate to URL
- `browser_click` — Click element by CSS selector
- `browser_type` — Type into input
- `browser_screenshot` — Capture visible tab
- `browser_get_text` — Read element text
- `browser_wait_for` — Wait for element to appear
- `browser_check_exists` — Assert element exists
- `browser_check_text` — Assert text content
- `browser_console_errors` — Get JS errors
- `browser_eval` — Execute JavaScript
- `git_read_file` / `git_write_file` / `git_commit` — For auto-fix workflow
- `save_markdown` — Save test report
