---
title: "Compaction"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, long-horizon-tasks]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
  - type: url
    url: 'https://www.anthropic.com/engineering/harness-design-long-running-apps'
    hash: sha256:47a08ad7125c953a6a359d169a11e61245c1d5329e47cb7057f496aaaef42b2a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The practice of summarising a conversation that is nearing the context window limit and reinitiating a new context window with that summary."
---

Compaction is the practice of taking a conversation nearing the context window limit, summarising
its contents, and reinitiating a new context window with the summary. Anthropic describes it as
typically the first lever in [[DefinedTerm/context-engineering]] for driving better long-term
coherence: at its core it distils the contents of a context window in a high-fidelity manner,
enabling an agent to continue with minimal performance degradation.

## Usage

In [[SoftwareApplication/claude-code]], Anthropic implements compaction by passing the message
history to the model to summarise and compress the most critical details. The model preserves
architectural decisions, unresolved bugs and implementation details while discarding redundant
tool outputs or messages; the agent then continues with that compressed context plus the five most
recently accessed files, so users get continuity without having to worry about context window
limitations.

Anthropic identifies clearing tool calls and results as low-hanging superfluous content — once a
tool has been called deep in the message history, the raw result generally need not be seen again
— and calls tool result clearing one of the safest, lightest-touch forms of compaction. It
describes this as having launched as a feature on the Claude Developer Platform.

A summarising pass is not always a single step. [[ScholarlyArticle/dive-into-claude-code]], reading
Claude Code's source at v2.1.88, describes compaction there as a pipeline of five shapers that run
in sequence before every model call, each more aggressive than the last: a per-tool-result budget
that replaces oversized outputs with content references, a lightweight trim of older history
segments, a fine-grained cache-aware compression, a read-time projection that presents a collapsed
view while leaving the stored history intact, and finally a full model-generated summary that fires
only when the context still exceeds the pressure threshold after the other four have run. The
authors describe this as a lazy-degradation principle — apply the least disruptive compression
first, escalate only when cheaper strategies prove insufficient — and note that the compaction
output is appended rather than written over prior transcript lines, so earlier content remains
available for reconstruction.

That same study is explicit about what the graduated design costs. Five interacting layers, several
gated by feature flags, produce behaviour users find difficult to predict, and the compression is
largely invisible: a user has no easy way to inspect what a budget replacement, a trim or a collapse
removed, and cache-aware behaviour makes compression decisions depend on prompt caching in ways not
surfaced to them. The authors also relay external work reporting two further costs of
summary-based compaction — that the summarisation step is a blocking inference stall, and that it is
non-deterministic, with retained content fluctuating across runs on identical inputs. They contrast
the whole approach with simpler alternatives, single-pass truncation or one summarisation step,
which sacrifice information but are easier to reason about.

## When It Applies

- Applies to long-horizon tasks where the token count exceeds the context window, and
  particularly to work requiring extensive back-and-forth; Anthropic says compaction maintains
  conversational flow for such tasks, in contrast to note-taking, which it says excels for
  iterative development with clear milestones.
- Assumes the message history can be summarised by a model, and that the compaction prompt has
  been tuned for the traces in question. Anthropic recommends carefully tuning that prompt on
  complex agent traces: first maximise recall so it captures every relevant piece of information
  from the trace, then iterate to improve precision by eliminating superfluous content.
- Fails when applied too aggressively. Anthropic says the art of compaction lies in selecting what
  to keep versus what to discard, and that overly aggressive compaction can lose subtle but
  critical context whose importance only becomes apparent later.
- Established as Anthropic's own implemented practice in Claude Code and as a shipped platform
  feature, described from its engineering experience rather than as a measured result. The
  five-layer account above rests on one study's reading of a single version's source, whose authors
  caution that feature flags make builds differ.
- A post on long-running agents describes Anthropic as explicit that summarization-as-compaction is
  not sufficient on its own for very long jobs: beyond ordinary compaction, Anthropic's harnesses
  also perform full context resets, where the harness tears a session down and rebuilds it from a
  structured handoff file — described as essentially how a human onboards a new engineer.
- Anthropic states the same limitation firsthand in
  [[BlogPosting/effective-harnesses-for-long-running-agents]], and names the mechanism behind it:
  compaction *doesn't always pass perfectly clear instructions to the next agent*. Its reported
  evidence is that a frontier model running on the [[SoftwareApplication/claude-agent-sdk]] in a loop
  across multiple context windows, with compaction available, still fell short of building a
  production-quality web app from a high-level prompt — and that the resulting half-implemented,
  undocumented features left the next session guessing at what had happened. The remedy it describes
  is not better compaction but durable artifacts outside the context window: a progress log, a git
  history, and a structured feature list (see [[DefinedTerm/initializer-agent]]).

- A later Anthropic engineering post,
  [[BlogPosting/harness-design-for-long-running-application-development]], draws the boundary between
  compaction and a full [[DefinedTerm/context-reset]] in terms of what each buys. Compaction summarises
  earlier parts of the conversation in place so the same agent can keep going on a shortened history,
  which preserves continuity but does not give the agent a clean slate; a reset clears the window
  entirely and starts a fresh agent, at the cost of the handoff artifact having to carry enough state
  for the work to be picked up cleanly.
- That distinction is load-bearing for one failure mode in particular. The same post reports that
  because compaction leaves the same agent running, [[DefinedTerm/context-anxiety]] — wrapping up work
  prematurely on approaching what the model believes is its context limit — can persist through it. It
  states that Claude Sonnet 4.5 exhibited this strongly enough that compaction alone was not sufficient
  for strong long-task performance, which made context resets essential to that harness's design, and
  that Claude Opus 4.5 largely removed the behaviour on its own, allowing a later harness to drop resets
  entirely and run as one continuous session with the
  [[SoftwareApplication/claude-agent-sdk]]'s automatic compaction handling context growth. Compaction's
  sufficiency is therefore reported as depending on the model, not on the technique alone.

## Related Terms

- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/long-running-agent]]
- [[DefinedTerm/context-reset]]
- [[DefinedTerm/context-anxiety]]
