---
name: tdd-enforcer
description: Enforce strict RED-GREEN-REFACTOR TDD discipline for all code generation
stage: development
triggers:
  - tdd
  - test driven
  - test first
  - red green refactor
prerequisites: []
output_format: code
version: 0
---

# TDD Enforcer Skill

## Overview

Enforces strict Test-Driven Development discipline during code generation. NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST. This is not a suggestion — it is a hard requirement. The agent must follow the RED-GREEN-REFACTOR cycle for every piece of functionality.

## The TDD Cycle (MANDATORY)

### Phase 1: RED — Write a Failing Test

1. Write a test that describes the expected behavior
2. Run the test — it MUST fail
3. If the test passes without new production code, the test is wrong (it's testing something that already exists)
4. The failing test is your specification

### Phase 2: GREEN — Make the Test Pass

1. Write the MINIMUM code to make the failing test pass
2. No extra features, no premature optimization, no "while I'm here" additions
3. The goal is a passing test, not perfect code
4. Run ALL tests — the new test must pass AND no existing tests must break

### Phase 3: REFACTOR — Clean Up

1. Clean up the code while keeping all tests green
2. Remove duplication, improve naming, extract methods
3. Run tests after every refactoring step
4. If any test fails during refactoring, revert the last change

## The Nuclear Option

If production code already exists WITHOUT corresponding tests:

1. STOP writing new code
2. Write tests for the existing behavior first
3. Only then proceed to modify the code using RED-GREEN-REFACTOR

## Quality Gates

- [ ] Every test was written BEFORE its corresponding production code
- [ ] Every test was verified to FAIL before production code was written
- [ ] Every test was verified to PASS after production code was written
- [ ] No production code exists without a corresponding test
- [ ] All tests pass at every step
- [ ] Refactoring did not change behavior (tests remain green)

## Anti-Rationalization Defense

| Rationalization                                       | Why It Is Wrong                                                                           | Required Behavior               |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------- |
| "I'll write the test after"                           | Post-hoc tests verify implementation, not intent. They miss design flaws.                 | RED test FIRST. Always.         |
| "The code is too simple to need a test"               | Simple code that breaks has no safety net. Tests catch regressions.                       | Every function gets a test      |
| "I already tested it mentally"                        | Mental testing has an 80% miss rate on edge cases.                                        | Write an automated test         |
| "This is just configuration/boilerplate"              | Config errors are the #1 cause of deployment failures.                                    | Test config values and behavior |
| "The test would just be testing the framework"        | You're testing YOUR usage of the framework, not the framework itself.                     | Write the test                  |
| "Writing tests first is slower"                       | TDD is faster total because it catches bugs during development, not after.                | Follow the cycle                |
| "I'll test the integration, unit tests aren't needed" | Integration tests don't pinpoint failures. Unit tests give precise feedback.              | Write both levels               |
| "The test is too hard to write"                       | Hard-to-test code is a design smell. Simplify the design.                                 | Refactor for testability        |
| "RED-GREEN-REFACTOR is a ritual, the spirit matters"  | The ritual IS the spirit. Each step has a purpose. Skipping any step defeats the purpose. | Follow every step exactly       |

## Reference Files

- `references/tdd-workflow.md` — Step-by-step examples of the TDD cycle
