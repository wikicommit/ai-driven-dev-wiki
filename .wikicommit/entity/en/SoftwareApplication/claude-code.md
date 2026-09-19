---
title: "Claude Code"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, anthropic, coding-tools, context-window]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
    hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's agentic coding solution, which combines up-front context files with just-in-time file and data retrieval, message-history compaction, and to-do list note-taking."
  applicationCategory: "Agentic coding tool"
  featureList: "Targeted database queries with stored results; Bash primitives including head, tail, glob and grep; CLAUDE.md context files loaded up front; message-history compaction; a to-do list for agentic note-taking"
  author: "[[Organization/anthropic]]"
---

Claude Code is Anthropic's agentic coding solution. Anthropic uses it as the worked example for
several of the [[DefinedTerm/context-engineering]] techniques it recommends, and describes it as
performing complex data analysis over large databases without ever loading full data objects into
context: the model writes targeted queries, stores the results, and leverages Bash commands such
as `head` and `tail` to analyse large volumes of data.

Anthropic characterises Claude Code as employing a hybrid context strategy — retrieving some data
up front for speed while pursuing further autonomous exploration at its discretion. CLAUDE.md
files are naively dropped into context up front, while primitives such as glob and grep let it
navigate its environment and retrieve files just in time, which Anthropic says effectively
bypasses the issues of stale indexing and complex syntax trees.

## Capabilities
- [[DefinedTerm/just-in-time-context-retrieval]] over large data sets: targeted queries whose
  results are stored, plus Bash primitives such as `head` and `tail` for working through large
  volumes without loading them whole.
- File-system navigation through glob and grep, retrieving files as they are needed rather than
  from a pre-built index.
- CLAUDE.md files, dropped into context up front as the fixed half of its hybrid strategy.
- [[DefinedTerm/compaction]] of the message history: the history is passed to the model to
  summarise and compress the most critical details, preserving architectural decisions,
  unresolved bugs and implementation details while discarding redundant tool outputs or messages.
  The agent then continues with that compressed context plus the five most recently accessed
  files, which Anthropic says gives users continuity without their having to worry about context
  window limitations.
- A to-do list, which Anthropic gives as an instance of [[DefinedTerm/structured-note-taking]].
- An on-demand planning mode, added more recently than some rival agents, in which the agent generates a plan and awaits human review before proceeding — contrasted by [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] with Google's [[SoftwareApplication/google-jules]], which has included a planning step from its inception.
- A set of extension mechanisms documented as distinct choices rather than alternatives: skills
  (`SKILL.md` files under `.claude/skills/`, loaded on demand so that domain knowledge does not
  occupy every conversation — see [[DefinedTerm/agent-skills]]), hooks running scripts at fixed
  points in the workflow ([[DefinedTerm/agent-hooks]]), custom subagents defined under
  `.claude/agents/` with their own context and tool set ([[DefinedTerm/sub-agent-architecture]]),
  MCP servers ([[DefinedTerm/model-context-protocol]]), and plugins bundling several of these.
- Session controls for working against the context constraint: `/clear` to reset between unrelated
  tasks, `/compact` with optional focusing instructions, and checkpoints created on every prompt that
  starts a turn, restorable through a rewind menu. The documentation is explicit that checkpoints
  track only changes made through the file-editing tools — changes made via Bash or external
  processes are not captured — and that this is not a replacement for git.
- Non-interactive operation via `claude -p "prompt"`, with plain-text, JSON and streaming-JSON output
  formats, intended for CI pipelines, pre-commit hooks and scripted fan-out across many files.

## Working Practices

Anthropic's best-practices documentation organises its guidance around a single stated constraint:
the context window holds the entire conversation — every message, every file read, every command
output — it fills fast, and model performance degrades as it does. Most of the remaining advice is
presented as following from that.

Its first recommendation is to give the agent a check it can run — a test suite, a build exit code, a
linter, a screenshot compared against a design — so that the loop closes without a human in it, and
it sets out four ways to bind that check with increasing firmness: asking for it in the prompt, making
it a session goal re-evaluated after every turn, enforcing it with a `Stop` hook, or having a separate
subagent try to refute the result. It also recommends asking for evidence rather than an assertion of
success, on the grounds that reviewing evidence is faster than re-running the verification.

Its second is to separate exploration and planning from implementation via plan mode, while cautioning
that planning adds overhead and should be skipped when the change could be described in one sentence.
For CLAUDE.md it recommends brevity over completeness, offering the test "would removing this cause
Claude to make mistakes?" and warning that a bloated file causes actual instructions to be ignored —
with the practical diagnostic that an instruction repeatedly skipped is usually a sign the file is too
long rather than that the rule needs restating. It names five recurring failure patterns: mixing
unrelated tasks in one session, correcting repeatedly instead of restarting with a better prompt, an
over-specified CLAUDE.md, trusting plausible-looking output without verification, and unscoped
investigation that fills the context. The documentation closes by presenting all of this as starting
points rather than rules, and advises developing intuition about when each does not apply.

## Adoption & Ecosystem

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes Claude Code's architecture as having shifted from a monolithic agent to a multi-agent one, spawning specialized sub-agents for specific tasks. The same paper cites it as an example of a powerful command-line agentic platform that grants developers immense control and flexibility but results in ephemeral interactions: the conversational context of planning, clarification, and refinement between the human and the agent exists only in a terminal's scroll-back buffer, with no systematic archival of the agent's reasoning or the human's guidance, making it difficult to reconstruct the evolution of design decisions or reproduce specific outcomes.
