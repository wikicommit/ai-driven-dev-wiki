---
title: "Designing Agentic Loops"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, agent-tooling]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Sep/30/designing-agentic-loops/'
    hash: sha256:616bc39546fd4aab969e3a8ec0a6fa01330405714c063a028ab4419f84132964
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The skill of setting up a coding agent to brute-force a problem: reducing it to a clear goal, choosing the tools the agent will iterate with, deciding how safely the loop can be allowed to run, and scoping any credentials it needs. Named by Simon Willison in a September 2025 post."
---

Designing agentic loops is the practice of deliberately constructing the goal, the toolset and the
running conditions under which a coding agent is left to iterate towards a solution. It follows from
treating an agent as something that runs tools in a loop to achieve a goal: if that is what an agent
is, then the part a person contributes is the loop's design rather than its execution. The term was
proposed by Simon Willison in a post of September 2025, explicitly as an attempt to give a name to a
skill he judged to be emerging — see [[BlogPosting/designing-agentic-loops]].

## Usage

The practice is described as having four parts. The first is reducing the problem to a clear goal
and a set of tools that can iterate towards it, so that the agent's ability to try repeatedly
becomes useful rather than aimless — the framing is that coding agents are brute-force tools, and
brute force needs something to push against. The second is deciding how freely the loop may run:
approval-per-command is safer but is argued to dramatically reduce effectiveness at this kind of
problem solving, so the design question is what containment makes unattended running acceptable (see
[[DefinedTerm/yolo-mode]] and [[DefinedTerm/sandboxing]]).

The third part is choosing the tools themselves. The source argues for thinking in shell commands
rather than reaching for [[DefinedTerm/model-context-protocol]], on the grounds that coding agents
are good at running shell commands, and for recording the ones an agent will need in an
[[DefinedTerm/agents-md]]-style file — with a single worked example generally sufficient for the
agent to generalise from, and well-known tools needing only to be named. The fourth is credentials:
where authenticated access is unavoidable, the recommendations are to prefer test or staging
environments where damage is contained, and to attach a hard budget limit to anything that can spend
money.

## When It Applies

The stated precondition is a problem with **clear success criteria** whose solution is likely to
involve tedious trial and error; the offered signal for recognising one is catching yourself
thinking that you will have to try a lot of variations. The source's examples are debugging a
failing test, benchmarking a slow query against added and dropped indexes, working through a backlog
of dependency upgrades, and iterating on a Dockerfile to shrink an image. Its stated common factor is
automated tests: a cleanly passing suite is what lets the agent tell progress from regression, and
the source holds that it massively amplifies what agents are worth.

The practice assumes a containment decision has already been made, because the loop only pays off
when the agent is not stopping for approval. The source is candid that the usual resolution is to
take the risk unmitigated, and that its own preferred alternatives — a container, or a disposable
cloud environment — are personal risk judgments rather than guarantees; it notes that container
escapes exist and that it has not seen agent vendors' own sandboxing documented convincingly enough
to trust. How well-established the practice is, is stated plainly in the source: it is a very fresh
area, and the term is offered as a starting point for discussion by one practitioner rather than as
settled usage.

## Related Terms

[[DefinedTerm/yolo-mode]], [[DefinedTerm/sandboxing]], [[DefinedTerm/ai-agent]],
[[DefinedTerm/ai-coding-agent]], [[DefinedTerm/agents-md]], [[DefinedTerm/agentic-loop-engineering]]

- [[DefinedTerm/agentic-loop-engineering]] — a separate, more formal proposal for governing how
  agents execute tasks, arrived at from a research rather than a practitioner direction
- [[DefinedTerm/outer-loop]] — the surrounding cycle this loop sits inside
