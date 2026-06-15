---
name: orchestrator
description: >
  Decision tree that ties all dev skills together. Maps the full software
  development lifecycle to the right skill at each phase. Phase 0: Understand,
  Phase 1: Plan, Phase 2: Implement, Phase 3: Quality, Phase 4: Review,
  Phase 5: Debug. Quick reference table for situation-to-skill mapping.
version: 1.0.0
license: MIT
metadata:
  tags: [workflow, orchestrator, dev-lifecycle, planning, debugging, tdd, verification]
  related_skills: [lazy-dev, test-driven-development, systematic-debugging, verification-before-completion, security-and-hardening, writing-plans, code-review, interview-me, brainstorming, context-engineering]
---

# Orchestrator — Development Lifecycle

A decision tree that coordinates your dev skills. Don't load everything — load what you need, when you need it.

## When to Use

- Starting any coding task (feature, bugfix, refactor)
- You're not sure which dev skill applies right now
- You want a structured approach but don't want to remember the full lifecycle

## How It Works

**Phase 0 → Phase 1 → ... → Done.** Each phase loads the right skill. Skip phases that don't apply.

---

## The Lifecycle

### Phase 0: Understand
**Before touching code.** Figure out what's actually needed.

- Load `interview-me` if the request is vague or could mean multiple things
- Load `brainstorming` if this is creative/feature work (not a bugfix)
- Load `context-engineering` if switching between projects/tasks

**Output:** Clear scope. What to build, what NOT to build.

### Phase 1: Plan
**Before writing code.** Break it down.

- Load `writing-plans` for multi-step work (3+ tasks)
- Load `spike` if you need to validate an approach before committing
- Load `api-and-interface-design` if designing/modifying APIs

**Output:** Ordered task list with exact file paths and success criteria.

### Phase 2: Implement
**Writing code.** This is where `lazy-dev` lives.

- **Always load `lazy-dev`** — decision ladder + compressed output
- Load `test-driven-development` if correctness matters (always load for features/bugfixes)
- Load `source-driven-development` if you need to ground decisions in official docs
- Load `frontend-ui-engineering` if building UI components

**Output:** Working code with tests.

### Phase 3: Quality
**Before claiming "done."**

- Load `verification-before-completion` — **always load this before finishing**
- Load `security-and-hardening` if touching auth, input handling, data storage
- Load `performance-optimization` if there are perf requirements
- Load `observability-and-instrumentation` if adding new features to production code
- Load `doubt-driven-development` if correctness is critical

**Output:** Verified, hardened code.

### Phase 4: Review
**Before merging.**

- Load `code-review` — covers both requesting and receiving review
- Load `simplify-code` for parallel cleanup of recent changes
- Load `finishing-a-development-branch` to integrate the work

**Output:** Reviewed, integrated code.

### Phase 5: Debug
**Anytime.** Not sequential — jumps in from any phase.

- Load `systematic-debugging` — **always start here for bugs**
- Load `browser-testing-with-devtools` for browser issues
- Load `debugging` for platform-specific debug patterns

---

## Quick Reference

| Situation | Load |
|-----------|------|
| Starting a feature | `brainstorming` → `writing-plans` → `lazy-dev` + `test-driven-development` |
| Fixing a bug | `systematic-debugging` → `lazy-dev` → `verification-before-completion` |
| Code review | `code-review` (requesting or receiving) |
| Before merging | `verification-before-completion` → `finishing-a-development-branch` |
| Security concern | `security-and-hardening` |
| Vague request | `interview-me` |
| Need to validate approach | `spike` |
| Cleaning up code | `simplify-code` |
| Multi-agent work | `dispatching-parallel-agents` or `subagent-driven-development` |
| Designing an API | `api-and-interface-design` |
| Building UI | `frontend-ui-engineering` |
| Documenting decisions | `documentation-and-adrs` |
| Git worktrees | `using-git-worktrees` |
| CI/CD | `ci-cd-and-automation` |
| Deprecation/migration | `deprecation-and-migration` |
| Performance tuning | `performance-optimization` |
| Adding observability | `observability-and-instrumentation` |

## Rules

1. **Always load `lazy-dev` in Phase 2** — it's the default coding posture
2. **Always load `verification-before-completion` in Phase 3** — never skip verification
3. **Don't load all skills at once** — load per-phase, unload when done
4. **Debugging is not sequential** — it can jump in from any phase
5. **Each skill is independent** — loading one doesn't require loading others

## Non-Negotiable

These apply regardless of which phase you're in:

- Security checks when touching auth/input/data (from `security-and-hardening`)
- Verification before claiming done (from `verification-before-completion`)
- Decision ladder before writing code (from `lazy-dev`)
- Tests before implementation when possible (from `test-driven-development`)
