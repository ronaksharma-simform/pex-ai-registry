---
name: dynamic-backend-qa-executor
description: Boot the API and exercise the endpoints for a feature/flow live via curl (happy path, validation, auth, edge cases), then produce an API test report
stage: qa
triggers:
  - dynamic backend qa
  - dynamic qa
  - dynamic api test
  - e2e api test
  - e2e backend test
  - api e2e test
  - test the api
  - test the endpoints
  - call the api
  - curl the api
  - hit the api
  - live api test
prerequisites:
  - api-scaffolding
output_format: md
version: 0
---

# Dynamic Backend QA Executor Skill

## Overview

Performs live end-to-end API testing for a given feature, flow, or domain. It reads
the source to map the relevant endpoints, boots the API server inside the project
container, exercises the endpoints dynamically with real HTTP requests (curl), and
produces an API Test Report from the observed responses. This is behavioral testing
against a running server — not static analysis and not unit testing.

## Prerequisites

- A backend scaffold / codebase exists with runnable API routes.
- A git workspace is provisioned (to read routes/controllers).
- A container/shell is running (to boot the server and issue curl requests).

## Workflow

1. **Map endpoints** — use `git_list_files` + `git_read_file` on routes/controllers to
   find the endpoints for the requested feature (method, path, auth, request/response
   shape, validation rules, listening port).
2. **Boot the API** — run `shell_install_deps`. If the start command runs compiled output
   (`node dist/...`, `node build/...`), run the project's build command first — never boot
   from a `dist/`/`build/` directory that could be stale from a previous run. Check for and
   kill any leftover server already listening on the target port before starting a new one.
   Then start the server in the background with `execute` (e.g.
   `nohup npm run dev > /tmp/server.log 2>&1 &`) and poll a readiness/health route until it
   responds. If it does not come up, DEBUG before giving up: read `/tmp/server.log`, apply
   the obvious prerequisite (install deps, run the DB migration/sync, free the port, fix
   env), and retry a few times. Only treat it as blocked after genuine debugging fails.
3. **Exercise live** — for each endpoint, issue real requests with `execute` + curl,
   capturing status code and body. Run the auth flow first when endpoints are protected
   and reuse the token. Cover happy path, validation (400), auth (401/403), not-found
   (404), and feature-relevant edge cases.
4. **Report & clean up** — save a Markdown API Test Report with `save_markdown` (pass
   `unique=true` so each run is its own file, never overwriting a prior report; real
   status codes + body excerpts, defects, recommendations; secrets redacted), then stop
   the background server.

## Quality Gates

- [ ] Endpoints were derived from the actual source (method/path/auth verified)
- [ ] The API was actually started and confirmed ready before testing (or a boot failure
      was debugged and, if unrecoverable, reported as a blocker)
- [ ] Every reported result comes from a real curl call (real status + body excerpt)
- [ ] Happy path AND negative/auth/edge cases were exercised
- [ ] Defects include the request, the actual response, and the expected result
- [ ] Secrets/tokens are redacted in the report
- [ ] A report artifact is ALWAYS saved as Markdown — a pass/failure report when the API was
      tested, or an "EXECUTION BLOCKED — API was NOT tested" report when it could not be. A
      run that ends with no saved report is a failed run.

## Anti-Rationalization Defense

| Rationalization                                           | Why It Is Wrong                                        | Required Behavior                                                                 |
| --------------------------------------------------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------- |
| "I'll infer the responses from the code"                  | Dynamic QA validates real runtime behavior.            | Actually call the running API and report what it returns.                         |
| "Happy path is enough"                                    | Most defects hide in validation, auth, and edge cases. | Exercise negative and boundary scenarios too.                                     |
| "The server won't start, I'll describe expected behavior" | An unstarted server means no dynamic evidence.         | Debug startup using the server log; if truly blocked, report the blocker plainly. |

## Output Format

Save as `{ProjectName}_DynamicBackendQA_{scope}_Report.md` via `save_markdown` (with
`unique=true`) in the qa stage. `unique=true` guarantees each run gets its own file
(auto-suffixed on collision) instead of overwriting the previous report.
