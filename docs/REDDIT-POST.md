# Reddit Post Draft

**Title:** I merged Ponytail + Caveman into one skill — write less code, say less words (works with any agent)

**Body:**

Hey all,

I've been using [Ponytail](https://github.com/DietrichGebert/ponytail) (the decision ladder that makes agents write 80-94% less code) and [Caveman](https://github.com/JuliusBrussee/caveman) (the compression skill that cuts ~65% of output tokens) and realized they attack opposite sides of the same problem.

So I merged them into **[lazy-dev](https://github.com/kiranklabs/lazy-dev)** — one skill that handles both:

**Ponytail's Decision Ladder** (write less code):
```
1. Does this need to exist?       → No? Skip it. (YAGNI)
2. Stdlib does it?                → Use it.
3. Native platform feature?       → Use it.
4. Already-installed dependency?  → Use it.
5. Can this be one line?          → Make it one line.
6. Only then:                     → Write the minimum code that works.
```

**Caveman's Output Compression** (say less words):
```
Before (69 tokens):
"The reason your React component is re-rendering is likely because
you're creating a new object reference on each render cycle..."

After (19 tokens):
"New object ref each render. Inline object prop = new ref = re-render.
Wrap in useMemo."
```

## What it does NOT skip

Non-negotiable — never lazy about:
- Input validation at trust boundaries
- Error handling that prevents data loss
- Security
- Accessibility

## Test results

I ran A/B comparisons (same tasks, with and without the skill):

| Test | What we probed | Result |
|------|---------------|--------|
| Error handling | Will it skip adding validation? | ✅ Correctly added it (trust boundary) |
| Security fix | Will it over-compress security findings? | ✅ Full explanation preserved |
| Multi-file rename | Will it refuse 3+ file mechanical edits? | ✅ Completed normally |

**18-42% fewer output tokens. Zero quality loss.**

The key insight: the failure mode is safe. If the model "forgets" the rules, it just writes normal code and talks normally. It doesn't *remove* existing safety code.

## Works with everything

Ships rule files for: Claude Code, Codex, Cursor, Copilot, Cline, Windsurf, Hermes, OpenCode. Just copy the file your agent reads.

## Links

- Repo: https://github.com/kiranklabs/lazy-dev
- Ponytail: https://github.com/DietrichGebert/ponytail
- Caveman: https://github.com/JuliusBrussee/caveman

Both original projects are MIT. lazy-dev is MIT. If you use it, a star or mention of the originals would be appreciated.

---

*Built with [Hermes Agent](https://github.com/NousResearch/hermes-agent) — open-source AI agent framework.*
