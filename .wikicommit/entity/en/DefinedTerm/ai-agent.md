---
title: "AI Agent"
type: "schema:DefinedTerm"
lang: en
tags: [agents, tool-use, definitions]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/22/tools-in-a-loop/'
    hash: sha256:1e129d045ec8fe0ea324cf824a117a430b932ba1b520e2acf024da8f64fe481d
  - type: url
    url: 'https://simonwillison.net/2025/Sep/18/agents/'
    hash: sha256:6d9f27a63efffc1ed6b38a09e0c4427dd2728ee4c790cc63fd2321499c95670f
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:5887de1aff52ec544bd35326f452d4de9e1c58a331298d155e4a1c9f23c87af6
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An LLM that runs tools in a loop to achieve a goal. The 'tools in a loop' half is the formulation Anthropic settled on; the closing 'to achieve a goal' is Simon Willison's own addition, supplying the stopping condition that keeps the loop bounded."
---

An AI agent, in the definition Simon Willison settles on, is a large language model that **runs
tools in a loop to achieve a goal** — the widely-used "tools in a loop" formulation, extended by a
goal clause he adds himself. The model is given the ability to request actions from its
harness; the outcome of each action is fed back into the model, which continues reasoning and
acting until the goal is reached. Each part does work: "tools in a loop" names the
mechanism, and "to achieve a goal" supplies the stopping condition that distinguishes it from an
unbounded loop.

The formulation has two recorded moments in these sources. In May 2025, at an Anthropic developer
conference, an Anthropic speaker is reported as stating that at Anthropic "agents are models using
tools in a loop" — an account written up approvingly by Simon Willison, who had been frustrated that
the word was used constantly at the event without being defined. In September 2025 Willison adopted
that formulation as his own working definition, adding the goal clause to it himself after
considering and rejecting a narrower "a goal set by a user".

## Usage

The longer treatment sets out what the definition includes and deliberately leaves out. Memory is
not a separate requirement: the source argues the tools-in-a-loop model has a basic form of memory
built in, since the tool calls accumulate in a conversation with the model and the earlier steps
supply the short-term memory needed for the current goal, with long-term memory best added as a
further set of tools. Nor does the goal have to come from a user — the source considers and rejects
"a goal set by a user" as a necessary clause, on the grounds that sub-agent patterns already exist in
which one LLM sets another's goal. This is the shape described under
[[DefinedTerm/sub-agent-architecture]].

Restating the definition for a general readership in [[CreativeWorkSeries/agentic-engineering-patterns]],
Willison spells out what the word "agent" actually denotes in it, which the compressed formulation
leaves implicit: the agent is the *software* that calls an LLM with your prompt and a set of tool
definitions, then executes whatever tools the LLM requests and feeds the results back into it. On that
reading the model is a component of the agent rather than the agent itself — the same separation the
harness framing makes (see [[DefinedTerm/ai-coding-agent]]). He adds the specialisation that produces
a coding agent: its tools include one that can execute code. He also places the difficulty of defining
the term further back than the LLM era, noting that clearly defining "agent" has frustrated AI
researchers since at least the 1990s.

The source is equally clear about what it rejects. It singles out the definition of agents as
replacements for human staff as its least favourite, and argues that category "remains science
fiction" — the distinguishing feature of human staff being accountability, the capacity to take
responsibility and learn from mistakes, which it illustrates with a quoted maxim that a computer can
never be held accountable and therefore must never make a management decision. It notes
the related point that humans have agency in the sense of forming their own goals, which AI agents,
despite the name, do not. It also names OpenAI as the largest single source of confusion, observing
that the company's CEO describes agents as systems that do work independently, that its "ChatGPT
agent" feature is a browser automation system, and that only its Agents SDK closely matches the
tools-in-a-loop idea.

## When It Applies

The definition is offered as a working convention among technical implementers, not as a settled
industry meaning, and the source is explicit about the boundary: when a technical implementer says
"agent" it proposes reading them as meaning tools wired to an LLM to achieve goals in a bounded
loop, while outside that field — in conversation with non-technical business audiences — it advises
clarifying which definition the other person is using before proceeding.

Its stated rationale is that jargon is only useful when both parties share a definition, and that a
contested term makes communication less effective rather than more. The source treats this as a
long-standing problem rather than a new one, citing an earlier remark by Carl Hewitt that the
question "what is an agent?" embarrasses the agent-based computing community much as "what is
intelligence?" embarrasses mainstream AI. How well-established the definition is can be
gauged from the source's own account of arriving at it: the author reports having previously
collected and attempted to cluster 211 crowdsourced definitions, and presents this one as a
definition he became willing to use without scare quotes rather than as an authority's ruling.
Compare [[DefinedTerm/semantic-diffusion]].

## Related Terms

[[DefinedTerm/ai-coding-agent]], [[DefinedTerm/augmented-llm]], [[DefinedTerm/sub-agent-architecture]], [[DefinedTerm/agentic-coding]], [[DefinedTerm/long-running-agent]], [[DefinedTerm/semantic-diffusion]], [[BlogPosting/agent-definition-useful-jargon]]
