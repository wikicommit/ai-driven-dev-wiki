---
title: "Auto Memory"
type: "schema:DefinedTerm"
lang: en
tags: [agent-memory, context-engineering, anthropic]
sources:
  - type: url
    url: 'https://docs.anthropic.com/en/docs/claude-code/memory'
    hash: sha256:b82b912f1cb5142539e561088fe1795bdeada1ef689b12e535152c8fafc326ee
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Claude Code mechanism in which Claude writes its own notes — about the user, corrections and confirmed approaches, ongoing project decisions, and where to find outside information — into a per-repository memory directory whose MEMORY.md index is loaded at the start of every session."
---

Auto memory is the mechanism by which [[SoftwareApplication/claude-code]] lets Claude accumulate
knowledge across sessions without the user writing anything: as it works, Claude saves notes for
itself, based on the user's corrections and preferences, into a memory directory for the project, and
an index of those notes is loaded at the start of every conversation. Anthropic's documentation
presents it as one of two complementary memory systems, alongside [[DefinedTerm/claude-md]]: CLAUDE.md
files are written by the user and hold instructions and rules, while auto memory is written by Claude
and holds learnings and patterns. Both are treated as context rather than enforced configuration.

## Usage

The documentation lists four kinds of note, recorded as a `type` field in each memory file's
frontmatter: `user` (the user's role, expertise and working preferences), `feedback` (corrections the
user gives and approaches they confirm), `project` (ongoing work, deadlines and decisions that cannot be
derived from the code or git history) and `reference` (where to find information outside the project,
such as an issue tracker or dashboard). Claude skips anything it can derive from the codebase — such as
architecture, file paths or debugging fixes — and anything the CLAUDE.md files already say, and does not
save something every session, deciding by whether the information would be useful in a future
conversation.

Each project gets its own directory at `~/.claude/projects/<project>/memory/`, with the `<project>`
path derived from the git repository so that all worktrees and subdirectories of one repository share a
single memory directory; the directory can be relocated with an `autoMemoryDirectory` setting. It holds
a `MEMORY.md` index, one line per memory, and one topic file per memory. Only the first 200 lines or
25KB of `MEMORY.md`, whichever comes first, is loaded at session start, and Claude Code reminds Claude to
shorten the index when it nears either limit, because content past the limit is dropped on the next
load; topic files are not loaded at startup but read on demand with Claude's ordinary file tools. Auto
memory is machine-local — not shared across machines or cloud environments — and its files are excluded
from the retention sweep that deletes old session transcripts. It is on by default, can be toggled from
the `/memory` command or with an `autoMemoryEnabled` setting, and can be disabled with an environment
variable; the files are plain markdown the user can read, edit or delete.

The same mechanism extends to [[DefinedTerm/sub-agent-architecture]] as Claude Code implements it: the
main conversation's auto memory is not loaded into a subagent (a fork, which inherits the parent
conversation, is the exception), but a subagent can be given persistent memory of its own through a
`memory` field, kept in a separate directory. When a user asks Claude to remember something, such as
always using a particular package manager, the documentation says Claude saves it to auto memory; adding
it to CLAUDE.md instead requires asking for that explicitly or editing the file.

## Related Terms

- [[DefinedTerm/claude-md]] — the user-written counterpart it is paired with
- [[DefinedTerm/memory-bank]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
