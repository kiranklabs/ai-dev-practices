# ai-dev-practices — Best Practices for AI Coding

@./skills/guardrails/SKILL.md
@./skills/orchestrator/SKILL.md
@./skills/lazy-dev/SKILL.md
@./skills/tdd/SKILL.md
@./skills/debugging/SKILL.md
@./skills/verification/SKILL.md
@./skills/security/SKILL.md
@./skills/planning/SKILL.md
@./skills/code-review/SKILL.md

## Claude Code Notes

- Load individual skills: `/skill lazy-dev`, `/skill tdd`, etc.
- The orchestrator (`skills/orchestrator/SKILL.md`) coordinates which skill to load per phase
- `guardrails` is always active — classifies every action as RED/YELLOW/GREEN
- Compression levels: `/lazy-dev full` or `/lazy-dev ultra`
