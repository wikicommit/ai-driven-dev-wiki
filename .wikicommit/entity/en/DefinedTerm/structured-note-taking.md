---
title: "Structured note-taking"
type: "schema:DefinedTerm"
lang: en
aliases: ["Agentic memory"]
tags: [agents, context-window, long-horizon-tasks, memory]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://platform.claude.com/cookbook/tool-use-context-engineering-context-engineering-tools'
    hash: sha256:ff18c6ce4f289fc1d0603542473d89de2170efe173360a83c70d460ec9204888
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A technique in which an agent regularly writes notes that persist outside its context window and are pulled back in at later times, also called agentic memory."
---

Structured note-taking, also called agentic memory, is a technique in which an agent regularly
writes notes that are persisted to memory outside of the context window and pulled back into it at
later times. Anthropic presents it as providing persistent memory with minimal overhead: the
pattern lets an agent track progress across complex tasks and hold on to critical context and
dependencies that would otherwise be lost across dozens of tool calls.

## Usage
Anthropic gives two shapes for the pattern: [[SoftwareApplication/claude-code]] creating a to-do
list, and a custom agent maintaining a NOTES.md file. It also points to Claude playing Pokémon as
a demonstration of the technique outside coding domains, where the agent maintains precise tallies
across thousands of game steps — tracking, for example, how many steps it has spent training in
one area and how many levels that has gained toward a target. Anthropic reports that without any
prompting about memory structure the agent develops maps of the regions it has explored, remembers
which key achievements it has unlocked, and maintains strategic notes on which attacks work best
against different opponents. After context resets it reads its own notes and continues multi-hour
training sequences or dungeon explorations, which Anthropic describes as enabling long-horizon
strategies that would be impossible while keeping all the information in the context window
alone.

Anthropic has also released a memory tool in public beta on the Claude Developer Platform, which
stores and consults information outside the context window through a file-based system. It says
this lets agents build up knowledge bases over time, maintain project state across sessions, and
reference previous work without keeping everything in context.

A later Claude Cookbook notebook,
[[TechArticle/context-engineering-memory-compaction-and-tool-clearing]], treats memory in this sense
as the primitive for *just-in-time* retrieval (see [[DefinedTerm/just-in-time-context-retrieval]]):
rather than loading everything up front, the agent stores what it learns and pulls it back on demand.
It presents the memory tool as `memory_20250818`, a client-side tool — the model issues memory
operations (view, create, str_replace, insert, delete, rename) and the application executes them
against storage it implements and controls — and says the API auto-injects a system prompt telling the
model to check its memory directory before doing anything else and to assume its context may be reset at
any moment. In the notebook's demonstration, a second session given the first session's saved memory
files opened by reading them and built on them, while the same follow-up task with an empty memory
directory had to go back to the source documents to rediscover the same facts.

The notebook also relays several ways to shape what gets saved: a system-prompt instruction limiting
memory to a given topic; asking the model to keep its memory folder up to date, coherent and organized
rather than accumulating new files; running a dedicated first session that sets up memory artifacts
such as a progress log and a feature checklist for later sessions to read; and client-side storage
hygiene — capping file sizes, clearing out files not accessed for a long time, and guarding against path
traversal.

## When It Applies
- Applies to long-horizon work with clear milestones. Anthropic says note-taking excels for
  iterative development, in contrast to [[DefinedTerm/compaction]], which it recommends for tasks
  requiring extensive back-and-forth.
- Assumes a persistence location outside the context window and a mechanism for reading the notes
  back in — a file the agent writes and re-reads, or a platform memory tool.
- The Claude Cookbook notebook scopes the memory tool to the *cross-session* problem: it gives lossless
  fidelity on whatever the agent chose to save, but does nothing about context growth within a session
  and adds tool-call overhead for every read and write. It suggests skipping memory where every session
  should start fresh, such as a chatbot whose conversations should be independent, and flags stale
  memory when facts change, and a data policy for personal or sensitive information when the agent learns
  user preferences, as things to watch.
- Established as Anthropic's own practice, evidenced by Claude Code's to-do list, the Claude
  playing Pokémon demonstration, and a memory tool in public beta. The Pokémon account is a
  demonstration Anthropic reports rather than a controlled measurement.

## Related Terms
- [[DefinedTerm/compaction]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/tool-result-clearing]]
- [[DefinedTerm/just-in-time-context-retrieval]]
