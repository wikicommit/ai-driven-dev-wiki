---
title: "Loop Specification"
type: "schema:DefinedTerm"
lang: en
tags: [loop-engineering, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.00038'
    hash: sha256:2f17c51102988847128a0fb57824555d6ac3a32183f9ed61e269f1a63d48d4c0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A bounded, reusable artifact — a trigger, a goal, a verification step, a stopping rule and a memory — that a human designs and hands to an agent harness so the agent pursues a goal on its own in place of step-by-step prompting; proposed as the object of study of loop engineering."
---

A loop specification is a bounded, reusable artifact that a human designs and hands to an agent
harness so that the agent pursues a goal on its own, in place of step-by-step prompting. The term
is proposed in [[ScholarlyArticle/stop-hand-holding-your-coding-agent]], which uses it to name the
object of [[DefinedTerm/loop-engineering]]. According to that paper, a loop specification has five
parts: a **trigger** that starts it (a person, a schedule or an event); a **goal**, preferably
verifiable; an **execution** phase in which the agent works, ideally by calling proven, named skills;
a **verification** that checks the result for real; and a **stopping rule** that drives the loop to a
named terminal state — success, no-op, blocked, stalled or exhausted — without ever mistaking an error
for success. A **memory** of progress and decisions persists across turns, on disk rather than in the
conversation.

## Usage

The paper introduces the term to separate three things that share the word "loop": an ordinary
programming loop, which is plain control flow; the internal agent cycle in which a model runs tools
over a stop condition, which is part of the [[DefinedTerm/agent-harness]] and exists whether or not
anyone designs it; and the loop specification, the external artifact a human writes and hands to that
harness. It summarizes the distinction as "the harness supplies the engine; loop engineering writes
the pilot," and argues that conflating the senses is exactly the confusion the "stop prompting"
slogan invites.

It organizes loop specifications along the dimensions a designer chooses: the trigger, the goal
type (verifiable, model-judged or mixed), the rigour of verification on a five-level
[[DefinedTerm/verification-ladder]], the architecture (solo, maker and separate checker, or manager
orchestrating helpers), and the named terminal states. In the operational form it adopts from
practitioner accounts, a real loop system assembles scheduled automations, isolated worktrees, skills,
plugins and connectors, and sub-agents that separate the maker from the checker, with memory kept in
files. The paper's accompanying skill, [[SoftwareApplication/sandeco-loop]], writes loop
specifications as a single document.

## When It Applies

The paper's "golden rule" is that a loop specification is justified over a bare scheduled prompt only
when the result of one turn changes the next action; a fixed task on a fixed cadence where nothing
about the last run informs the next is a scheduled one-shot, not a loop. It names further cases where
a loop is the wrong tool: when the goal is pure taste with no reproducible check, when the work is
ambiguous greenfield construction where the right direction is unknown, and when the cost of looping
does not pay for itself. It assumes a harness that already provides the internal agent cycle, and
state that can live on disk.

Failure modes it names include a loop that wraps a raw model in an unbounded retry with no named
skills and no real check; a loop in which the same model produces and grades the work; specification
gaming, where the loop satisfies the letter of its check but not its spirit; reporting a model
judge's opinion as if it were a deterministic check; and an unattended runaway with no task-related
stopping rule, stagnation detector or budget ceiling.

As for how established it is: the term is a single author's proposal in a position paper. Its
supporting evidence is a descriptive, hand-coded reading of one public catalogue of fifty loops, and
its design principles are grounded in literature that mostly studies the internal agent cycle, a
transfer the author calls an argued analogy rather than a measured result.

## Related Terms

[[DefinedTerm/loop-engineering]], [[DefinedTerm/verification-ladder]],
[[DefinedTerm/harness-engineering]], [[DefinedTerm/ralph-loop]], [[DefinedTerm/agent-harness]]
