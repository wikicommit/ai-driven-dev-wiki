---
title: "Context Reset"
type: "schema:DefinedTerm"
lang: en
tags: [context-window, long-horizon-tasks, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/harness-design-long-running-apps'
    hash: sha256:47a08ad7125c953a6a359d169a11e61245c1d5329e47cb7057f496aaaef42b2a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Clearing an agent's context window entirely and starting a fresh agent, combined with a structured handoff carrying the previous agent's state and next steps. Distinguished from compaction, which shortens the history in place and leaves the same agent running."
---

A context reset is the practice of clearing the context window entirely and starting a fresh agent,
combined with a structured handoff that carries the previous agent's state and its next steps. It is
set out under that name in [[BlogPosting/harness-design-for-long-running-application-development]] as
one way of handling work that exceeds a single context window, presented in contrast with
[[DefinedTerm/compaction]]: an earlier harness relied on resets because compaction alone was not
sufficient, and a later one dropped resets entirely and left context growth to automatic compaction.

The defining contrast is with [[DefinedTerm/compaction]], which summarises earlier parts of the
conversation in place so the same agent can continue on a shortened history. On that post's account
compaction preserves continuity but does not give the agent a clean slate, whereas a reset does — at
the cost of requiring the handoff artifact to carry enough state for the next agent to pick the work
up cleanly. The two are therefore not interchangeable: which one a harness needs depends on whether
continuity or a clean slate is the thing being bought.

## Usage

The technique is applied where an agent must work coherently across multiple sessions. The post
describes an earlier harness in which an [[DefinedTerm/initializer-agent]] decomposed a product spec
into a task list and a coding agent implemented tasks one feature at a time, handing off artifacts to
carry context between sessions; resets between those sessions are described as a key unlock for
keeping the model on task.

Its stated costs are concrete: resets add orchestration complexity, token overhead and latency to each
harness run. The condition the post attaches is on the handoff artifact, which has to carry enough
state for the next agent to pick the work up cleanly.

## When It Applies

The post's stated reason for needing resets is [[DefinedTerm/context-anxiety]] — a model wrapping up
work prematurely as it approaches what it believes is its context limit — together with ordinary loss
of coherence as the window fills. Because compaction leaves the same agent running, the post argues it
does not clear the first of those, which is what makes a reset necessary rather than merely
preferable.

That reasoning also bounds when the technique applies. The post reports that Claude Sonnet 4.5
exhibited context anxiety strongly enough that compaction alone was insufficient, making resets
essential to that harness; and that Claude Opus 4.5 largely removed the behaviour on its own, so
resets were dropped from a later harness entirely and the agents run as one continuous session with
the [[SoftwareApplication/claude-agent-sdk]]'s automatic compaction handling context growth. The
technique is thus presented as a compensation for a specific model behaviour, and as something to
re-examine when a new model lands — an instance of the post's more general argument that every harness
component encodes an assumption about what the model cannot do on its own.

How well-established it is: this is one vendor's engineering account of its own harnesses, written by
a member of its Labs team, describing what worked across its experiments rather than reporting a
controlled comparison between reset-based and compaction-only harnesses.

## Related Terms

- [[DefinedTerm/compaction]] — the alternative this is defined against
- [[DefinedTerm/context-anxiety]] — the failure mode resets are introduced to address
- [[DefinedTerm/initializer-agent]] — the agent that decomposed the product spec into a task list in the earlier harness
- [[DefinedTerm/structured-note-taking]] — another technique for holding state outside the context window (this wiki's cross-reference, not this post's framing)
- [[DefinedTerm/harness-engineering]] — the discipline this technique belongs to
