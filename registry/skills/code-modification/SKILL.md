---
name: code-modification
# model: determined dynamically by task complexity classifier
# Low complexity → claude-sonnet-5 (5x cheaper), High → claude-opus-4-8
description: Modify existing code with impact analysis, dead code detection, full-stack sync, and E2E validation
stage: development
triggers:
  - fix the
  - fix a
  - fix this
  - modify the
  - change the
  - update the code
  - update code
  - refactor
  - rewrite
  - rename the
  - remove the
  - delete the
  - move the
  - extract the
  - add a method
  - add a function
  - add an endpoint
  - add endpoint
  - remove copyright
  - remove message
  - bug in
  - broken
  - not working
prerequisites: []
output_format: code
version: 0
---

# Code Modification Skill

## Overview

Modifies existing code in a repository using a disciplined 5-phase workflow that ensures completeness, correctness, and full-stack consistency. Unlike the scaffolding skills which generate code from scratch, this skill analyzes the existing codebase first, identifies all affected files, checks for dead code, makes synchronized changes across backend and frontend, and validates the result.

## Prerequisites

- A git workspace must be available (configured via GitHub integration)
- The repository must contain existing code to modify

## Workflow

The agent follows 5 mandatory phases in strict order:

1. **Impact Analysis** — Map all files that depend on or reference the code being changed
2. **Dead Code Detection** — Verify the target code is in the active execution flow
3. **Make Changes (Full-Stack Sync)** — Modify ALL affected files, keeping backend and frontend in sync
4. **Self-Review** — Use git diff to verify completeness and consistency
5. **E2E Validation** — Generate test scenarios and update test files

## Quality Gates

- [ ] Impact map produced before any code changes
- [ ] Dead code identified and skipped (or explicitly cleaned up)
- [ ] All dependent files from impact map addressed
- [ ] Backend route changes reflected in frontend API client
- [ ] Type/interface changes propagated to all consumers
- [ ] git diff reviewed for completeness
- [ ] Import paths verified correct
- [ ] E2E test scenarios generated covering happy path + edge case
- [ ] Existing test files updated if present

## Output Format

The agent produces:

- Modified files written directly to the git workspace via `git_write_file`
- A summary markdown artifact saved via `save_markdown` containing:
  - Impact analysis results
  - Dead code report
  - List of all files modified with descriptions
  - Self-review results
  - E2E test scenarios
  - Commit SHA and PR URL (if pushed)

## Anti-Rationalization Defense

The agent MUST NOT skip any phase of the workflow. Below are common rationalizations and why they are wrong:

| Rationalization                                  | Why It Is Wrong                                                                                         | Required Behavior                                                                   |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| "The change is trivial, no test needed"          | Trivial changes cause 40% of production incidents. A one-line typo can break a system.                  | Write a test that covers the change before making it                                |
| "I'll add tests after the code works"            | Post-hoc tests verify implementation, not intent. They miss edge cases the code accidentally handles.   | RED test first, then GREEN implementation                                           |
| "I already verified mentally"                    | Mental verification misses edge cases 80% of the time. Confirmation bias makes you see what you expect. | Run actual verification commands (git_diff, tests)                                  |
| "The spirit of the rule matters, not the ritual" | The ritual IS the discipline. Skipping steps is how bugs ship.                                          | Follow every phase of the 5-phase workflow exactly                                  |
| "This is just a refactor, tests aren't needed"   | Refactors that break behavior are bugs, not refactors. Only tests prove behavior is preserved.          | Run existing tests before AND after the refactor                                    |
| "I'll clean this up in a follow-up"              | Follow-ups never happen. The next task will have its own priorities.                                    | Do it now or explicitly flag it as tech debt in the summary                         |
| "Only one file is affected"                      | Impact analysis exists precisely because developers underestimate blast radius.                         | Complete the full impact analysis phase before concluding only one file is affected |
| "The frontend doesn't need updating"             | Backend changes without frontend sync cause silent failures that are hard to debug.                     | Check the frontend API client and types for every backend change                    |

## Reference Files

- `references/modification-workflow.md` — Detailed phase-by-phase instructions
