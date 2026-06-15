---
name: systematic-debugging
description: "Iron law: NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST. Four-phase process for reliable bug resolution."
---

# Systematic Debugging

## When to Use

- Any bug or unexpected behavior — especially under time pressure
- When your first instinct is "I know what's wrong, let me just change X"
- When a fix seems obvious but you haven't verified the root cause
- Recurring bugs that previous "fixes" didn't actually resolve
- Production incidents where you need confidence, not speed

## The Iron Law

**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST.**

An unverified fix is a guess. A guess is not a fix. Stop before you change anything and investigate first.

## The Four Phases

### 1. Root Cause Investigation
- Reproduce the issue reliably — if you can't reproduce it, you can't fix it
- Read error messages and stack traces fully — don't skim
- Trace the data flow from input to failure point
- Check recent changes (git log, recent commits)
- Ask: "What changed?" and "Why did this work before?"

### 2. Hypothesis Formation
- Form a specific, testable hypothesis about the root cause
- One hypothesis at a time — don't juggle multiple theories
- State it clearly: "I believe X happens because of Y"
- If you can't articulate the hypothesis, you don't understand the root cause yet

### 3. Fix Implementation
- Write the minimum change that addresses the root cause
- If the fix requires large changes, question whether you truly found the root cause
- Every fix should be small enough to explain in one sentence

### 4. Verification
- Run the original reproduction steps — does the bug still occur?
- Run the existing test suite — did you break anything?
- If possible, write a regression test that catches this specific bug
- Verify edge cases around the fix

## Rules

- Never skip Phase 1 — "it looks obvious" is not investigation
- Each phase must complete before the next begins
- If Phase 3 requires more than a few lines, go back to Phase 2
- The fix must be verified with evidence, not just "it looks right"

## Common Failures

| Failure | Symptom |
|---------|---------|
| Cowboy fixing | Changing code before understanding the problem |
| Confirmation bias | Looking for evidence that supports your first theory |
| Proximity blame | Fixing the file where the error manifests, not where the bug lives |
| Partial investigation | Understanding enough to feel confident, but not enough to be right |
| No regression test | Same bug reappears in a future commit |

## Quick Checklist

- [ ] Bug reproduced reliably?
- [ ] Root cause identified (not just symptom)?
- [ ] Hypothesis stated and tested?
- [ ] Fix is minimal and targets the root cause?
- [ ] Bug no longer reproduces?
- [ ] Existing tests still pass?
- [ ] Regression test added?
