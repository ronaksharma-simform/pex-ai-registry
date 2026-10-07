---
name: test-script-generator
description: Generate executable test scripts for both backend (Jest + Supertest) and frontend (React Testing Library), plus API collections
stage: qa
triggers:
  - write tests
  - test scripts
  - test suite
  - jest tests
  - generate tests
  - unit tests
  - integration tests
  - frontend tests
  - component tests
  - react tests
  - write frontend tests
  - generate frontend tests
  - ui tests
  - backend tests
  - write backend tests
  - generate backend tests
  - controller tests
  - service tests
  - api tests
prerequisites: []
output_format: code
version: 0
---

# Test Script Generator Skill

## Overview

Generates executable test scripts for **both backend and frontend**: backend Jest + Supertest suites (TypeScript), frontend React Testing Library tests (TSX), and API test collections (HTTP format for VS Code REST Client).

## Prerequisites

- Read test plan artifacts if available for test case alignment.
- Read scaffold artifacts for accurate import paths and function signatures.

## Workflow

1. Generate backend Jest test scripts for controllers and services
2. Generate frontend React Testing Library tests for page components
3. Create API test collection in HTTP format for manual testing
4. Use the `generated/tests/` directory structure and `// FILE: generated/tests/unit/controllers/example.test.ts` comment pattern
5. Include setup/teardown, mocking, and assertion patterns
6. Save each test file as a real, runnable file preserving its extension:
   - If a git workspace is active, write files into the repo with `git_write_file`
   - Otherwise, save each file with `save_code` (`.ts`/`.tsx`/`.http`) — never wrap code in a markdown artifact

## Quality Gates

- [ ] Backend Jest test files for all major controllers and services
- [ ] Frontend RTL test files for every key page component (not just one)
- [ ] API collection (.http) with requests for all major endpoints
- [ ] Proper test structure (describe/it blocks) for both backend and frontend
- [ ] Meaningful assertions (not just snapshot tests) — verify behavior, state, and content
- [ ] Mock setup for external dependencies (API calls mocked in frontend, DB/services mocked in backend)
- [ ] Test coverage for happy path AND error/edge cases in both layers
- [ ] Test files stay isolated from the app: they live under `generated/` (or `test/`) and
      the production build must NOT compile them. If the build tsconfig does not already
      exclude `generated/` and the test globs (`*spec.ts`, `*.test.ts(x)`), the app build
      would pull test code + test-only devDeps into `dist/` — verify they are excluded.
- [ ] Generated code compiles under `strict` TypeScript — no implicit-any errors. In
      particular: a mock factory that references itself (e.g. `createPrismaMock()` calling
      itself inside a `$transaction` stub) MUST have an explicit return type annotation
      (`function createPrismaMock(): any {`), or TS7023/TS7024 will make the whole suite fail
      to run. Annotate destructured mock-callback params too (`({ data }: any) => ...`).

## Anti-Rationalization Defense

The agent MUST NOT weaken tests or skip test categories. Below are common rationalizations and why they are wrong:

| Rationalization                           | Why It Is Wrong                                                                                 | Required Behavior                                                     |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| "Mocking the database is good enough"     | Mock/prod divergence masks real bugs. Mocks pass while production fails.                        | Use realistic test data and test against actual behavior contracts    |
| "Snapshot tests are sufficient"           | Snapshots test structure, not behavior. They pass when behavior breaks silently.                | Write assertion-based tests that verify specific behaviors            |
| "100% coverage isn't necessary"           | Coverage gaps are where bugs hide. Untested code is unverified code.                            | Cover happy path, error cases, edge cases, and boundary conditions    |
| "This component is too simple to test"    | Simple components break when their dependencies change. Tests catch that.                       | Write at least a renders-without-crashing test and key behavior tests |
| "I'll test the integration, not the unit" | Integration tests are slow and don't pinpoint failures. Unit tests give fast, precise feedback. | Write both unit tests AND integration tests                           |
| "The test is flaky, I'll skip it"         | Flaky tests indicate real timing or state issues. Skipping hides the problem.                   | Fix the flakiness root cause, don't skip or disable the test          |
| "Modifying the assertion to make it pass" | Tests define expected behavior. If test and code conflict, the code is wrong.                   | Fix the implementation, NEVER weaken the assertion                    |

## Output Format

Save each test file as a real, runnable file with its native extension via `save_code`
(or `git_write_file` when a workspace is active), following the `generated/tests/` layout:

- Backend Jest suites → `.ts`
- Frontend React Testing Library suites → `.tsx`
- API test collection → `.http`
