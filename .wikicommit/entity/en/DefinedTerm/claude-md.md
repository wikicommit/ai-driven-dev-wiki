---
title: "CLAUDE.md"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-instructions, anthropic]
sources:
  - type: url
    url: 'https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more'
    hash: sha256:bb67b24e7e743610aadc45e492a9035d66952bb3cadff52ef8301bc773391708
  - type: url
    url: 'https://code.claude.com/docs/en/how-claude-code-works'
    hash: sha256:bd22d00c3d6884ed8323b1d1a90abe77a12c9df0272a5a855041afec603c6196
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A markdown file that Claude Code loads into context to give it project facts — build commands, directory layout, conventions and team norms. A root CLAUDE.md loads at session start and stays for the whole session; one in a subdirectory loads only when Claude reads a file there."
---

CLAUDE.md is a markdown file that [[SoftwareApplication/claude-code]] reads into its context so that
Claude holds a project's standing facts for the whole of a session: build commands, directory layout,
monorepo structure, coding conventions and team norms. Anthropic describes it, in
[[BlogPosting/steering-claude-code]], as an overview of the codebase, or an index pointing to other
files where Claude can find more information as needed.

## Usage

Anthropic's post distinguishes two kinds by when they load. A **root** CLAUDE.md — kept in a shared
repository, saved locally for personal preferences specific to a project, or both — loads at session
start, and all such files are re-read after Claude Code compacts the conversation, so they are not
lost or degraded across long sessions. A CLAUDE.md in a **subdirectory** below the folder where the
session started loads on demand, when Claude reads a file under that subdirectory (the post's example
is `app/api/CLAUDE.md`), and after compaction it is gone until that subdirectory is touched again.

In a monorepo the post suggests giving each team's directory its own subdirectory CLAUDE.md so teams
load only their own conventions, with a `claudeMdExcludes` setting letting developers skip files from
teams whose code they never touch. For standards that must apply to every repository in an
organisation, such as security or compliance policies, it describes a centrally managed CLAUDE.md
deployed to developer machines through MDM or configuration management, which individual settings
cannot exclude.

Anthropic's documentation of how Claude Code works gives CLAUDE.md the same role from the other side:
it lists the file among what Claude can access in every session, as the place to store
project-specific instructions, conventions and context, and notes that where a repository has an
AGENTS.md written for other coding agents, Claude can read that on its own or alongside CLAUDE.md (see
[[DefinedTerm/agents-md]]). Because each new session starts with a fresh context window and
instructions from early in a conversation can be lost to compaction, the documentation's advice is to
put persistent rules in CLAUDE.md rather than rely on conversation history. It also describes a
"Compact Instructions" section in CLAUDE.md as a way to control what is preserved when the
conversation is compacted, and an `/init` command that generates a starter CLAUDE.md for a project.

CLAUDE.md is one of seven places the post lists for instructions, and its advice is largely about what
does not belong there. Procedures such as a deployment runbook or a review checklist belong in skills
([[DefinedTerm/agent-skills]]), whose bodies load only when invoked; a constraint that applies to one
part of the codebase belongs in a path-scoped rule; and behaviour that must happen every time, or must
never happen, belongs in hooks ([[DefinedTerm/agent-hooks]]) or permissions, because a prompted rule
can fail to be followed. It calls an unscoped rule mechanically identical to putting its content in
CLAUDE.md.

## When It Applies

The post treats CLAUDE.md as the home for facts Claude should hold all the time, and its main failure
mode as growth. In a shared repository it grows the way any unowned configuration file does — every
team appends and nothing is deleted — and since every line loads into every session for every
engineer, relevant or not, the cost compounds; the post says it also dilutes adherence to the
instructions that matter. Its recommendations are to keep the file under 200 lines, give it an owner,
review changes to it like code, and write its content following the same rules as any prompt. These
are Anthropic's recommendations for its own product rather than measured thresholds.

## Related Terms

- [[DefinedTerm/agents-md]]
- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/agent-hooks]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
