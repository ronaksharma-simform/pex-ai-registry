---
name: manual-backend-qa-executor
description: Execute the existing backend test files for a given feature or domain inside the project container, then produce a test execution report
stage: qa
triggers:
  - manual backend qa
  - run backend tests
  - run the backend tests
  - execute backend tests
  - run existing tests
  - execute existing tests
  - existing backend tests
  - run the test suite
  - execute the test suite
  - run the backend test suite
  - run existing backend tests
  - execute the existing tests
prerequisites:
  - api-scaffolding
output_format: md
version: 0
---

# Manual Backend QA Executor Skill

## Goal

Run the backend tests that ALREADY EXIST in the codebase for a named feature/domain/module,
observe the REAL test-runner output, and produce a truthful Test Execution Report. The report
is the deliverable: an accurate record of what the runner actually did. This skill is a
measurement instrument, not a fixer.

## Scope

IN SCOPE: discover matching test files → install deps → EXECUTE the tests → report real
results per suite with verbatim runner output → diagnose failures and RECOMMEND fixes.

OUT OF SCOPE (read-only — a different agent's job): writing new tests; editing, fixing,
deleting, or "cleaning up" any file (tests, test helpers / mock factories, source, config);
committing/pushing/opening PRs; weakening or skipping an assertion to go green; testing
modules outside the requested scope. If a fix looks necessary, put it in Recommendations
and stop. The mutating git tools are not granted to this agent.

## Overview

Discovers, executes, and reports on the tests that are already there — it does not author
new tests or modify existing ones. Execution happens inside the project's Docker container
via the shell tools (a container is auto-provisioned if none is running).

## Prerequisites

- A backend scaffold / codebase exists with committed test files.
- A git workspace is provisioned (to discover and read test files).
- A container/shell is running (to install dependencies and execute the tests).

## Workflow

1. **Discover** — use `git_list_files` to locate backend test files (`*.test.ts`,
   `*.spec.ts`, `__tests__/`, `tests/`, `test_*.py`, `*_test.go`). Map the requested
   feature/domain to the matching files by path and name.
2. **Prepare** — run `shell_install_deps` if dependencies are not installed. If no
   container/shell is available, you CANNOT execute — do not analyze statically. Save a
   report whose Summary is "EXECUTION BLOCKED — tests were NOT run", list the files that
   would have run, and stop. Never project pass/fail results.
3. **Execute (mandatory)** — run the scoped tests with `shell_run_tests` (using `testFilter`
   for the feature) or a precise `execute` command. Capture the full pass/fail/skip
   output and error excerpts. A compile error or "0 tests ran" is a real result — report it.
4. **Report (truthfully)** — save a Markdown Test Execution Report with `save_markdown`
   (`unique=true` so each run is its own file). Paste the runner's VERBATIM summary line(s);
   every count in the report MUST equal that text. A suite that failed to compile /
   "Test suite failed to run" is a FAILURE (0 passed), never a pass. Include per-suite
   results, failures (verbatim errors + root-cause hypothesis), coverage if available, and
   recommended fixes (do not apply them).

## Quality Gates

- [ ] Test files were discovered from the actual repo (not assumed)
- [ ] The scope (feature/domain) is clearly stated and matched to real files
- [ ] Tests were actually EXECUTED (shell tools) — no static/"expected" projection
- [ ] The report embeds the verbatim runner summary, and every count matches it
- [ ] A suite that failed to compile / did not run is reported as a FAILURE (0 passed)
- [ ] Failing tests are reported with verbatim error output and a root-cause hypothesis
- [ ] NOTHING was modified, fixed, or committed — report is the only output
- [ ] Report artifact saved as Markdown (or marked EXECUTION BLOCKED if it could not run)

## Anti-Rationalization Defense

| Rationalization                                                                           | Why It Is Wrong                                                                                                  | Required Behavior                                                                      |
| ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| "I'll just summarize what the tests probably do"                                          | The report must reflect real execution, not guesses.                                                             | Actually run the tests and report the runner output.                                   |
| "No shell available, I'll project what the runner would output (EXPECTED PASS/FAIL)"      | A static projection is not a test result and is often wrong (e.g. misses compile errors).                        | Report "EXECUTION BLOCKED — tests were NOT run" and stop. Never emit projected counts. |
| "This test is failing, I'll tweak the assertion"                                          | A failing test is a signal, not an obstacle.                                                                     | Report the failure and diagnose it; never edit the test to pass.                       |
| "The suite failed to compile, but the tests look correct, so I'll report them as passing" | If it didn't compile, 0 tests ran. Reporting a pass is fabrication (the exact bug that shipped a false 131/131). | Report the compile error verbatim as a blocking FAILURE with 0 passed.                 |
| "I'll just fix the mock/helper so it passes, then report green"                           | Fixing is out of scope and hides the real state from the human.                                                  | Report the failure + a recommended fix; apply nothing.                                 |
| "The report should match my earlier prediction of 130 passing"                            | The runner's printed totals are the only source of truth.                                                        | Take every count from the verbatim runner output; discard predictions.                 |
| "No matching tests, I'll write some"                                                      | This skill executes existing tests only.                                                                         | State that no tests exist for the scope and list what does exist.                      |

## Output Format

Save as `{ProjectName}_ManualBackendQA_{scope}_Report.md` via `save_markdown` (with
`unique=true`) in the qa stage. `unique=true` guarantees each run gets its own file
(auto-suffixed on collision) instead of overwriting the previous report.
