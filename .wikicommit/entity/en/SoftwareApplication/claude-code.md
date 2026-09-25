---
title: "Claude Code"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, anthropic, coding-tools, context-window, agent-architecture, agent-safety]
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
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
  - type: url
    url: 'https://baoyu.io/blog/2026-04-06/claude-code-token-optimization'
    hash: sha256:287e81a37d9c6dc213f594b3dd3f401600e6fe71f7d49622f3492c33f13b0a75
  - type: url
    url: 'https://www.anthropic.com/engineering/april-23-postmortem'
    hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
  - type: url
    url: 'https://code.claude.com/docs/en/how-claude-code-works'
    hash: sha256:bd22d00c3d6884ed8323b1d1a90abe77a12c9df0272a5a855041afec603c6196
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Anthropic's agentic coding solution, an assistant that runs in the terminal and works through a loop of gathering context, taking action and verifying results. It combines up-front context files with just-in-time file and data retrieval, message-history compaction, and to-do list note-taking."
  applicationCategory: "Agentic coding tool"
  featureList: "Targeted database queries with stored results; Bash primitives including head, tail, glob and grep; CLAUDE.md context files loaded up front; message-history compaction; a to-do list for agentic note-taking; local, cloud and Remote Control execution environments; resumable and forkable sessions; file-edit checkpoints; permission modes"
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

Anthropic's documentation describes Claude Code as an agentic assistant that runs in the terminal and
that, while it excels at coding, can help with anything done from the command line. Given a task, it
works through three phases — **gather context**, **take action** and **verify results** — which the
documentation says blend together, with Claude choosing each step from what it learned in the previous
one and the user able to interrupt and steer at any point. The loop is powered by two components,
models that reason and tools that act, and the documentation names Claude Code itself as the layer
around the model that provides the tools and manages the context the model sees — the layer it says
the term agentic harness refers to (see [[DefinedTerm/agent-harness]]). It groups the built-in tools
into five categories: file operations, search, execution, web, and code intelligence (the last
requiring code intelligence plugins), alongside tools for spawning subagents and asking the user
questions.

On that account, running `claude` in a directory gives it access to the project's files, the
terminal, the current git state, [[DefinedTerm/claude-md]] (and an AGENTS.md written for other coding
agents, which it can read on its own or alongside CLAUDE.md), and an auto memory in which it saves
learnings as it works, of which the first 200 lines or 25KB of `MEMORY.md` load at the start of each
session. The same loop runs in three execution environments — locally, in the cloud on
Anthropic-managed VMs or self-hosted environments, and under Remote Control, where a browser drives a
session whose execution and files stay on the user's machine — and behind several interfaces,
including the terminal, a desktop app, IDE extensions, the web, Slack and CI/CD pipelines.

Each session is written locally as a plaintext JSONL file under `~/.claude/projects/`, and sessions are
independent: a new one starts with a fresh context window. Resuming with `--continue` or `--resume`
reopens a session under the same ID, while forking with `--fork-session` or `/branch` copies its
history into a new one. As context fills, the documentation says Claude Code first clears older tool
outputs and then summarises the conversation if needed, and that it stops auto-compacting and shows an
error after a few attempts when a single oversized file or output refills the context each time. MCP
tool definitions are deferred by default and loaded on demand via tool search. Two safety mechanisms
are named: checkpoints, which snapshot a file before Claude edits it and are rewound by pressing `Esc`
twice, and which cannot cover actions on remote systems such as databases, APIs or deployments; and
[[DefinedTerm/permission-modes]], cycled with `Shift+Tab`, of which the documentation lists Auto,
Manual, Accept edits and Plan.

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

## Architecture

[[ScholarlyArticle/dive-into-claude-code]] describes the system from its publicly available
TypeScript source, at version 2.1.88, and its summary of the shape is that the core is a simple
while-loop that calls the model, runs tools and repeats, while most of the code lives in the
systems around that loop. Everything in this section is that study's reading of the code it
examined at that version, not documented behaviour Anthropic states.

It presents the system as seven components — user, interfaces, agent loop, permission system,
tools, state and persistence, and execution environment — and then as five layers: surface, core,
safety/action, state and backend. All four surfaces it names — interactive CLI, headless CLI,
Agent SDK and IDE/desktop/browser — are reported to feed the same loop.

