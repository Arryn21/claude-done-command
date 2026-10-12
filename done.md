---
description: End-of-session wrap-up for any project. Keeps CLAUDE.md small (current state only), appends history to SESSION-LOG.md
argument-hint: "[optional notes, e.g. 'left X half-done']"
---

The session is ending. Wrap up the **current project** (git root, else the working directory) so the next session
starts fast and cheap. Extra notes from the user, if any: $ARGUMENTS

Two files, two jobs:
- `CLAUDE.md` (project root) is auto-loaded into EVERY request. It holds **current state only**. Budget: about
  **10,000 characters**. Every line must still be true and useful next session.
- `SESSION-LOG.md` (project root) is NOT auto-loaded. It holds history: dated session entries, finished work,
  rollback/backup details, replaced plans. It can grow.

Steps:

1. **Measure** `CLAUDE.md` (`wc -c`) and note the size. If it's missing, create it with the sections in step 4.
   If `SESSION-LOG.md` is missing, create it with a title, a line saying it is not auto-loaded and is newest-first,
   and a `## Entries` heading.

2. **Session entry** at the top of `## Entries` in `SESSION-LOG.md` (newest first):
   `- **YYYY-MM-DD (<where: local / server / both>):** what changed, files touched, backups made (names), what was
   verified and how, gotchas learned, decisions the user made.` The detail goes here, not in CLAUDE.md.

3. **Rewrite `## Resume here` in `CLAUDE.md`. Replace it; never add a second one.** Only: the next 1–5 concrete
   actions, anything half-done or broken (first, in bold), anything TEMPORARY that must be undone and how, and what's
   waiting on the user or someone else. Date in the heading. If nothing is pending, say so.

4. **Update the other `CLAUDE.md` sections in place** (create missing ones; keep the project's own extra sections).
   Typical layout: `## Resume here` · `## Key pointers` (commands, paths, URLs, where secrets live, never the secrets
   themselves) · `## Architecture` · `## Gotchas` · `## Backlog / ideas`.
   - Edit facts that changed (versions, hosts, URLs, file names). No dated "what I did today" paragraphs.
   - Backlog: remove finished items, add new ones as one-liners.
   - Gotchas: only ones that will bite again **in this project**. A technique useful across projects goes in
     `~/.claude/skills/<category>/SKILL.md` instead (per the global CLAUDE.md skill-file rules).

5. **Prune** (always check; required when over budget): move to `SESSION-LOG.md` under `## Archived notes`,
   verbatim, anything finished, superseded, old as-built detail, per-change backup names, or long explanations a
   pointer could replace. In `CLAUDE.md`, replace the detail with a pointer to the file that has it. Never delete
   information outright; move it. Make sure `CLAUDE.md` mentions `SESSION-LOG.md` near the top.

6. **Memory** (if this project has a memory directory): pointer-level facts only, one line per file in `MEMORY.md`.
   Don't copy CLAUDE.md content. Fix or delete memories that are now wrong.

7. Do **not** commit or push. Don't touch other projects.

8. **Reply in ≤6 lines:** what was saved, `CLAUDE.md` size before → after (chars and ≈chars/4 tokens), and the top
   item to resume on.
