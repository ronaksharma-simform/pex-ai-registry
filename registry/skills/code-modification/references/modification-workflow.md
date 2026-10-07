# Code Modification Workflow — 5-Phase Process with TDD

This document defines the mandatory workflow for modifying existing code. Every code modification task MUST follow all 5 phases in order.

---

## Phase 1: Impact Analysis (MANDATORY FIRST STEP)

Before making ANY changes, perform a complete dependency analysis.

### Steps:

1. Use `git_list_files` with `recursive=true` to get the full file tree
2. Identify the primary file(s) that need modification based on the change request
3. Use `git_read_file` to read each primary file
4. For EACH function/type/export/route you plan to change, search for ALL references:
   - Scan `import` and `require` statements across the codebase
   - Search for function/method name usage in other files
   - For route paths (e.g., `/api/users`), find frontend code that calls them
   - For types/interfaces, find all files that reference them
   - For database model changes, find migrations, seeds, queries, and ORM schema
5. Build and output an **Impact Map**

### Output Format:

```
## Impact Analysis

### Primary Files (will be modified)
- path/to/file.ts — reason for modification

### Dependent Files (must be checked/updated)
- path/to/dependent.ts — imports functionX from primary file
- path/to/api-client.ts — calls /api/route that is being changed

### Risk Assessment
- [HIGH/MEDIUM/LOW] Description of risk and blast radius
```

**STOP: Do NOT proceed to Phase 2 until the impact analysis is complete.**

---

## Phase 2: Dead Code Detection

For each file in the impact map, verify the code is actively used.

### Steps:

1. Find entry points:
   - **Server**: main entry file (index.ts, app.ts, server.ts) → trace route registrations
   - **Frontend**: router config (routes.tsx, App.tsx) → trace which pages/components render
2. For each function/route/component you plan to modify:
   - Is it imported by a file that IS in the active flow?
   - Is the route registered in the app/router?
   - Is the component rendered in any active page?
3. Check for dynamic usage patterns that may look dead but aren't:
   - Dynamic imports (`import()`)
   - String-based route registration
   - Dependency injection
   - Event-driven invocations
   - Middleware chains
4. If code is genuinely dead (unreachable from any entry point):
   - Report it clearly
   - Do NOT modify it unless the change request specifically asks for cleanup

### Output Format:

```
## Dead Code Check

### Active Code (will modify)
- path/file.ts:functionName — called via: app.ts → routes/index.ts → this file

### Dead Code (skipping)
- path/old.ts:deprecatedHandler — not imported anywhere, no route points to it

### Dynamic Usage (verified active)
- path/middleware.ts:authCheck — loaded via middleware chain, not direct import
```

---

## Phase 3: Make Changes (Types-First + TDD Red-Green-Refactor + Full-Stack Sync)

Modify ALL affected files using a disciplined approach.

### Step 3a: Types First (Contract-Driven)

ALWAYS start by updating types/interfaces/schemas BEFORE touching implementation:

1. Update shared TypeScript types/interfaces first — these are the contract.
2. Update validation schemas (Zod, Joi) to match the new types.
3. Update database schema (Prisma, etc.) if data model changed.
4. The compiler will now flag every consumer that needs updating — use this as your guide.

### Step 3b: TDD Red-Green-Refactor Cycle

For EACH logical unit of change, follow this strict cycle:

**🔴 RED — Write a FAILING test FIRST:**

- Before writing ANY implementation, write ONE test that describes the expected behavior.
- Use `git_read_file` to check if test files already exist for the module you're changing.
- If tests exist, ADD a new test case to the existing file. If not, create a new test file.
- Write the test using `git_write_file`. The test MUST fail against current code.
- Focus on testing observable behavior through public APIs, not internal implementation details.

**🟢 GREEN — Write MINIMAL code to pass:**

- Write ONLY enough implementation code to make the failing test pass.
- Do NOT write speculative code beyond what the test requires.
- Do NOT over-engineer or add "nice to have" features.

**🔵 REFACTOR — Clean up while tests pass:**

- With the test green, improve code quality: extract helpers, reduce duplication, simplify conditionals.
- After refactoring, verify the test still passes.
- If the test breaks during refactoring, your refactor changed behavior — revert and try again.

**Repeat** the 🔴🟢🔵 cycle for each distinct behavior change.

### Step 3c: Full-Stack Sync Rules

After each Red-Green-Refactor cycle, propagate changes across the stack:

**If you modify a backend ROUTE (path, method, params, response shape):**

- Update the frontend API client (services/api.ts or equivalent)
- Update any page/component that calls that API endpoint
- Update shared TypeScript types/interfaces (already done in 3a)

**If you modify a TypeScript TYPE or INTERFACE:**

- Update all backend code that uses this type (controllers, services, routes)
- Update all frontend code that uses this type (components, hooks, pages)
- Update validation schemas (already done in 3a)

**If you modify a DATABASE SCHEMA or MODEL:**

- Update the ORM schema (already done in 3a)
- Update TypeScript interfaces to match (already done in 3a)
- Update route handlers that query this model
- Update frontend components that display this data
- Update seed files or fixtures

