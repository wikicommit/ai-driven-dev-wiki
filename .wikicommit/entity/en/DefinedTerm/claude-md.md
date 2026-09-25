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
  - type: url
    url: 'https://docs.anthropic.com/en/docs/claude-code/memory'
    hash: sha256:b82b912f1cb5142539e561088fe1795bdeada1ef689b12e535152c8fafc326ee
  - type: url
    url: 'https://www.humanlayer.dev/blog/writing-a-good-claude-md'
    hash: sha256:fa23502d53bddbb8cccdecb704426d3137dbffcf62a88ed2965780a516d208fb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
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

Claude Code's memory documentation sets CLAUDE.md beside a second mechanism, [[DefinedTerm/auto-memory]]:
CLAUDE.md holds instructions and rules that the user writes, while auto memory holds learnings Claude
writes itself, and both are loaded at the start of every conversation as context rather than as
enforced configuration. It lists four scopes, in load order from broadest to most specific: a managed
policy file deployed organization-wide by IT or DevOps (which individual settings cannot exclude), a
user file at `~/.claude/CLAUDE.md`, a project file at `./CLAUDE.md` or `./.claude/CLAUDE.md` shared
through version control, and a personal `./CLAUDE.local.md` meant to be gitignored. Files found in the
working directory and every directory above it are concatenated rather than overriding one another,
ordered from the filesystem root down, so instructions closer to where Claude was launched are read
last, and within each directory `CLAUDE.local.md` follows `CLAUDE.md`. A CLAUDE.md can pull in other
files with `@path` imports, which are expanded into context at launch and may nest to a maximum depth
of four hops; block-level HTML comments are stripped before the content is injected, so they can hold
notes for human maintainers without costing context.

For larger projects the documentation describes splitting instructions into topic files under
`.claude/rules/`. A rule without `paths` frontmatter loads at launch with the same priority as
`.claude/CLAUDE.md`; one whose `paths` field lists glob patterns loads only when Claude reads a
matching file. It also describes Claude Code reading a repository's AGENTS.md as project instructions:
by default only when no `CLAUDE.md` or `CLAUDE.local.md` exists in the working directory or above it,
with a setting to read both, and with importing `@AGENTS.md` from a CLAUDE.md as the way to share one
file with other coding tools.

CLAUDE.md is one of seven places the post lists for instructions, and its advice is largely about what
does not belong there. Procedures such as a deployment runbook or a review checklist belong in skills
([[DefinedTerm/agent-skills]]), whose bodies load only when invoked; a constraint that applies to one
part of the codebase belongs in a path-scoped rule; and behaviour that must happen every time, or must
never happen, belongs in hooks ([[DefinedTerm/agent-hooks]]) or permissions, because a prompted rule
can fail to be followed. It calls an unscoped rule mechanically identical to putting its content in
CLAUDE.md.

HumanLayer's [[BlogPosting/writing-a-good-claude-md]], written from outside Anthropic, approaches the file
from the premise that LLMs are stateless: since CLAUDE.md is, in that post's words, the only file that by
default goes into every conversation with the agent, it should onboard Claude to the codebase by stating
the project's **what** (stack and a map of the codebase), **why** (purpose of each part) and **how** (how to
work on it and verify changes). The post says it applies equally to AGENTS.md.

## When It Applies

Anthropic's post treats CLAUDE.md as the home for facts Claude should hold all the time, and its main failure
mode as growth. In a shared repository it grows the way any unowned configuration file does — every
team appends and nothing is deleted — and since every line loads into every session for every
engineer, relevant or not, the cost compounds; the post says it also dilutes adherence to the
instructions that matter. Its recommendations are to keep the file under 200 lines, give it an owner,
review changes to it like code, and write its content following the same rules as any prompt. These
are Anthropic's recommendations for its own product rather than measured thresholds.

The memory documentation's own guidance runs the same way. It frames CLAUDE.md as the place to write
down what would otherwise be re-explained — when Claude makes the same mistake twice, when code review
catches something Claude should have known, or when a new teammate would need the same context — and
advises moving multi-step procedures to a skill and part-of-the-codebase concerns to a path-scoped
rule. It recommends targeting under 200 lines per file, on the grounds that longer files consume more
context and reduce adherence, and writing instructions concrete enough to verify ("Use 2-space
indentation" rather than "Format code properly"). It explains why a file may not be followed: CLAUDE.md
content is delivered as a user message after the system prompt, not as part of the system prompt, so
there is no guarantee of strict compliance, especially for vague or conflicting instructions — and an
instruction that must run at a fixed point, such as before every commit, should be written as a hook
instead. On size limits it states that Claude Code loads a CLAUDE.md of up to 4 MiB in full and skips a
larger file, and that after `/compact` the project-root CLAUDE.md is re-read from disk while nested
files and path-scoped rules reload only as Claude reads files they apply to.

HumanLayer's post reaches similar advice by a different route. It reports that Claude Code injects
CLAUDE.md with a system reminder saying the context may or may not be relevant, so Claude ignores
content it judges irrelevant to the current task — and the more instructions a file holds that are not
universally applicable, the more likely it is ignored. Its recommendations are to include as few
instructions as reasonably possible, keep the file concise and universally applicable (it reports a
general consensus that under 300 lines is best and says HumanLayer's own root file is under sixty lines),
move task-specific material into separate files that CLAUDE.md points to (see
[[DefinedTerm/progressive-disclosure]]), leave code style to deterministic linters and formatters rather
than the model, and write the file by hand rather than generating it with `/init`, because it is the
highest-leverage point of the harness. These are one company's recommendations drawn from its own
experience, which the post itself qualifies with "your mileage may vary".

## Related Terms

- [[DefinedTerm/agents-md]]
- [[DefinedTerm/auto-memory]]
- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/agent-hooks]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/progressive-disclosure]]
