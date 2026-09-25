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
  - type: url
    url: 'https://arxiv.org/pdf/2604.03515'
    hash: sha256:5afdaed7652dc3b8c3833fd90b9e8d54cd5d758f847d5d80b3aee353a3cb3acd
  - type: url
    url: 'https://arxiv.org/pdf/2606.30560'
    hash: sha256:90d9d93dde14b87925191228c1addb5b483ccd600b3080a99d134b04712cf1e3
  - type: url
    url: 'https://code.claude.com/docs/en/how-claude-code-works'
    hash: sha256:bd22d00c3d6884ed8323b1d1a90abe77a12c9df0272a5a855041afec603c6196
  - type: url
    url: 'https://platform.claude.com/cookbook/tool-use-context-engineering-context-engineering-tools'
    hash: sha256:ff18c6ce4f289fc1d0603542473d89de2170efe173360a83c70d460ec9204888
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

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

Claude Code's user documentation describes the same behaviour from the user's side. As the context
limit approaches, it says, Claude Code first clears older tool outputs and then summarises the
conversation if needed; the user's requests and key code snippets are preserved, while detailed
instructions from early in the conversation may be lost, which is why it advises putting persistent
rules in [[DefinedTerm/claude-md]] rather than relying on conversation history. What is kept can be
steered, by adding a "Compact Instructions" section to CLAUDE.md or by running `/compact` with a focus.
The documentation also records a failure case: if a single file or tool output is so large that the
context refills immediately after each summary, Claude Code stops auto-compacting after a few attempts
and shows an error instead of looping.

Anthropic's API offers compaction as a server-side feature, which
[[TechArticle/context-engineering-memory-compaction-and-tool-clearing]] walks through as the
`compact_20260112` context edit. It fires automatically at a token threshold (minimum 50K, default
150K), returns a typed compaction block that the application sends back in place of the earlier
conversation, and handles tool-use pairing across the summary boundary. The notebook stresses that
compaction is a *whole-transcript* operation — user and assistant messages, tool calls, tool results and
even earlier compaction blocks are all flattened into the summary — which is what distinguishes it from
[[DefinedTerm/tool-result-clearing]], a sub-transcript edit that drops only old tool results. Its custom
`instructions` parameter does not supplement the default summarisation prompt but replaces it entirely,
so a caller who supplies one takes on the full framing; the notebook's example names the specific
details its research agent needs preserved, such as every quantitative figure with its source and which
documents remain unread. Probing the summaries its agent produced, the notebook reports that high-level
facts central to the task tended to survive while obscure specifics, such as a single cell in an
appendix table, tended not to: compaction keeps the substance in compressed form but loses verbatim
detail.

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

How often compaction actually fires in everyday use has been measured from session logs.
[[ScholarlyArticle/tracelab]], analysing about 4,300 real sessions of
[[SoftwareApplication/claude-code]] and [[SoftwareApplication/openai-codex]], identifies a
compaction as a drop of at least 64K input tokens in one step, taken near the session's peak context
and followed by slow regrowth. By that definition it finds compaction "not rare but not dominant":
9.7% of sessions undergo at least one, and those that do average 3.7 compactions with a long tail.
It is overwhelmingly tool-initiated — occurring mid-loop rather than at a user's turn — and far more
common in Codex (18.4% of sessions) than in Claude Code (4.5%), which the authors relate to Codex's
shorter context length.

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

- The Claude Cookbook notebook on context-engineering primitives recommends compaction first where
  dialogue is the primary context, and over tool-result clearing where tool results cannot easily be
  re-fetched, such as ephemeral APIs or uploads; it suggests skipping compaction when sessions stay well
  under the context limit, since compaction is lossy and without the need for headroom one would be
  paying fidelity for nothing. It notes that compaction costs inference, because a model has to write the
  summary, and that it provides no persistence across sessions.

- Compaction is one design choice among several, and
  [[ScholarlyArticle/inside-the-scaffold]] counts it among the dimensions on which open-source coding
  agents diverge, alongside state management and multi-model routing — seven distinct strategies
  across the 13 scaffolds it analysed, from no management at all to compaction the model itself
  requests. It sorts these into two philosophies.
  *Prevention* agents bound context growth structurally, by scoping messages per unit of work,
  capping search rounds and truncating results, or limiting trajectory depth; *cure* agents let
  context grow and compress it when a token threshold is reached. Prevention avoids summarisation
  cost and information loss, but requires the scaffold to anticipate how context will grow.
- The strategies that paper distinguishes between those poles are rule-based truncation (keeping the
  first and last N observations and eliding the rest), structural isolation, token-based selective
  inclusion within a budget, scaffold-triggered model summarisation, summarisation followed by a
  verification turn that checks whether critical information was lost, and model-initiated
  compaction, where a tool lets the model decide when to compact rather than the scaffold. It
  observes that one agent avoids the problem altogether by making every model call single-turn with
  no conversation history, so that fitting the work into context becomes a prompt-construction
  problem rather than a runtime one.
- The same paper places compaction among its *diverging* dimensions rather than its converging ones,
  and reads that divergence as genuine uncertainty rather than noise: balancing information
  preservation against token cost has an optimum that depends on task length, model capability and
  cost tolerance, which it says no single strategy resolves.

## Related Terms

- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/long-running-agent]]
- [[DefinedTerm/context-reset]]
- [[DefinedTerm/context-anxiety]]
- [[DefinedTerm/agent-scaffold]]
- [[DefinedTerm/claude-md]]
- [[DefinedTerm/tool-result-clearing]]
