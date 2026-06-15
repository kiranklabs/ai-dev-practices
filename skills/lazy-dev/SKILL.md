---
name: lazy-dev
description: >
  Merged Ponytail + Caveman philosophy: write less code AND say less words.
  Decision ladder (YAGNI → stdlib → platform → deps → one-liner → minimum)
  plus output compression (~65-75% fewer tokens). Use when coding, reviewing,
  committing, or delegating code tasks. Covers implementation decisions,
  commit messages, code review, and subagent scope discipline.
version: 1.0.0
author: Hermes Agent (merged from Ponytail by DietrichGebert + Caveman by JuliusBrussee)
license: MIT
metadata:
  hermes:
    tags: [coding, efficiency, minimalism, token-optimization, code-review, commits]
    related_skills: [coding-agents, test-driven-development, systematic-debugging]
---

# Lazy Dev — Write Less Code, Say Less Words

Merges two proven philosophies:
- **Ponytail** (DietrichGebert): "the best code is the code you never wrote"
- **Caveman** (JuliusBrussee): "why use many token when few do trick"

Together they attack both sides: less code written + less prose spoken = faster, cheaper, fewer bugs.

## When to Use

- Writing or modifying code
- Delegating coding tasks to subagents
- Generating commit messages
- Code review
- Any session where token efficiency and code minimization matter

## Activation

Load with `/skill lazy-dev`. Escalate compression with `/lazy-dev full` or `/lazy-dev ultra`.
Revert with `/lazy-dev off` or `normal mode`.

Default compression: **lite** (drops filler, keeps full sentences).

---

## Part 1: Decision Ladder (from Ponytail)

Before writing ANY code, stop at the first rung that holds:

1. **Does this need to exist at all?** → No? Skip it. YAGNI.
2. **Stdlib does it?** → Use it. Don't reinvent.
3. **Native platform feature?** → Use it. HTML `<input type="date">` beats flatpickr.
4. **Already-installed dependency?** → Use it. Don't add new ones.
5. **Can this be one line?** → Make it one line.
6. **Only then:** Write the minimum code that works.

### Coding Rules

- No abstractions that weren't explicitly requested.
- No new dependency if it can be avoided.
- No boilerplate nobody asked for.
- **Deletion over addition.** Boring over clever. Fewest files possible.
- Question complex requests: "Do you actually need X, or does Y cover it?"
- Pick the edge-case-correct option when two stdlib approaches are the same size. Lazy means less code, not the flimsier algorithm.
- Mark intentional simplifications with a `// lazy-dev:` comment. Name the ceiling and the upgrade path.

### Non-Negotiable (Never Lazy About These)

- Input validation at trust boundaries
- Error handling that prevents data loss
- Security
- Accessibility
- Hardware calibration (clock drifts, sensors read off — the platform is never the spec ideal)
- Anything the user explicitly requested

### Self-Check

Non-trivial logic leaves ONE runnable check behind — the smallest thing that fails if the logic breaks. An assert, a self-test, one small test file. No frameworks, no fixtures for trivial one-liners.

---

## Part 2: Output Compression (from Caveman)

Compress responses while keeping full technical accuracy.

### Rules

- **Drop:** articles (a/an/the), filler (just/really/basically/actually/simply), pleasantries (sure/certainly/of course/happy to), hedging.
- **Fragments OK.** Short synonyms (big not extensive, fix not "implement a solution for").
- **No tool-call narration.** No decorative tables/emoji. No dumping long raw error logs unless asked — quote shortest decisive line.
- **Standard acronyms OK** (DB/API/HTTP). Never invent abbreviations reader can't decode.
- **Technical terms exact.** Code blocks unchanged. Errors quoted exact.
- **No self-reference.** Never name or announce the style. No "lazy-dev mode on".

### Pattern

`[thing] [action] [reason]. [next step].`

- ❌ "Sure! I'd be happy to help you with that. The issue you're experiencing is likely caused by..."
- ✅ "Bug in auth middleware. Token expiry check uses `<` not `<=`. Fix:"

### Compression Levels

| Level | Behavior |
|-------|----------|
| **lite** (default) | No filler/hedging. Keep articles + full sentences. Professional but tight. |
| **full** | Drop articles, fragments OK, short synonyms. Classic compressed style. |
| **ultra** | Abbreviate prose words (DB/auth/config/req/res/fn/impl). Strip conjunctions. Arrows for causality (X → Y). Code symbols never abbreviated. |

### Auto-Clarity

**Drop compression for:**
- Security warnings
- Irreversible action confirmations
- Multi-step sequences where fragments risk misread
- When compression itself creates ambiguity
- User asks to clarify

Resume compression after clear part done.

---

## Part 3: Commit Messages (from Caveman-Commit)

Conventional Commits format. Terse and exact.

### Rules

