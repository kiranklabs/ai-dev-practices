# Reddit Post — ai-dev-practices

**Title:** Built 9 skills for AI coding agents — guardrails + lazy-dev + TDD + debugging (from Ponytail + Caveman + a production incident)

---

Been collecting AI coding best practices and turned them into **[ai-dev-practices](https://github.com/kiranklabs/ai-dev-practices)** — 9 modular skills that cover the full dev lifecycle. Works with any agent that reads rules files.

**Three things merged into one repo:**

**1. [Ponytail](https://github.com/DietrichGebert/ponytail)** — Decision ladder → 80-94% less code:
```
1. Does this need to exist?       → No? Skip it.
2. Stdlib does it?                → Use it.
3. Platform feature?              → Use it.
4. Installed dep?                 → Use it.
5. One line?                      → Make it one line.
6. Only then:                     → Minimum code that works.
```

**2. [Caveman](https://github.com/JuliusBrussee/caveman)** — Output compression → 65% fewer tokens:
```
Before: "The reason your React component is re-rendering is likely because
you're creating a new object reference on each render cycle..."
After:  "New object ref each render. Wrap in useMemo."
```

**3. Agent guardrails** — Born from a real production incident where an AI agent deleted a database in 9 seconds. Classifies every action as RED/YELLOW/GREEN and forces verification before destructive operations.

**Plus:** TDD, systematic debugging, verification, security (STRIDE), planning, code review.

**Tested A/B across 3 tasks:**
- Added input validation when it should (trust boundary → not skipped)
- Fixed SQL injection without over-compressing the security explanation
- Completed a 3-file rename without false scope refusal
- 18-42% fewer output tokens, zero quality loss

**9 skills, each with an iron law:**

| Skill | Iron Law |
|-------|----------|
| guardrails | Classify every action RED/YELLOW/GREEN |
| lazy-dev | YAGNI + output compression |
| tdd | No code without a failing test first |
| debugging | No fixes without investigation first |
| verification | No claims without fresh evidence |
| security | STRIDE at every trust boundary |
| planning | 2-5 min tasks, exact file paths |
| code-review | Verify before implementing feedback |
| orchestrator | Load the right skill per phase |

**Works with:** Claude Code, Codex, Cursor, Copilot, Cline, Windsurf, Hermes, OpenCode. Just copy the file your agent reads.

[Repo](https://github.com/kiranklabs/ai-dev-practices) · [Ponytail](https://github.com/DietrichGebert/ponytail) · [Caveman](https://github.com/JuliusBrussee/caveman) — all MIT.
