# TDD Workflow Reference

## Example: Adding a User Validation Function

### Step 1: RED — Write a Failing Test

```typescript
// FILE: server/src/__tests__/validators/userValidator.test.ts
import { describe, it, expect } from "vitest";
import { validateEmail } from "../../validators/userValidator.js";

describe("validateEmail", () => {
  it("should return true for valid email", () => {
    expect(validateEmail("user@example.com")).toBe(true);
  });

  it("should return false for email without @", () => {
    expect(validateEmail("userexample.com")).toBe(false);
  });

  it("should return false for empty string", () => {
    expect(validateEmail("")).toBe(false);
  });
});
```

Run: `npm test -- --run validators/userValidator`
Expected: FAIL (function doesn't exist yet)

### Step 2: GREEN — Minimum Code to Pass

```typescript
// FILE: server/src/validators/userValidator.ts
export function validateEmail(email: string): boolean {
  if (!email) return false;
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
```

Run: `npm test -- --run validators/userValidator`
Expected: PASS (all 3 tests green)

### Step 3: REFACTOR — Clean Up

No refactoring needed in this simple case. If the regex were duplicated elsewhere, extract it to a constant.

Run tests again to confirm: PASS

## Key Principles

1. **One test at a time** — Don't write all tests upfront. Write one, make it pass, then write the next.
2. **Minimum code** — Only write enough code to pass the current failing test. Not more.
3. **Run tests constantly** — After every change, run the relevant tests.
4. **Never skip RED** — If you can't make a test fail first, you don't understand what you're building.
