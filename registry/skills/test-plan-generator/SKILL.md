---
name: test-plan-generator
description: Generate comprehensive test plans covering both backend and frontend, with coverage matrix, test cases, and QA strategy
stage: qa
triggers:
  - test plan
  - qa plan
  - testing strategy
  - test cases
  - test coverage
  - generate test plan
  - frontend test plan
  - backend test plan
  - e2e test plan
  - write test plan
  - qa strategy
prerequisites:
  - docx
output_format: docx
version: 0
---

# Test Plan Generator Skill

## Overview

Generates a comprehensive test plan covering both **backend** (API, services, controllers) and **frontend** (React components, pages, UI flows), with coverage matrix, test cases, and QA strategy across all 9 required sections.

## Prerequisites

- Read PRD and user stories for requirement-to-test-case traceability.
- If design artifacts exist, load them for architecture-aware test planning.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Define overall test strategy and approach — backend (Jest + Supertest) and frontend (React Testing Library + Vitest)
2. Create coverage matrix mapping user stories to test cases (both backend and frontend)
3. Design functional test cases for each feature area — include API endpoint tests AND React page/component tests
4. Identify edge cases and boundary conditions for both server-side logic and client-side UI
5. Define API test scenarios for all endpoints (method, payload, status codes, response shape)
6. Define frontend component/page test scenarios (render, interaction, state, error UI)
7. Specify non-functional tests (performance, security, accessibility, responsive layout)
8. Plan regression testing strategy
9. Document environment requirements and test data needs
10. Use TC-EPIC-NNN format for test case IDs
11. Include summary metrics with totals

## Quality Gates

- [ ] All 9 required sections present (strategy, coverage, functional, edge, API, frontend components, NFR, regression, environment)
- [ ] At least 10 test cases with TC-EPIC-NNN IDs
- [ ] Coverage matrix table mapping stories to test cases — includes both backend API and frontend UI test cases
- [ ] Summary metrics with test count totals
- [ ] Edge cases identified for each feature area (backend validation AND frontend UI edge cases)
- [ ] Non-functional requirements covered (performance, security, accessibility, responsive layout)
- [ ] Frontend component/page test cases present for every major page/component

## Anti-Rationalization Defense

The agent MUST NOT cut corners on test coverage. Below are common rationalizations and why they are wrong:

| Rationalization                                       | Why It Is Wrong                                                                                 | Required Behavior                                                             |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| "Happy path coverage is sufficient"                   | 60% of production bugs occur in edge cases and error paths, not happy paths                     | Include edge case and error path test cases for every feature                 |
| "This feature is too simple to test thoroughly"       | Simple features interact with complex systems. Integration points are where bugs hide.          | Map all integration points and test each one                                  |
| "We can add more tests later"                         | Test debt compounds faster than code debt. Later never comes.                                   | Write comprehensive test cases now                                            |
| "Performance testing isn't needed yet"                | Performance issues found in production are 10x more expensive to fix                            | Include non-functional test cases from the start                              |
| "Security testing is someone else's job"              | Security is everyone's job. OWASP top 10 vulnerabilities are preventable with basic test cases. | Include security test scenarios for input validation, auth, and data exposure |
| "The coverage matrix is overkill for this project"    | Without traceability, you cannot prove requirements are tested. Gaps become invisible.          | Complete the coverage matrix mapping every story to test cases                |
| "Manual testing will catch what automated tests miss" | Manual testing is inconsistent, non-repeatable, and doesn't scale                               | Design test cases that are automatable from the start                         |

## Output Format

Save as `{ProjectName}_Test_Plan_v{Version}.docx` in the outputs directory.