Safety is described as seven independent layers, any one of which can block a request: blanket-
denied tools removed from the model's view before it can attempt them; deny-first rule evaluation
in which deny rules take precedence over allow rules even when the allow rule is more specific;
the active permission mode (see [[DefinedTerm/permission-modes]]) setting the baseline for
requests that match no rule; an ML-based auto-mode classifier that can deny what the rule system would allow;
shell sandboxing that restricts filesystem and network access independently of the permission
system; not restoring session-scoped permissions on resume or fork; and hook-based interception.
The study counts up to seven permission modes, up to 54 built-in tools of which 19 are
unconditional and 35 conditional on feature flags and user type, and a hook pipeline spanning 27
event types of which 5 are safety-related and 22 serve lifecycle and orchestration purposes.

Context pressure is handled by a pipeline of five sequential shapers that run before every model
call — budget reduction, snip, microcompact, context collapse and auto-compact. Delegation runs
through the same tool factory as everything else: the agent tool re-enters the loop with an
isolated context window and returns only a summary to the parent, which the study lists alongside
lazy CLAUDE.md loading, deferred tool schemas and a per-tool-result budget as decisions following
from treating context as the binding constraint.

Persistence is three independent channels: mostly append-only JSONL session transcripts, one file
per session at a project-specific path; a global prompt history file holding user prompts only;
and separate sidechain files for each subagent's conversation. The study reads the append-only
JSONL format as a deliberate choice favouring auditability and simplicity over query power, since
every logged event is human-readable, version-controllable and inspectable without specialized
tooling, where a database-backed store would allow richer queries at the cost of deployment
dependencies and transparency. It also notes that what Claude Code calls checkpoints are
file-history snapshots for reverting filesystem changes rather than a generic checkpoint store,
and that resume and fork deliberately do not restore session-scoped permissions, treating sessions
as isolated trust domains so that stale trust decisions are not carried into a changed context.

The study frames all of this as following from five human values it attributes to the design —
human decision authority, safety/security/privacy, reliable execution, capability amplification
and contextual adaptability — traced through thirteen design principles to specific implementation
choices. Its own closing concern is that while the system amplifies the short-term capabilities of
programmers and end users, it offers limited mechanisms that explicitly support long-term human
improvement, deeper understanding and sustained codebase coherence.

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
with the practical diagnostic that if Claude keeps doing something despite a rule against it, the file
is probably too long and the rule is getting lost; for a single instruction Claude keeps skipping, it
suggests adding emphasis to that line alone, since emphasising many lines makes none stand out. It names five recurring failure patterns: mixing
unrelated tasks in one session, correcting repeatedly instead of restarting with a better prompt, an
over-specified CLAUDE.md, trusting plausible-looking output without verification, and unscoped
investigation that fills the context. The documentation closes by presenting all of this as starting
points rather than rules, and advises developing intuition about when each does not apply.

### Session and context configuration

[[BlogPosting/claude-code-token-saving-guide]] describes a second set of practices, organised not
around what the agent should be asked to do but around how a session's input is assembled and
billed. Its starting point is that a session carries a large unchanging prefix — system
instructions, tool definitions, CLAUDE.md and project configuration, which that post puts at
roughly 50,000 tokens — and that [[DefinedTerm/token-caching]] covers it only while the session
stays active. That post reports a one-hour cache window for the main agent against five minutes
for a subagent, and that caches are held separately per model, so switching model mid-session
rebuilds from nothing.

Several controls follow from that. The post reports two environment settings in
`~/.claude/settings.json`, `CLAUDE_CODE_DISABLE_1M_CONTEXT` to turn the 1M context window off and
`CLAUDE_CODE_AUTO_COMPACT_WINDOW` to set the threshold at which the session compacts, and
recommends keeping the larger window while compacting conservatively rather than choosing between
them. Separately, at the project level rather than the user-global one, it reports `permissions.deny`
in `.claude/settings.json` as a way to keep whole paths — `node_modules`, build output, large data
files — out of file discovery, search results and direct reads, on the grounds that an agent will
otherwise spend turns re-reading irrelevant files even when given an explicit path. Two smaller mechanics it records: HTML comments in CLAUDE.md are stripped before the
file is injected, so maintainer notes cost nothing, and skills load when invoked rather than being
held in context, which is why it recommends moving situational instructions out of CLAUDE.md and
into them — with the caveat, which it states in the same breath, that more skills is not better,
since loading many skills and agents is itself a hidden drain.

