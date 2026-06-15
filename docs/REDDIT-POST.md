# lazy-dev — Reddit Post

**Title:** Merged Ponytail + Caveman into one skill — less code, fewer tokens, any agent

---

I've been running [Ponytail](https://github.com/DietrichGebert/ponytail) (decision ladder → 80-94% less code) and [Caveman](https://github.com/JuliusBrussee/caveman) (output compression → 65% fewer tokens) side by side and realized they're complementary — one cuts what you write, the other cuts what you say.

Merged them into **[lazy-dev](https://github.com/kiranklabs/lazy-dev)** — a single skill, works with any agent that reads rules files.

**The core:**

```
1. Does this need to exist?       → No? Skip it.
2. Stdlib does it?                → Use it.
3. Platform feature?              → Use it.
4. Installed dep?                 → Use it.
5. One line?                      → Make it one line.
6. Only then:                     → Minimum code that works.
```

Plus output compression (drop filler, fragments OK, short synonyms).

**Non-negotiable:** security, data loss, accessibility — never lazy.

**Tested A/B across 3 tasks:**
- Added input validation when it should (trust boundary → correctly not skipped)
- Fixed SQL injection without over-compressing the security explanation
- Completed a 3-file rename without false scope refusal
- 18-42% fewer output tokens, zero quality loss

**Works with:** Claude Code, Codex, Cursor, Copilot, Cline, Windsurf, Hermes, OpenCode. Just copy the file your agent reads.

[Repo](https://github.com/kiranklabs/lazy-dev) · [Ponytail](https://github.com/DietrichGebert/ponytail) · [Caveman](https://github.com/JuliusBrussee/caveman) — both MIT, lazy-dev is MIT too.
