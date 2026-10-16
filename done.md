---
description: End-of-session wrap-up for any project. Keeps CLAUDE.md small (current state only), appends history to SESSION-LOG.md
argument-hint: "[optional notes, e.g. 'left X half-done']"
---

Wrap up the current project (git root, else working directory). User notes: $ARGUMENTS

- `CLAUDE.md` = auto-loaded every request: **current state only**, budget ~10,000 chars, every line true and useful.
- `SESSION-LOG.md` = not auto-loaded: history, newest first (`## Entries`), archive at the end (`## Archived notes`).
  Never Read it in full: `grep -n '^## '` for line numbers, Read only around the spot you edit.
- Missing files: create them (SESSION-LOG with title, "not auto-loaded, newest first", `## Entries`).

1. `wc -c CLAUDE.md` (note size).
2. **Log entry** at the top of `## Entries`: `- **YYYY-MM-DD (local / server / both):** what changed, files, backups
   (names), what was verified and how, gotchas, user decisions.` If `CLAUDE.md` names another canonical log (e.g. a
   server setup log), log server changes/backups there too.
3. **Replace `## Resume here`** (one only, dated heading): half-done/broken items first in bold, next 1–5 numbered
   actions, TEMPORARY changes and how to undo them, what waits on others. **Carry over every open item** from the old
   one, links included; drop an item only if done and logged in step 2. Extra open items stay here as one-liners
   (e.g. `Parked:`). Nothing pending → say so.
4. **Other sections, targeted Edits** (no full rewrite): Key pointers (commands, paths, URLs, where secrets live,
   never secrets) · Architecture · Gotchas · Backlog / ideas; keep the project's own sections. Fix changed facts, no
   dated narratives. Backlog: drop finished, add one-liners. Gotchas: project-only; cross-project techniques go to
   `~/.claude/skills/<category>/SKILL.md`.
5. **Prune** only stale lines; full pass if over ~9,000 chars. Move (never delete) finished, superseded, as-built
   detail, backup names, long explanations to the end of `## Archived notes`, verbatim but headings one level down
   (`##`→`###`). Leave a pointer behind. Order: Backlog, Gotchas, Architecture, Key pointers detail. **Never prune
   `## Resume here`**; if still over budget, say so. Keep the `SESSION-LOG.md` mention near the top of `CLAUDE.md`.
6. **Memory** (if any): use the `MEMORY.md` index in context; open a memory only to change it. Pointer-level, no
   CLAUDE.md copies; fix or delete wrong ones.
7. No commit/push. Don't touch other projects.
8. **Reply ≤6 lines:** what was saved, `CLAUDE.md` size before → after (chars, ≈/4 tokens), top resume item.
