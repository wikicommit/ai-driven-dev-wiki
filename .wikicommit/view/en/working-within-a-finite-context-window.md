---
title: "Working within a finite context window"
lang: en
kind: landscape
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/context-engineering.md
    source_commit: d5488c1df4d0cbce781137bbb410c0d112fd8758
  - path: .wikicommit/entity/en/DefinedTerm/attention-budget.md
    source_commit: d6b740fcefb776ad598c9c610d08c7220255d861
  - path: .wikicommit/entity/en/DefinedTerm/context-rot.md
    source_commit: 136844949634913857d6d1eb26ef9cb9cfaf8876
  - path: .wikicommit/entity/en/DefinedTerm/context-as-a-tool.md
    source_commit: 48d80cbbb1b1176580f1d3e42bed65bbe89633ce
  - path: .wikicommit/entity/en/DefinedTerm/ralph-loop.md
    source_commit: 7567a177e4f0172fd7847cc2fe9a076543e5ad54
  - path: .wikicommit/entity/en/DefinedTerm/long-running-agent.md
    source_commit: d3a6cc04042ea62012d6cdb8d9075c83b708d517
  - path: .wikicommit/entity/en/DefinedTerm/externalization.md
    source_commit: 2b5f014fc7cc03f207d83ea499c4a231c110d0fe
  - path: .wikicommit/entity/en/DefinedTerm/token-caching.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/ai-ide-rules.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/harness-engineering.md
    source_commit: c6b8c68a8b3e34ab51b855aeb44d0daa53497505
  - path: .wikicommit/entity/en/DefinedTerm/agent-skills.md
    source_commit: 10e9746c9bd7c8cfc2db7e41ba9601f191b8bb0f
  - path: .wikicommit/entity/en/BlogPosting/effective-context-engineering-for-ai-agents.md
    source_commit: d6b740fcefb776ad598c9c610d08c7220255d861
  - path: .wikicommit/entity/en/BlogPosting/context-engineering-for-agents.md
    source_commit: 918f7af409eaecc35e50dea8e21fc3277faf15bf
  - path: .wikicommit/entity/en/BlogPosting/langchain-context-engineering.md
    source_commit: 2dde03e70d40180419b38bfd339ee1be7c0efcfa
  - path: .wikicommit/entity/en/BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes.md
    source_commit: 02f7d23719e4ec300fc997d58e966c19037dfd22
  - path: .wikicommit/entity/en/BlogPosting/what-is-harness-engineering.md
    source_commit: f1038a285945837f7d6e6669210e65fb6f31011a
  - path: .wikicommit/entity/en/ScholarlyArticle/externalization-in-llm-agents.md
    source_commit: 2b5f014fc7cc03f207d83ea499c4a231c110d0fe
  - path: .wikicommit/entity/en/ScholarlyArticle/dive-into-claude-code.md
    source_commit: 85965d4810db6ca0ab5d75ba68b7a03eeaa9f1ea
  - path: .wikicommit/entity/en/ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/ScholarlyArticle/deepcode-open-agentic-coding.md
    source_commit: fb81a1a633a4538dec7293228db126d1e781d8ff
  - path: .wikicommit/entity/en/SoftwareApplication/claude-code.md
    source_commit: f06be6ff6feaf095ffb8e7a4ce28dc6471758c20
---

The pages this wiki holds on agents and their context share one premise: that the context available to a language model during inference is a finite resource with diminishing marginal returns, rather than a container to be filled. This page is a way into that group — where the area starts, why the constraint is held to exist, what fills the window, what is done within a session and across sessions when a task outruns it, and where the accounts it rests on come from.

## Where the area starts

[[DefinedTerm/context-engineering]] is the entry point. It names the practice of curating and dynamically managing what information occupies a model's context window during inference, and it is the page that gathers the differing accounts of the practice side by side — including how each positions it against [[DefinedTerm/prompt-engineering]]: as its natural progression, as fundamentally different from it, or as containing it as a subset. Its "When It Applies" section states the premise this area rests on: the practice assumes context is a finite resource with diminishing marginal returns, grounded in context rot and the attention-budget framing rather than in any particular window size.

