# Test Behavior, Not Implementation

A test calls the code the way its users do and asserts the result they observe against a literal expected value. A test that asserts which internal functions the code called, or restates a constant the code contains, does neither. At a system boundary the outbound call *is* the result: the charge sent to the payment API or the message handed to the mailer is what users observe, so assert its payload.

The check: before you keep a test, ask whether it would still pass if the code under test gave a plausible wrong answer: `undefined`, an empty value, a wrong value of the right type, or a boundary call with the wrong payload. If one does, the test cannot fail for that defect. Rewrite the assertion or delete the test.

**Why:** A test that cannot fail for a defect costs CI time and review attention and catches nothing. A constant pin also fails when someone edits the constant or the prompt it restates, so it prevents that edit.

**Five shapes that pass a wrong answer:**

- **Weak assertion.** Passes any wrong value of the right type: no `expect`, `toBeDefined`, `toBeTruthy`, `toBeInstanceOf`, `toBeGreaterThan(0)`, `not.toThrow`, `toHaveBeenCalled` without a payload check.
- **Absence only.** Passes `undefined` or an empty result: `toBeUndefined`, `not.toHaveBeenCalled`, `not.toBe(wrongValue)`, `toEqual([])`, `toHaveLength(0)`.
- **Self-referential.** The expected value comes from the code under test, or is recomputed the way the code computes it: `expect(f(a)).toBe(f(a))`, `expect(parsed.url).toBe(buildUrl(...))`, `expect(add(a, b)).toBe(a + b)`. Expected values come from an independent source: a known-good literal, a worked example, the spec.
- **Constant pin.** The assertion restates a hand-maintained constant, config default, table row, or prompt string: `expect(LIMITS.maxTools).toBe(8)`, `expect(PROMPT).toContain("You are")`.
- **Fixture asserts fixture.** The assertion reads data the test built or a value computed in `beforeEach`, and the subject never runs inside the body.

**The fix:** call the subject inside the test body with one concrete input and assert the literal output or the observable effect, `expect(slugify("Hello, World!")).toBe("hello-world")`. For an absence, assert the presence on the other input in the same test. For a constant, test the mechanism that reads it with one input instead of restating the value. For a boundary mock, assert the payload it received or the state after the call, not that it was called. When no such assertion exists, delete the test.

**Keep** a test of a relation across a table's rows (a key present in two tables, a parent that exists), and a compile-time check in a `*.test-d.ts` file.

**Name and scope:** one behavior per test, one logical assertion. The name says what a caller can do ("user can checkout with valid cart"), not how the code does it ("checkout calls paymentService.process"). A how-name is the first sign the test is coupled to internals.

## Where tests go

A **seam** is the public interface where you observe behavior without reaching inside. Tests live at seams. A test that mocks internal collaborators, calls private methods, or verifies through a side channel (querying the database instead of reading back through the interface) breaks on a refactor that kept behavior intact.

**Test only at pre-agreed seams.** Before writing any test, ask "what's the public interface, and which seams should we test?", write the seams down, and confirm them with the user. Agreeing them up front puts testing effort on the critical paths and complex logic instead of every edge case. When the interface shape itself is in question (how deep the module is, where the seam belongs), read the `codebase-design` skill. Read `CONTEXT.md` if it exists so test names match the project's domain language.

**Mock at system boundaries only:** external APIs, time, randomness, and sometimes the database or filesystem (prefer a real test database). Your own modules and internal collaborators run for real. At those boundaries, pass the dependency in instead of constructing it inside, and give each external operation its own function (`api.getUser`, `api.createOrder`) instead of one generic `fetch(endpoint, options)`, so each mock returns one shape with no conditional logic in test setup.

## Test-first loop (TDD)

When building test-first, the loop is red → green:

- **Red before green.** Write the failing test first, then only enough code to pass it. No anticipated tests or speculative features.
- **Vertical slices.** One seam, one test, one minimal implementation per cycle, each test a **tracer bullet** that responds to what the last cycle taught you. Writing all tests first and then all implementation tests imagined behavior and commits to test structure before you understand the code.
- **Refactoring belongs to review**, not the red → green cycle.
