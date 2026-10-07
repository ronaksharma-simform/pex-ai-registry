---
name: manual-qa-executor
description: Execute interactive manual QA tests against a running application using browser preview tools
stage: qa
triggers:
  - manual qa
  - manual test
  - smoke test
  - test the ui
  - run manual tests
  - functional test
  - click test
  - interactive test
  - visual test
  - test the pages
prerequisites:
  - api-scaffolding
  - frontend-scaffolding
output_format: md
version: 0
---

# Manual QA Executor Skill

## Overview

Executes interactive manual QA tests by starting the dev server, navigating pages, clicking elements, filling forms, and verifying behavior through screenshots, console logs, and network monitoring. Auto-derives test scenarios from the codebase — no manual test writing required.

## Prerequisites

- Development scaffold must exist (code to test against).
- launch.json must have dev server configurations for client and/or server.
- If a test plan artifact exists, load it for scenario prioritization.

## Workflow

### Phase 1: Codebase Discovery

1. Read `client/src/App.tsx` or router configuration to extract all route definitions.
2. Scan `client/src/pages/**/*.tsx` for forms, buttons, links, and API calls.
3. Read `server/src/routes/*.ts` to find API endpoints.
4. Generate a prioritized list of test scenarios:
   - Every route → "page load" scenario (navigate, screenshot, check console).
   - Every form → "happy path submission" + "validation error" scenario.
   - Every navigation link → "click and verify destination" scenario.
   - Every API-dependent page → "network error handling" scenario.
   - Every page → "responsive check" (mobile viewport) scenario.

### Phase 2: Server Startup

5. Start the dev server using `preview_start`.
6. Verify readiness via `preview_logs`.

### Phase 3: Test Execution

7. For each scenario, execute steps using preview tools:
   - `preview_eval` to navigate to the route.
   - `preview_screenshot` to capture initial state.
   - `preview_snapshot` to verify page structure and text content.
   - `preview_console_logs(level: "error")` to check for JavaScript errors.
   - `preview_network(filter: "failed")` to check for failed HTTP requests.
   - `preview_fill` and `preview_click` for form interactions.
   - `preview_resize` for responsive layout checks.

### Phase 4: Failure Handling (Dev Loop)

8. Track consecutive failure count per scenario ID.
9. On failure (retryCount < 3):
   a. Diagnose root cause from console errors, network failures, DOM snapshot.
   b. Read the source file causing the issue.
   c. Apply the fix using code editing tools.
   d. Wait for HMR reload.
   e. Re-run this scenario only.
10. On failure (retryCount >= 3): mark as UNRESOLVABLE, move to next scenario.
11. After all scenarios: regression re-run of previously passing tests.

### Phase 5: Reporting

12. Produce a markdown test report with:
    - Summary table: scenario ID | title | status | screenshot reference.
    - All console errors and network failures encountered.
    - Fix recommendations for unresolved failures.
    - Overall pass/fail statistics.

## Quality Gates

- [ ] All discovered routes tested for basic page load
- [ ] No unhandled console errors on any page
- [ ] No failed network requests (4xx/5xx) during normal flows
- [ ] Forms submit without error on happy path
- [ ] Navigation flows complete successfully
- [ ] Responsive layout verified (mobile + desktop viewports)
- [ ] Test report artifact saved with screenshots

## Output Format

Save as `{ProjectName}_ManualQA_Report_v{Version}.md` in the outputs directory.
