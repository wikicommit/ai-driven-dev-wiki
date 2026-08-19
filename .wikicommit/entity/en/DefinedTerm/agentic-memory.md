---
title: "agentic memory"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Writing information to storage outside the context window and reading it back later — covering both within-task scratchpads and memories that persist across sessions — so an agent's continuity does not depend on everything staying in context."
  termCode: ""
  inDefinedTermSet: ""
---

Agentic memory is the practice of writing information to storage outside the context window and reading it back later, so that an agent's continuity does not depend on everything remaining in context. [[TechArticle/effective-context-engineering-for-ai-agents]] uses the term interchangeably with **structured note-taking**, defining it as a technique where the agent regularly writes notes persisted to memory outside the context window, which are pulled back in at later times. [[BlogPosting/context-engineering]] splits the same idea across two of its four buckets: *writing* context is saving it outside the window, and *selecting* context is pulling the right part of it back in.

## Usage

[[BlogPosting/context-engineering]] organises the idea by scope. In its account, **scratchpads** persist information while an agent works on a single task, and can be implemented either as a tool that writes to a file or as a field in a runtime state object that persists during the session — the difference determining how the agent reads them back, by tool call or by the developer choosing which parts of state to expose at each step. **Memories**, in the same account, persist across many sessions. That post traces the idea to Reflexion, which introduced reflecting after each agent turn and reusing the self-generated memories, and to Generative Agents, which synthesised memories periodically from collections of past feedback, and observes that ChatGPT, Cursor, and Windsurf all ship mechanisms to auto-generate long-term memories from user interactions.

Anthropic's account emphasises the payoff for long-horizon work: the pattern provides persistent memory with minimal overhead, letting an agent track progress across complex tasks and maintain critical context and dependencies that would otherwise be lost across dozens of tool calls. Its examples are Claude Code creating a to-do list and a custom agent maintaining a `NOTES.md` file. Its most striking illustration is outside coding — Claude playing Pokémon, where the agent maintains precise tallies across thousands of game steps, develops maps of explored regions, remembers unlocked achievements, and keeps strategic notes on which attacks work against which opponents, all without being prompted about memory structure. After context resets it reads its own notes and continues multi-hour sequences, which the post presents as coherence across summarization steps enabling strategies impossible from context alone.

Selection is the harder half. LangChain's post distinguishes episodic memories (few-shot examples of desired behaviour), procedural memories (instructions that steer behaviour), and semantic memories (task-relevant facts), and notes that many code agents sidestep selection entirely by always pulling in a narrow fixed set of files — `CLAUDE.md` for Claude Code, rules files for Cursor and Windsurf. Where a larger collection is stored, embeddings and knowledge graphs are commonly used for indexing, and the post concedes selection remains challenging: it relays Simon Willison's example of ChatGPT retrieving his location from memory and unexpectedly injecting it into a requested image, and observes this kind of unwanted retrieval can leave users feeling the context window "no longer belongs to them."

## Related Terms

Agentic memory is one of three standard techniques for long-horizon tasks, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/multi-agent-orchestration]]; Anthropic matches it specifically to iterative development with clear milestones. The always-loaded files that serve as its simplest form are covered under [[DefinedTerm/context-files]], and the surrounding discipline under [[DefinedTerm/context-engineering]]. [[SoftwareApplication/langgraph]] implements both scopes explicitly through checkpointed short-term state and a long-term memory store.
