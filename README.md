# /done — end-of-session wrap-up for Claude Code

A Claude Code slash command that saves where you left off, so the next session starts
with the context it needs instead of a cold read of the repo.

Type `/done` before you close a session. Claude will:

1. **Update `CLAUDE.md`** in the project root (creating it if needed), which Claude Code
   loads automatically next session:
   - a dated **Session log** entry for what was built or changed
   - a **Backlog / ideas** section, with finished items removed and new ones added
   - any facts that changed: architecture, gotchas, URLs, versions
2. **Sync persistent memory** with short pointer-level notes, leaving the detail in `CLAUDE.md`.
3. **Flag unfinished work** under a **Resume here** heading, so the next session starts on it.
4. **Reply with a short summary**: what was saved and the top item to pick up.

It never commits or pushes. Saving the files is the whole job.

## Install

For every project (user-level):

```bash
mkdir -p ~/.claude/commands
curl -o ~/.claude/commands/done.md https://raw.githubusercontent.com/Arryn21/claude-done-command/main/done.md
```

For one project only, put `done.md` in that project's `.claude/commands/` folder instead.

## Use

At the end of a session:

```
/done
```

Next session, Claude reads `CLAUDE.md` on startup and picks up from **Resume here**.

## Why

Long Claude Code sessions build up context that disappears when the window closes. Keeping
the session log, the backlog and the next step in the one file Claude always reads means the
next session starts where this one stopped.
