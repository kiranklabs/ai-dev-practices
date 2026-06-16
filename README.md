# ai-dev-practices

> Best practices for AI coding agents — 9 modular skills, agent-agnostic, tested.

A collection of **9 skills** that cover the full software development lifecycle. Each skill is standalone. Use the orchestrator to coordinate them, or pick individual skills for your workflow.

**Built on:** [Ponytail](https://github.com/DietrichGebert/ponytail) + [Caveman](https://github.com/JuliusBrussee/caveman) + battle-tested Hermes Agent patterns + real incident lessons (Cursor/Railway production deletion).

## Skills

| Skill | What it does | Iron Law |
|-------|-------------|----------|
| **[guardrails](skills/guardrails/SKILL.md)** | Pre-action safety checklist | Classify every action RED/YELLOW/GREEN |
| **[lazy-dev](skills/lazy-dev/SKILL.md)** | Write less code, say less words | YAGNI + output compression |
| **[tdd](skills/tdd/SKILL.md)** | Test-driven development | No code without a failing test first |
| **[debugging](skills/debugging/SKILL.md)** | Systematic root cause analysis | No fixes without investigation first |
| **[verification](skills/verification/SKILL.md)** | Pre-completion verification | No claims without fresh evidence |
| **[security](skills/security/SKILL.md)** | Threat modeling + hardening | STRIDE at every trust boundary |
| **[planning](skills/planning/SKILL.md)** | Bite-sized implementation plans | 2-5 min tasks, exact file paths |
| **[code-review](skills/code-review/SKILL.md)** | Request + receive reviews | Verify before implementing feedback |
| **[orchestrator](skills/orchestrator/SKILL.md)** | Decision tree for the lifecycle | Load the right skill at the right phase |

**Total: ~52KB of rules.** Load one at a time, not all at once. `guardrails` is the universal overlay — always active.

## The Lifecycle

```
Phase -1: Guardrails  →  Classify every action. RED/YELLOW/GREEN. (always active)
Phase 0: Understand   →  What does the user actually need?
Phase 1: Plan         →  Break it into 2-5 min tasks
Phase 2: Implement    →  lazy-dev + tdd (write less, test first)
Phase 3: Quality      →  verification + security
Phase 4: Review       →  code-review (request + receive)
Phase 5: Debug        →  (jumps in from any phase when things break)
```

## What Makes This Different

**Three origins, one system:**

1. **[Ponytail](https://github.com/DietrichGebert/ponytail)** — The decision ladder. "The best code is the code you never wrote." Makes agents check YAGNI → stdlib → platform → deps → one-liner → minimum code.

2. **[Caveman](https://github.com/JuliusBrussee/caveman)** — Output compression. "Why use many token when few do trick." Cuts 65-75% of response tokens while keeping technical accuracy.

3. **Agent guardrails** — Born from the [Cursor/Railway incident](https://github.com/kiranklabs/ai-dev-practices/blob/main/skills/guardrails/SKILL.md) where an AI agent deleted a production database in 9 seconds. Makes safety procedural, not declarative.

**Plus battle-tested patterns** from Hermes Agent's 30+ software development skills: TDD, systematic debugging, verification before completion, code review, and planning.

## Quick Start

### Claude Code
```bash
# Copy the orchestrator (references all skills)
cp skills/orchestrator/SKILL.md ./CLAUDE.md

# Or pick individual skills
cp skills/lazy-dev/SKILL.md ./CLAUDE.md
```

### Codex / OpenCode
```bash
cp skills/orchestrator/SKILL.md ./AGENTS.md
```

### Cursor
```bash
cp skills/orchestrator/SKILL.md .cursorrules
```

### Copilot
```bash
mkdir -p .github
cp skills/orchestrator/SKILL.md .github/copilot-instructions.md
```

### Windsurf
```bash
mkdir -p .windsurf
cp skills/orchestrator/SKILL.md .windsurf/rules.md
```

### Cline
```bash
cp skills/orchestrator/SKILL.md .clinerules
```

### Hermes Agent
```bash
# Copy all skills
cp -r skills/* ~/.hermes/skills/software-development/

# Load in session
# /skill lazy-dev
# /skill dev-workflow (orchestrator)
```

### Any Agent
Copy `skills/orchestrator/SKILL.md` to whatever rules/instructions file your agent reads. The content is plain Markdown — no agent-specific syntax.

## Installation (Pick Your Style)

**Option A: Orchestrator only** — One file that references all skills. Agent loads skills on-demand per phase. Guardrails always active.

**Option B: Individual skills** — Copy only the skills you want. Mix and match.

**Option C: All skills** — Copy everything. Orchestrator coordinates.

## Design Principles

1. **One skill per concern** — No mega-skills. Load what you need.
2. **Iron laws** — Each skill has one non-negotiable rule.
3. **Agent-agnostic** — Plain Markdown. Works with any agent that reads rules files.
4. **Tested** — A/B comparison results in [docs/TEST-RESULTS.md](docs/TEST-RESULTS.md).
5. **Attribution** — Built on Ponytail + Caveman + real incident lessons. MIT licensed.

## Test Results

See [docs/TEST-RESULTS.md](docs/TEST-RESULTS.md) for A/B comparison data across 3 coding tasks.

**Key finding:** lazy-dev (the core skill) delivers 18-42% token savings with zero quality loss. The failure mode is safe — worst case, the agent writes normal code and talks normally.

## Attribution

- [Ponytail](https://github.com/DietrichGebert/ponytail) by DietrichGebert — Decision ladder philosophy
- [Caveman](https://github.com/JuliusBrussee/caveman) by JuliusBrussee — Output compression + commit/review patterns
- [Hermes Agent](https://github.com/NousResearch/hermes-agent) by Nous Research — Testing framework + skill patterns
- Cursor/Railway incident — Guardrails origin story

All skills are MIT licensed. Star the original repos if you find this useful.

## Contributing

Issues and PRs welcome. If a skill gives wrong advice in your context, open an issue with the specific scenario.

## License

MIT