## Why the window is treated as scarce

The case for the constraint is carried by an empirical page and an explanatory one.

- [[DefinedTerm/context-rot]] is the empirical side: a model's ability to recall information from its context declines as the number of tokens grows. Anthropic attributes the concept to needle-in-a-haystack style benchmarking and describes the effect as a performance gradient rather than a hard cliff.
- [[DefinedTerm/attention-budget]] is the explanatory side: Anthropic's framing of attention as a finite pool that every additional token depletes, which it traces to the pairwise relationships transformer attention creates between tokens, to training distributions in which shorter sequences are more common, and to the accuracy cost of techniques for extending context length.

[[ScholarlyArticle/externalization-in-llm-agents]] adds a second reason alongside uneven attention: context is ephemeral, so unless state is externalized elsewhere, every new session begins with partial amnesia. [[DefinedTerm/long-running-agent]] names finite context, no persistent state and no self-verification together as the obstacles that stop ordinary agent designs working over hours or days.

### Larger windows as an answer

Several pages record the position that a larger window does not remove the problem, each on its own grounds. [[DefinedTerm/context-rot]] and [[DefinedTerm/context-engineering]] carry Anthropic's argument that windows of all sizes remain subject to context pollution and information-relevance concerns. [[ScholarlyArticle/externalization-in-llm-agents]] argues that expanding windows does not dissolve the underlying tension, citing the "lost in the middle" finding. [[DefinedTerm/long-running-agent]] notes that even a large window fills, and that context rot degrades performance before the hard limit is reached. In [[BlogPosting/what-is-harness-engineering]], the author argues that a larger window would not have fixed a drifting slide deck, because the problem lay in how the task was organized. [[DefinedTerm/token-caching]] adds a cost angle: a very large window is not free even at the same per-token price, because the cost of a cache miss scales with context length.

## What fills the window

A group of pages is about what occupies context before or alongside the work itself.

- **Standing instructions.** [[DefinedTerm/ai-ide-rules]] and the study behind it, [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]], recommend not spending limited context window on formatting and syntax that linters enforce more reliably, and report compliance with a rule declining after the commit that introduces it, which the study attributes partly to growing context-window complexity. [[SoftwareApplication/claude-code]] records Anthropic's advice to keep CLAUDE.md brief, warning that a bloated file causes actual instructions to be ignored.
- **Capabilities loaded on demand.** [[DefinedTerm/agent-skills]] describes [[DefinedTerm/progressive-disclosure]]: a skill's metadata is always loaded, its body when triggered, and bundled resources only when read, and bundled scripts run so that only their output enters context. [[BlogPosting/what-is-harness-engineering]] reports its author measuring how much context each accumulated skill takes when loaded — context consumed before any work begins. [[ScholarlyArticle/dive-into-claude-code]] orders Claude Code's extension mechanisms by what they cost in context.
- **Tool and test output.** [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] designed its test output around context window pollution: print a few lines, log the rest to files, and put each error and its reason on one line for grep.

[[ScholarlyArticle/externalization-in-llm-agents]], relayed on [[DefinedTerm/harness-engineering]], treats this competition as a harness-level coordination problem: memory retrieval, skill loading, protocol schemas, tool descriptions and the model's own reasoning traces all draw on the same finite allocation, and the right split depends on the phase of execution.

## What is done within a session

Anthropic's post, [[BlogPosting/effective-context-engineering-for-ai-agents]], organises its responses to the constraint around a guiding principle — find the smallest possible set of high-signal tokens — applied to system prompts, tools and examples. It then turns to retrieval, describing a move toward [[DefinedTerm/just-in-time-context-retrieval]], and to three techniques for tasks that outrun the window: [[DefinedTerm/compaction]], [[DefinedTerm/structured-note-taking]] and [[DefinedTerm/sub-agent-architecture]], each suited to a different task shape.