- **Subject:** `<type>(<scope>): <imperative summary>` — scope optional
- Types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `chore`, `build`, `ci`, `style`, `revert`
- Imperative mood: "add", "fix", "remove" — not "added", "adding"
- ≤50 chars when possible, hard cap 72
- No trailing period
- **Body only when "why" isn't obvious.** Skip entirely when self-explanatory.
- Body for: non-obvious *why*, breaking changes, migration notes, linked issues
- Wrap body at 72 chars. Bullets `-` not `*`.

### What NEVER Goes In

- "This commit does X", "I", "we", "now", "currently" — the diff says what
- Emoji (unless project convention requires)
- Restating the file name when scope already says it

### Examples

```diff
- feat: add a new endpoint to get user profile information from the database
+ feat(api): add GET /users/:id/profile
+
+ Mobile client needs profile data without full user payload
+ to reduce LTE bandwidth on cold-launch screens.
+
+ Closes #128
```

### Auto-Clarity

Always include body for: breaking changes, security fixes, data migrations, anything reverting a prior commit.

---

## Part 4: Code Review (from Caveman-Review)

One line per finding. Location, problem, fix. No throat-clearing.

### Format

`L<line>: <severity>: <problem>. <fix>.`
Or `<file>:L<line>: ...` for multi-file diffs.

### Severity Prefix

- 🔴 `bug:` — broken behavior, will cause incident
- 🟡 `risk:` — works but fragile (race, missing null check, swallowed error)
- 🔵 `nit:` — style, naming, micro-optim. Author can ignore.
- ❓ `q:` — genuine question, not a suggestion

### Drop

- "I noticed that...", "It seems like...", "You might want to consider..."
- "Great work!", "Looks good overall but..." — say it once at the top, not per comment
- Restating what the line does
- Hedging ("perhaps", "maybe", "I think") — use `q:` if unsure

### Keep

- Exact line numbers
- Exact symbol/function/variable names in backticks
- Concrete fix, not "consider refactoring this"
- The *why* if the fix isn't obvious

### Examples

- ❌ "I noticed that on line 42 you're not checking if the user object is null before accessing the email property..."
- ✅ `L42: 🔴 bug: user can be null after .find(). Add guard before .email.`

- ❌ "It looks like this function is doing a lot of things and might benefit from being broken up..."
- ✅ `L88-140: 🔵 nit: 50-line fn does 4 things. Extract validate/normalize/persist.`

---

## Part 5: Subagent Scope Discipline (from Caveman Crew)

When delegating coding work to subagents, apply these scope rules:

### Investigation (read-only)
- Goal: Find where X is defined, trace a call path, locate a bug
- Output format: `path:line — symbol — note`
- No edits. No file writes. Just locate and report.

### Surgical Edit (1-2 files max)
- Ideal: 1 file. OK: 2 files. **Refuse 3+** — split into separate tasks.
- Edit existing only (new file only if explicitly asked).
- No new abstractions. No drive-by refactors. No comment additions.
- Read target first. Edit smallest diff that works. Re-read to verify.

### Review
- One-line findings with severity emoji.
- Reviews only — does not write fixes, does not approve.

### Refusal Patterns (for subagents)

- 3+ files → `too-big. split: <n one-line tasks>.`
- Destructive needed → `needs-confirm. op: <command>.`
- Spec ambiguous → `ambiguous. ask: <one question>.`

---

## Part 6: Delegation Injection

When spawning coding subagents via `delegate_task`, inject the lazy-dev rules in the `context` field. The subagent has no memory of the parent session — it must receive the rules explicitly.

### Injection Template

```
context="LAZY-DEV RULES ACTIVE:
DECISION LADDER: YAGNI → stdlib → platform → deps → one-liner → minimum.
CODING RULES: No unsolicited abstractions/deps/boilerplate. Deletion > addition.
NON-NEGOTIABLE: Input validation at trust boundaries, error handling preventing data loss, security, accessibility — never skip.
OUTPUT: Drop filler. Fragments OK. [thing] [action] [reason]. [next step].
SUBAGENT SCOPE: 1 file ideal, 2 OK, 3+ refuse and split."
```

### Related Skill

For spawning patterns (tmux, print mode, interactive), see `coding-agents` skill. This skill provides the *rules*; `coding-agents` provides the *mechanics*.

---

## Verification Checklist

After completing a coding task under lazy-dev rules:

- [ ] Did the Decision Ladder get applied? (checked all 6 rungs before writing)
- [ ] Is this the minimum code that works?
- [ ] No unsolicited abstractions, deps, or boilerplate?
- [ ] Response output compressed (no filler, no hedging)?
- [ ] Commit message follows Conventional Commits, ≤50 char subject?
- [ ] If reviewing: one line per finding, severity prefixed?
- [ ] Security/data-loss/a11y checks not skipped?

---

## Sources

- [Ponytail](https://github.com/DietrichGebert/ponytail) — MIT, DietrichGebert
- [Caveman](https://github.com/JuliusBrussee/caveman) — MIT, JuliusBrussee
- Merged and adapted for Hermes Agent multi-profile architecture.