**If you modify a FRONTEND COMPONENT:**

- Check if props/types changed → update parent components
- Check if API calls changed → verify backend compatibility
- Update route config if the component path changed
- Update any sibling components that share state

### Step 3d: Incremental Verification

After writing EACH file, immediately verify consistency:

- Check that import paths resolve correctly in the file you just wrote.
- Verify type references match the updated types from Step 3a.
- Do NOT batch all files then check at the end — errors cascade and become harder to fix.

### 🚫 NEVER-MODIFY-TESTS-TO-PASS Rule

When a test fails, you MUST fix the IMPLEMENTATION, never the test.
The ONLY exceptions for modifying a test are:

- The test itself has a genuine bug (wrong assertion logic, not wrong expected value)
- The test setup is incorrect (missing mocks, wrong fixtures)
- The requirements explicitly changed and the test reflects old requirements
  If you are tempted to change an assertion's expected value to make it pass, STOP — that means your implementation is wrong.

---

## Phase 4: Self-Review (Completeness Check)

After all changes are written, verify nothing was missed.

### Steps:

1. Use `git_diff` to see ALL changes at once
2. Cross-reference against Phase 1 Impact Map:
   - Every "Dependent File" must either be updated OR have an explicit reason why no change was needed
   - If you discover a missed file, go back and fix it NOW
3. Run consistency checks:
   - All import paths are correct (no broken imports from renamed/moved files)
   - All type references match (no type mismatches between producer and consumer)
   - All route paths match between backend route definitions and frontend API calls
   - All function signatures match between callers and callees
4. Use `git_get_status` to confirm all changes are tracked
5. Verify no tests were weakened to pass (check git_diff for changed assertions)

### Output Format:

```
## Self-Review

### Changes Made
- [M] path/to/file.ts — description of what changed

### Dependency Verification
- path/to/dependent.ts — [OK] no changes needed: doesn't use the modified function
- path/to/api-client.ts — [UPDATED] changed endpoint path from /old to /new

### Consistency Checks
- [PASS] Import paths — all imports resolve correctly
- [PASS] Type consistency — types match across backend and frontend
- [PASS] Route path sync — frontend API client matches backend routes
- [PASS] Function signatures — callers match callees
- [PASS] Test integrity — no test assertions weakened to force passing
```

---

## Phase 5: E2E Validation & Test Verification

Verify the changes work end-to-end. If you followed Phase 3's TDD cycle, you already have unit/integration tests.

### 5a: Verify All Tests Pass

1. Review every test file you wrote or modified in Phase 3.
2. Confirm each test is meaningful — tests observable behavior, not implementation internals.
3. Check that no test was weakened or deleted to make it pass.

### 5b: E2E Test Scenarios

Define 2-3 integration/E2E scenarios that cross module boundaries:

1. **Happy path**: The primary use case end-to-end
2. **Edge case**: An error condition or boundary
3. **Cross-boundary**: Exercises both backend and frontend together

For each scenario describe:

- Preconditions (what data/state must exist)
- Steps (API calls, user actions, or code invocations)
- Expected results (response codes, UI state, database state)
- What would break if the change is incomplete

### 5c: Write E2E Tests

If test files exist in the repo (`__tests__/`, `*.test.ts`, `*.spec.ts`, `*.e2e.ts`):

- Add new E2E test cases covering the scenarios from 5b
- Write updated test files using `git_write_file`

### 5d: Generate Validation Commands

- curl commands for API endpoint testing with realistic test data
- Expected response bodies for verification
- Description of manual UI verification steps if applicable

---

## Handoff Protocol (If Approaching Turn Limit)

If you are running low on turns or context, save a handoff document BEFORE stopping:

1. Use `save_markdown` to create a file named `HANDOFF_<timestamp>.md`
2. Include:
   - **What was completed**: All files modified/created with descriptions
   - **What remains**: Pending changes from Impact Analysis not yet addressed
   - **What was tried and failed**: Approaches that didn't work
   - **Current state**: Whether the code compiles, which tests pass/fail
   - **TDD status**: Which 🔴🟢🔵 cycles were completed vs still in progress
   - **Next steps**: Exactly what the next agent should do first

---

## Common Pitfalls to Avoid

1. **Editing only the file mentioned in the request** — Always check dependent files
2. **Modifying commented-out or dead code** — Trace from entry points first
3. **Changing a backend route without updating the frontend API client** — Full-stack sync is mandatory
4. **Changing a type without updating all consumers** — Types propagate everywhere
5. **Skipping the self-review** — git diff catches missed files
6. **Not generating test scenarios** — Untested changes are incomplete changes
7. **Writing implementation before tests** — Use Red-Green-Refactor. Test FIRST, implement SECOND.
8. **Modifying test assertions to make tests pass** — NEVER change the test; fix the implementation.
9. **Writing multiple tests at once** — One test → one implementation → repeat. Keep cycles small.
10. **Batching all file writes then checking at the end** — Verify incrementally after each file.
