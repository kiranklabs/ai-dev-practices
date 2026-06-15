---
name: verification-before-completion
description: "Iron law: NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE. Gate function ensures work is verified before claiming done."
---

# Verification Before Completion

## When to Use

- Before claiming any task is "done" or "complete"
- Before submitting a PR or merging to main
- Before telling a human "this is fixed"
- Before moving on to the next task
- Any time you've made changes that affect running code

## The Iron Law

**NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE.**

"It should work" is not verification. "I ran it and it works" is. Never claim completion based on assumptions, old test results, or visual inspection alone.

## Gate Function: IDENTIFY → RUN → READ → VERIFY → CLAIM

### 1. IDENTIFY — What needs to be checked?
- List every test command relevant to your changes
- Identify what "success" looks like for each
- Don't skip tests that seem "unrelated" — they might catch regressions

### 2. RUN — Execute the verification
- Run ALL relevant tests (not just the one you wrote)
- Run them fresh — never cite old results
- Capture full output, not just the exit code

### 3. READ — Actually read the output
- Scan for failures, warnings, and deprecations
- Check that expected tests actually ran (not skipped or filtered)
- A green exit code with skipped tests is not success

### 4. VERIFY — Confirm against success criteria
- Did every test pass?
- Did every expected test run?
- Are there any warnings that indicate future problems?
- Does the output match what you expect for the changes you made?

### 5. CLAIM — Only then claim completion
- State what you verified and the evidence
- Include the specific commands you ran and their output
- If verification fails, return to the task — do not claim done

## Rules

- Verification must be fresh — run it now, not last time
- Never trust cached results or "it passed before"
- If you can't run the tests, you can't claim completion
- Partial verification is not verification
- When in doubt, run it again

## Common Failures

| Failure | Symptom |
|---------|---------|
| Assumption completion | "I wrote the code, it must work" |
| Stale results | "It passed last time" without re-running |
| Partial verification | Only running the test you wrote, not the full suite |
| Cosmetic check | Looking at code instead of running it |
| Selective tests | Filtering out failures as "expected" without proof |

## Red Flags

- You haven't run any commands before claiming done
- You're citing test results from earlier in the session
- You say "it should work" instead of "it passed"
- You changed code but didn't re-run the test suite
- You're tired and tempted to skip verification

## Quick Checklist

- [ ] All relevant tests identified?
- [ ] Tests run fresh (not cached)?
- [ ] Output read and understood?
- [ ] All tests passed?
- [ ] No skipped or filtered tests?
- [ ] Verification evidence captured?