These are a practitioner's account relaying vendor statements and community reports rather than
documentation, and the post itself notes that the consumption behaviour prompting the advice was
still under investigation at the time of writing.

### Effort defaults and their revision

[[BlogPosting/update-on-recent-claude-code-quality-reports]] describes how
[[DefinedTerm/reasoning-effort]] is set here: effort levels are calibrated per model as points
along the test-time-compute curve, the product layer picks one of them as its default and sends it
to the Messages API as the effort parameter, and `/effort` exposes the rest. That post is
Anthropic's postmortem on a month of reports that Claude had got worse, which it traces to three
unrelated changes rather than one regression, all resolved as of April 20, 2026 in version 2.1.116.
The three are stated as having affected Claude Code, the Claude Agent SDK and Claude Cowork, with
the API unaffected; what follows is the part of that account that bears on Claude Code.

The effort default is the first of the three. It was lowered from `high` to `medium` on March 4,
2026 to address occasional thinking times long enough to make the interface appear frozen, and
reverted on April 7 after user feedback, with defaults now stated as `xhigh` for Opus 4.7
and `high` for every other model. Anthropic reports having first tried notices, an inline effort
selector and the reinstatement of ultrathink, and that most users stayed on the default anyway.

The second is a defect Anthropic places at the intersection of Claude Code's context management,
the Anthropic API and extended thinking. An optimization shipped on March 26 was meant to clear old thinking once from sessions idle for more than an hour, reducing the cost
of resuming them; the implementation instead cleared it on every turn for the rest of the session,
so the agent continued working with progressively less memory of why it had chosen what it had.
Anthropic reports this surfaced as forgetfulness, repetition and odd tool choices, that the
resulting cache misses are its best explanation for separate reports of usage limits draining
faster than expected, and that it was fixed on April 10 in version 2.1.101. Its own account of why
it took over a week to find is worth recording alongside the architecture above: the change passed
multiple human and automated code reviews, unit and end-to-end tests, automated verification and
dogfooding, and two unrelated changes made the issue hard to reproduce at first — an internal-only
server-side experiment on message queuing, and an orthogonal change in how thinking is displayed,
which Anthropic says suppressed the bug in most CLI sessions.

The third is a system prompt instruction limiting text between tool calls to 25 words and final
responses to 100, added on April 16 to curb Opus 4.7's verbosity. It cleared weeks of internal
testing before release; when more ablations were run during the investigation against a broader set
of evaluations, one of those evaluations showed a 3% drop for both Opus 4.6 and 4.7, and the
instruction was reverted on April 20. The
process commitments Anthropic attaches — a broad per-model eval suite for every system prompt
change, continued ablations, tooling to review and audit prompt changes, a CLAUDE.md rule gating
model-specific changes to the model they target, and soak periods with gradual rollouts for
anything that could trade against intelligence — are stated as applying to Claude Code's own
development.

## Adoption & Ecosystem

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes Claude Code's
architecture as having shifted from a monolithic agent to a multi-agent one, spawning specialized
sub-agents for specific tasks. The same paper cites it as an example of a powerful command-line
agentic platform that grants developers immense control and flexibility but results in ephemeral
interactions: on its account the conversational context of planning, clarification and refinement
between the human and the agent exists only in a terminal's scroll-back buffer, with no systematic
archival of the agent's reasoning or the human's guidance, making it, in the paper's words, nearly impossible to reconstruct the
evolution of design decisions or reproduce specific outcomes.

The two sources disagree here, and this page follows the source-level study. That paper mentions
Claude Code as one example among several platforms while arguing a broader point, whereas
[[ScholarlyArticle/dive-into-claude-code]] takes the system's own persistence design as one of its
subjects and documents the durable record described under Architecture above — session transcripts
written to disk as events occur, a global prompt history, and per-subagent sidechains. What that
study leaves open is not whether the archive exists but what sits between a static instruction
hierarchy and a single session's transcript: cross-session persistence is one of the six
directions for future work it identifies, and it names the question of durable state that is
neither a static instruction nor one session's transcript as unresolved.
