# /done — end-of-session wrap-up for Claude Code

A Claude Code slash command that saves where you left off, so the next session starts
with the context it needs instead of a cold read of the repo.

Type `/done` before you close a session. It works on the current project (the git root, or
the working directory if there isn't one) and splits what it saves across two files:

- `CLAUDE.md` holds current state only. Claude Code loads it into every request, so it's
  kept to about 10,000 characters, and every line in it should still be true next session.
- `SESSION-LOG.md` holds history: dated session entries, finished work, backup names,
  plans that got replaced. It isn't auto-loaded, so it can grow.

What Claude does when you run it:

1. Measures `CLAUDE.md`, and creates either file if it's missing.
2. Adds a dated entry to the top of `SESSION-LOG.md`: what changed, files touched,
   backups made, how it was verified, gotchas, and decisions you made. If `CLAUDE.md`
   names another canonical log (a server setup log, say), server changes go there too.
3. Replaces the single `## Resume here` section in `CLAUDE.md`. Anything half-done or
   broken goes first, then the next 1–5 actions, temporary changes that need undoing,
   and anything waiting on someone else. Every open item from the old section carries
   over; an item is dropped only once it's done and logged.
4. Updates the other `CLAUDE.md` sections with targeted edits (key pointers, architecture,
   gotchas, backlog). Finished backlog items come out and new ones go in as one-liners.
5. Prunes `CLAUDE.md` (a full pass once it's over ~9,000 characters). Finished or
   superseded detail moves verbatim to the end of `SESSION-LOG.md` under
   `## Archived notes`, with headings demoted one level and a pointer left behind.
   Nothing gets deleted outright, and **Resume here is never pruned**: if the file is
   still over budget, the reply says so.
6. Syncs persistent memory, if the project has a memory directory, with pointer-level
   facts only.
7. Replies in six lines or fewer: what was saved, the `CLAUDE.md` size before and after
   (in characters and rough tokens), and the top item to resume on.

`SESSION-LOG.md` is never read in full. Claude greps for its headings and reads only the
lines around each spot it edits, so wrap-up stays cheap as the log grows.

It never commits or pushes, and it doesn't touch other projects.

You can pass a note, which ends up in the wrap-up:

```
/done left the migration half-done, tests not run
```

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

## Why two files

Long Claude Code sessions build up context that disappears when the window closes, so it
has to be written down somewhere. But `CLAUDE.md` is sent with every request. If each
session appends a log entry to it, the file grows until you're paying tokens on every
prompt for notes from three weeks ago. Keeping only the current state there, and pushing
history into a file Claude reads only when it needs to, keeps startup cheap without
losing anything.
