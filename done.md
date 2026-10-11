---
description: End-of-session wrap-up — save progress notes so the next session picks up easily
---

The session is ending. Perform the end-of-session wrap-up for the current project:

1. **Update `CLAUDE.md`** in the project root (create if missing). It is the canonical
   progress file, auto-loaded next session. Make sure it reflects reality as of now:
   - Add a dated entry to a **Session log** section summarizing what was built/changed today
   - Update (or create) a **Backlog / ideas** section: remove completed items, add new ones raised today
   - Update any changed facts elsewhere in the file (architecture pieces, gotchas learned,
     URLs/services, versions)
2. **Update persistent memory** (the memory directory, if available): keep the project
   memory file consistent with CLAUDE.md — brief pointer-level updates only; CLAUDE.md
   holds the detail.
3. Do **not** commit or push anything — saving the files is enough.
4. If anything was left half-done or broken, list it prominently in CLAUDE.md under a
   **"Resume here"** heading so the next session starts there.
5. Reply with a short summary: what was saved and the top item to resume on.