Lance Martin's [[BlogPosting/context-engineering-for-agents]] and LangChain's [[BlogPosting/langchain-context-engineering]] group the strategies seen across popular agents into four buckets — write, select, compress and isolate — starting from the framing of the model as a CPU and its context window as RAM. The LangChain post additionally maps each bucket to features of its own [[SoftwareApplication/langgraph]], which that page marks as vendor guidance.

Two pages describe one production agent's handling of context from different angles. [[SoftwareApplication/claude-code]] records the documented behaviour — older tool outputs cleared first and the conversation summarised if needed, with `/clear` and `/compact` as session controls. [[ScholarlyArticle/dive-into-claude-code]] reads the source code and identifies the context window as the binding resource constraint, managed by a sequence of shapers that run before every model call and escalate only when cheaper strategies prove insufficient.

Isolation recurs as its own response. [[ScholarlyArticle/dive-into-claude-code]] describes subagents running in isolated context windows and returning only summary text to the parent. [[BlogPosting/what-is-harness-engineering]] reports giving each unit of work to an independent agent with the full design rules, and states the author's resulting view that an agent's core value is context isolation rather than parallelism.

[[DefinedTerm/context-as-a-tool]] takes a different route: it makes context maintenance a callable tool within the agent's own decision-making, so that the agent compresses its history at milestones rather than relying on append-only context or passively triggered compression.

## What is done across sessions

Where a task runs longer than one window can hold, the pages describe moving state out of the window and starting fresh.

- [[DefinedTerm/long-running-agent]] records Anthropic's account that what a fresh context window needs most is a fast way to understand the state of the work, supplied by a progress file alongside the git history.
- [[DefinedTerm/ralph-loop]] resets the agent's context at every iteration of a pick–implement–validate–commit cycle, carrying state across resets on the filesystem instead of in the window.
- [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] had each agent start in a fresh container with no context, and instructed the agents to maintain extensive READMEs and progress files.
- [[DefinedTerm/externalization]] frames memory as externalizing state across time, rather than treating the context window as the sole carrier of history.
- [[ScholarlyArticle/deepcode-open-agentic-coding]] frames its whole problem as information overload against a finite context window, and compares a stateful summary-based memory of generated files against a naive sliding-window eviction baseline that lost foundational definitions to truncation.

## Where the accounts come from

Most of what this area records is practitioners describing their own practice rather than measuring it. [[DefinedTerm/context-engineering]] states that none of its accounts is an independent evaluation. [[BlogPosting/effective-context-engineering-for-ai-agents]] is written by [[Organization/anthropic]]'s Applied AI team from its own engineering experience, and presents itself as a mental model rather than a set of benchmarks. The two write–select–compress–isolate posts present their buckets as a grouping of patterns already in use. [[BlogPosting/what-is-harness-engineering]] and [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] are first-hand accounts, and [[DefinedTerm/ralph-loop]]'s reported limits come from Geoffrey Huntley's own experience with the technique.

Measured results appear in a few places, each with its own scope: [[DefinedTerm/context-as-a-tool]] and [[ScholarlyArticle/deepcode-open-agentic-coding]] each report a single paper's benchmark results, and [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] is a mixed-methods study of rule files. [[ScholarlyArticle/externalization-in-llm-agents]] is a synthesis rather than a measured result, and [[ScholarlyArticle/dive-into-claude-code]] reads one static snapshot of source code, grading its own claims by evidence tier.

## Related pages

[[DefinedTerm/context-poisoning]], [[DefinedTerm/context-confusion]], [[DefinedTerm/tool-call-offloading]], [[DefinedTerm/context-reset]], [[DefinedTerm/initializer-agent]], [[DefinedTerm/agent-harness]]
