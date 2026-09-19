---
title: "Context Anxiety"
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
  description: "A failure mode in which a model begins wrapping up work prematurely as it approaches what it believes to be its context limit, rather than because the task is finished. Named in Anthropic's engineering writing on long-running harnesses, where it is given as the reason compaction alone was insufficient and context resets became necessary."
---

Context anxiety is the tendency of some models, on a lengthy task, to begin wrapping up their work
prematurely as they approach what they believe is their context limit. It is named as such in
[[BlogPosting/harness-design-for-long-running-application-development]]. It appears there alongside a
plainer problem with a filling context window — models losing coherence on lengthy tasks — as something
only some models exhibit. What distinguishes it is that the trigger is the model's own estimate of
remaining room rather than the state of the work: the task is wrapped up early because the model
believes it is running out of context, not because it is done.

## Usage

The term is used in harness design to explain why one context-management technique is chosen over
another. That post draws the distinction sharply against [[DefinedTerm/compaction]]: compacting
summarises earlier parts of the conversation in place so that the same agent continues on a
shortened history, which preserves continuity but does not give the agent a clean slate — and so, on
the post's account, context anxiety can persist through it. A full context reset, by contrast, clears
the window entirely and starts a fresh agent from a structured handoff, which the post presents as
addressing both of those context-window problems at once.

The concept is therefore load-bearing in an architectural argument rather than purely descriptive: it
is the stated reason a harness would accept the orchestration complexity, token overhead and latency
that resets add, instead of relying on compaction alone.

## When It Applies

The behaviour is reported as model-specific rather than universal, on the strength of two separate
observations across different harness experiments rather than a controlled comparison. Claude Sonnet
4.5 is described as exhibiting it strongly enough
that compaction alone was not sufficient for strong long-task performance, which is why context resets
became essential to that harness's design. Claude Opus 4.5 is reported to have largely removed the
behaviour on its own, allowing the author to drop context resets from a later harness entirely and run
agents as one continuous session with the [[SoftwareApplication/claude-agent-sdk]]'s automatic
compaction handling context growth.

That is also the concept's main limitation as a design input: a harness component introduced to
compensate for it can become dead weight when a newer model no longer exhibits it. The same post makes
this the general case, arguing that every component in a harness encodes an assumption about what the
model cannot do on its own, and that those assumptions are worth stress testing because they may be
incorrect and because they can quickly go stale as models improve.

How well-established it is: the term and the observation come from one vendor's engineering account of
its own experiments, written by a member of its Labs team. No measurement of the behaviour's frequency
or magnitude is reported — the authors describe it as something they observed while decomposing why
agents still tend to go off the rails on more complex tasks.

## Related Terms

- [[DefinedTerm/compaction]] — the technique this failure mode is given as persisting through
- [[DefinedTerm/context-rot]] — a different degradation associated with a filling context window
- [[DefinedTerm/long-running-agent]] — the setting in which this behaviour matters
- [[DefinedTerm/harness-engineering]] — the discipline in which the concept is applied
