---
name: test-driven-development
description: "Iron law: NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST. Enforces red-green-refactor cycle for every feature and bug fix."
---

# Test-Driven Development (TDD)

## When to Use

- Writing new functions, methods, or classes
- Fixing bugs (write a test that reproduces the bug first)
- Adding new features to existing code
- Refactoring code that lacks test coverage
- Any time you're about to write production code

## The Iron Law

**NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST.**

No exceptions. No "I'll write the test later." No "this is too simple to test." The test must exist and must fail before any production code is written.

## Red-Green-Refactor Cycle

### 1. RED — Write a Failing Test
- Write the smallest possible test that describes the behavior you want
- Run the test and confirm it fails for the right reason
- A test that passes immediately is meaningless — it proves nothing

### 2. GREEN — Make It Pass
- Write the minimum amount of production code to make the test pass
- Do not add extra functionality, edge cases, or "while I'm here" changes
- Run the test and confirm it passes

### 3. REFACTOR — Clean Up
- Improve the code's structure without changing its behavior
- Run all tests after each refactoring step to confirm nothing broke
- Remove duplication, extract methods, improve naming

## Rules

- Each cycle should be short (5-15 minutes)
- Never skip the RED phase — if the test passes immediately, delete it and write a better one
- Never write more production code than needed to pass the failing test
- Keep the test suite green at all times
- If a test fails after refactoring, revert and try again

## Common Failures

| Failure | Symptom |
|---------|---------|
| Skipping RED | Test passes immediately — no proof the code works |
| Golden hammer | Writing all implementation at once, then retro-fitting tests |
| Fake tests | Tests that always pass or don't actually assert behavior |
| Fear-driven design | Writing tests that mirror implementation instead of behavior |
| Test debt | Leaving broken tests or skipping tests under time pressure |

## Quick Checklist

- [ ] Test written before code?
- [ ] Test fails for the right reason?
- [ ] Minimal code to pass?
- [ ] All tests still green?
- [ ] Refactored with tests passing?
