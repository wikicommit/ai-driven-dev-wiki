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
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:2fa27ef4cd354e98bc9fd4d6cc5bec7f182d3b5a96745c6de6f694f18541f1a6
  - type: url
    url: 'https://arxiv.org/pdf/2510.04618'
    hash: sha256:6b917acfae2be76706c1360bd37b74776f6c979139cfb5a5604b5f0ed5f78951
  - type: url
    url: 'https://arxiv.org/pdf/2604.10352'
    hash: sha256:7a767caa51983f4f753aa5982e1e2dae9ca37450e66a43fe2e0d7b116d017c7f
review_status: pending
generated_at: "2026-08-21"
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

[[TechArticle/effective-harnesses-for-long-running-agents]] reports the same pattern used as the primary mechanism for continuity across sessions rather than as a supplement to context. In that harness, an initializer agent writes a progress file and an initial git commit, and every subsequent session begins by reading the git logs and the progress file to establish what was recently worked on, alongside a structured feature list from which it picks its next task. The post's own framing is that this is where the leverage lies: the key insight it reports was finding a way for agents to quickly understand the state of work when starting with a fresh context window, and it credits the design to observing what effective software engineers do every day.

That account also contributes an unusually concrete finding about the storage format. After some experimentation the authors settled on JSON for the feature list, because, in their words, "the model is less likely to inappropriately change or overwrite JSON files compared to Markdown files" — a durability property of the note itself, distinct from the selection problem above.

### Maintaining the note without destroying it

Writing a note outside the window raises a maintenance question the accounts above leave open: what happens when the note itself is updated. [[ScholarlyArticle/agentic-context-engineering]] reports that the obvious answer — ask the model to rewrite the accumulated note at each step — fails in a specific and severe way it calls [[DefinedTerm/context-collapse]]. In its AppWorld case study a context of 18,282 tokens at 66.7 accuracy collapsed at the next adaptation step to 122 tokens and 57.1 accuracy, below the 63.7 the same setup achieved with no accumulated context at all.

Its proposed alternative treats the note as an append-and-refine artifact rather than a document to regenerate. Three roles divide the work: a Generator produces reasoning trajectories, a Reflector distils lessons from their successes and errors, and a Curator emits compact delta entries that are merged deterministically into the existing context — so no step ever rewrites the whole, and multiple deltas can be merged in parallel. The paper reports average gains of 10.6% on agent benchmarks and 8.6% on domain-specific ones from this arrangement, built from execution feedback rather than labelled supervision. The evaluation is on agent and finance benchmarks rather than on coding tasks, and the measurements are the authors' own.

### From best-effort note-taking to an enforceable contract

[[ScholarlyArticle/clawvm]] accepts everything above as necessary and argues it is not sufficient. Its criticism of the existing building blocks — pruning, retrieval, compaction, pre-compaction memory flushes, external memory plugins — is that "these improve recall quality, but none provides an enforceable contract over residency, durability, or auditability," so in practice "flushes can still be bypassed, writeback can still be destructive, and no mechanism guarantees that critical state survives lifecycle transitions." Its evidence that this bites is three patterns it reports from public issue trackers and practitioner reports: rules and constraints lost after context summarization, state silently dropped on session reset, and persistence operations that overwrite rather than merge.

Its proposed abstraction borrows from operating systems rather than from note-taking. Agent state becomes **typed pages**, each of which can be held at full detail, compressed, reduced to structured fields, or shrunk to a pointer as token pressure rises, and each carrying a **minimum-fidelity invariant** stating how far it may degrade before space is reclaimed. The harness enforces those invariants at every lifecycle boundary with validated writeback — placed there, the paper argues, because the harness "already assembles prompts, mediates tools, and observes lifecycle events," which makes residency and durability deterministic and auditable rather than emergent.

The reported result is conditional and the condition is the interesting part: all policy-controllable faults are eliminated "whenever the minimum-fidelity set fits within the token budget," at a median of under 50 microseconds of policy-engine overhead per turn. Deciding what belongs in that set remains a human judgment; the mechanism enforces it rather than making it.

## Related Terms

Agentic memory is one of three standard techniques for long-horizon tasks, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/multi-agent-orchestration]]; Anthropic matches it specifically to iterative development with clear milestones. The always-loaded files that serve as its simplest form are covered under [[DefinedTerm/context-files]], and the surrounding discipline under [[DefinedTerm/context-engineering]]. [[SoftwareApplication/langgraph]] implements both scopes explicitly through checkpointed short-term state and a long-term memory store.
