# lazy-dev

> Merge of [Ponytail](https://github.com/DietrichGebert/ponytail) + [Caveman](https://github.com/JuliusBrussee/caveman)
> **Write less code. Say less words. Ship faster.**

lazy-dev combines two proven AI coding philosophies into one agent-agnostic skill:

- **Ponytail** (DietrichGebert): A decision ladder that makes agents write 80-94% less code by enforcing YAGNI, stdlib-first, and minimum-viable implementation
- **Caveman** (JuliusBrussee): Output compression that cuts 65-75% of response tokens while keeping full technical accuracy

Together they attack both sides of the token equation: less code written + less prose spoken = faster, cheaper, fewer bugs.

## What It Does

Before writing any code, the agent walks the **Decision Ladder**:

```
1. Does this need to exist?       → No? Skip it. (YAGNI)
2. Stdlib does it?                → Use it.
3. Native platform feature?       → Use it.
4. Already-installed dependency?  → Use it.
5. Can this be one line?          → Make it one line.
6. Only then:                     → Write the minimum code that works.
```

While communicating, it applies **Output Compression**:

```
Before (69 tokens):
"The reason your React component is re-rendering is likely because
you're creating a new object reference on each render cycle..."

After (19 tokens):
"New object ref each render. Inline object prop = new ref = re-render.
Wrap in useMemo."
```

## What It Does NOT Skip

These are **non-negotiable** — never lazy about:

- Input validation at trust boundaries
- Error handling that prevents data loss
- Security
- Accessibility
- Anything the user explicitly requested

## Test Results

Tested with an A/B comparison across 3 coding tasks (see [docs/TEST-RESULTS.md](docs/TEST-RESULTS.md) for full details):

| Test | What We Probed | Result |
|------|---------------|--------|
| **Error handling** (false YAGNI) | Will the agent skip adding validation? | ✅ Correctly identified as non-negotiable |
| **Security fix** (auto-clarity) | Will it over-compress security findings? | ✅ Full explanation for security issues |
| **Multi-file rename** (scope refusal) | Will it refuse 3+ file mechanical edits? | ✅ Correctly completed (not an abstraction) |

**Key findings:**
- Code quality identical between lazy-dev and standard agent
- 18-42% fewer output tokens
- No false YAGNI — trust boundary validation was always added
- Security findings received full treatment, not compressed
- Failure mode is safe: worst case, agent writes normal code and talks normally

## Installation

### Claude Code

Add to your project root:

```bash
# Copy the rules
cp skills/lazy-dev/SKILL.md ./CLAUDE.md
```

Or install as a skill:
```bash
/plugin marketplace add <your-org>/lazy-dev
/plugin install lazy-dev@lazy-dev
```

### Codex

```bash
cp skills/lazy-dev/SKILL.md ./AGENTS.md
```

### OpenCode

Add to `opencode.json`:
```json
{
  "plugin": ["./skills/lazy-dev/SKILL.md"]
}
```

### Cursor

Copy to project root:
```bash
cp skills/lazy-dev/SKILL.md .cursorrules
```

### Windsurf

```bash
mkdir -p .windsurf
cp skills/lazy-dev/SKILL.md .windsurf/rules.md
```

### Cline

```bash
cp skills/lazy-dev/SKILL.md .clinerules
```

### GitHub Copilot

```bash
mkdir -p .github
cp skills/lazy-dev/SKILL.md .github/copilot-instructions.md
```

### Hermes Agent

```bash
# Copy to your Hermes skills directory
mkdir -p ~/.hermes/skills/software-development/lazy-dev
cp skills/lazy-dev/SKILL.md ~/.hermes/skills/software-development/lazy-dev/SKILL.md

# Load in session
# /skill lazy-dev
```

### Any Agent

Copy `skills/lazy-dev/SKILL.md` to whatever rules/instructions file your agent reads. The content is plain markdown — no agent-specific syntax.

## Compression Levels

| Level | Behavior |
|-------|----------|
| **lite** (default) | No filler/hedging. Keep articles + full sentences. Professional but tight |
| **full** | Drop articles, fragments OK, short synonyms. Classic compressed style |
| **ultra** | Abbreviate prose words. Strip conjunctions. Arrows for causality (X → Y) |

## The Rules (Quick Reference)

### Decision Ladder
1. YAGNI — does this need to exist?
2. Stdlib does it — use it
3. Platform feature — use it
4. Installed dep — use it
5. One line — make it one line
6. Minimum code that works

### Coding Rules
- No abstractions not explicitly requested
- No new dependency if avoidable
- No boilerplate nobody asked for
- Deletion over addition. Boring over clever. Fewest files possible
- Mark intentional simplifications with `// lazy-dev:` comment

### Output Compression
- Drop: articles, filler, pleasantries, hedging
- Fragments OK. Short synonyms.
- Pattern: `[thing] [action] [reason]. [next step].`
- No self-reference ("lazy-dev mode on")

### Commit Messages
- Conventional Commits, subject ≤50 chars
- Body only when "why" isn't obvious
- Never: "This commit does X", "I", "we"

### Code Review
- One line per finding: `L<line>: <severity>: <problem>. <fix>.`
- Severity: 🔴 bug, 🟡 risk, 🔵 nit, ❓ question

### Auto-Clarity
- Drop compression for: security warnings, irreversible actions, ambiguous sequences
- Resume compression after clear part done

## Attribution

This skill merges the work of two open-source projects:

- **[Ponytail](https://github.com/DietrichGebert/ponytail)** by DietrichGebert — MIT License
- **[Caveman](https://github.com/JuliusBrussee/caveman)** by JuliusBrussee — MIT License

lazy-dev is licensed under MIT. If you use this in your project, a star or mention of the original repos would be appreciated.

## Contributing

Issues and PRs welcome. If you find a case where the decision ladder gives wrong advice, or where compression loses critical meaning, please open an issue with the specific scenario.

## License

MIT
