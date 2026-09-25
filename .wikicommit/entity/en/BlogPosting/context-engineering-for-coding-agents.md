---
title: "Context Engineering for Coding Agents"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, context-window, claude-code]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html'
    hash: sha256:5d6208219888475f13564a3c1495a0291ee1a06c40a75c10315de16798f766b5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A February 2026 memo by Birgitta Böckeler in the \"Exploring Gen AI\" series on martinfowler.com, giving a primer on the context configuration features of coding agents and mapping Claude Code's features onto dimensions of what kind of context each is and who decides to load it."
  author: ["Birgitta Böckeler"]
  datePublished: "2026-02-05"
  publisher: "martinfowler.com"
---

This memo, part of the "Exploring Gen AI" series on martinfowler.com in which Thoughtworks
technologists record their explorations of generative AI for software development, is a primer on
the options for configuring and enriching a coding agent's context. The author observes that these
options have multiplied over the preceding months, with Claude Code leading and other coding
assistants following, and that [[DefinedTerm/context-engineering]] is becoming a large part of the
developer experience of these tools. She quotes a colleague's definition of the practice as
"curating what the model sees so that you get a better result."

The memo sorts context configuration into reusable prompts and what the author calls
[[DefinedTerm/context-interfaces]], asks who decides when each piece of context is loaded and how
much of it there should be, and then walks through the features of
[[SoftwareApplication/claude-code]] as of January 2026 along those dimensions. It closes with the
difficulties of sharing context configurations and a warning against overestimating how much
control they give.

## Key Points

- Almost all forms of context engineering for coding agents come down to Markdown files holding
  prompts. The author splits their intent into **instructions** (prompts telling the agent to do
  something) and **guidance** (general conventions it should follow, also called rules or
  guardrails), while noting that the two often blend.
- The author uses "context interfaces", a term she says she could not find an established name for,
  for descriptions that tell the LLM how it can obtain more context if it decides to: built-in
  tools, MCP servers ([[DefinedTerm/model-context-protocol]]) and skills
  ([[DefinedTerm/agent-skills]]). The more of them are configured, the more of the context they
  occupy, so they should be chosen per task.
- File reading and searching in the workspace are singled out as the most basic and powerful context
  interfaces, which makes it worth reflecting on how well an existing codebase serves as context.
- Context can be loaded by three kinds of decider: the LLM (needed for unsupervised agents, but with
  some uncertainty whether it will actually load the context when expected — e.g. skills), a human
  (control at the cost of automation — e.g. slash commands), or the agent software itself at
  deterministic points (e.g. Claude Code hooks).
- An agent's effectiveness goes down when it is given too much context, and too much context also
  costs money, so large context windows are not a reason to fill them. The author recommends
  building up context such as rules files gradually rather than front-loading it, noting that more
  capable models may no longer need what had to be spelled out half a year earlier.
- Transparency about how full the context is and what is taking up space is presented as a crucial
  tool feature; some tools also optimise context themselves, by periodically compacting the
  conversation history or by optimising how tools are represented.
- In Claude Code's feature set as the memo describes it: [[DefinedTerm/claude-md]] is guidance always
  loaded at the start of a session, for the most frequently repeated project-wide conventions, with
  [[DefinedTerm/agents-md]] mentioned as an attempt to standardise such a main rules file; rules are
  guidance that can be scoped to file paths and are loaded when matching files are loaded; slash
  commands ([[DefinedTerm/custom-slash-commands]]) are human-triggered instructions, described as
  deprecated in Claude Code and superseded by skills; skills bundle guidance, instructions,
  documentation and scripts that the LLM (based on the skill's description) or a human can load on
  demand; subagents combine instructions with a model and tool configuration and run in their own,
  parallelisable context window; MCP servers give the agent access to data sources and actions;
  hooks ([[DefinedTerm/agent-hooks]]) are scripts run deterministically on lifecycle events; and
  plugins are a way to distribute any of these.
- The author calls the current moment a "storming" phase and expects the feature list to converge —
  for example, skills absorbing both slash commands and rules.
- Good context setups take time to build, because a configuration has to be used for a while before
  one can tell whether it works — "there are no unit tests for context engineering". Sharing them is
  hampered by differences between the sharer's and receiver's contexts (it works better within a team
  than between strangers), a tendency to over-engineer with copied instructions, differing
  experience levels, and low awareness of what copied context contains, which can lead to repeated or
  contradictory instructions.
- The memo argues that context engineering is not really engineering: execution still depends on how
  the LLM interprets the instructions, so claims that a feature will "ensure" behaviour or "prevent
  hallucinations" overstate it. It can raise the probability of useful results, but one still has to
  think in probabilities and choose an appropriate level of human oversight.

## Context

The memo is explicitly a snapshot: its Claude Code feature list is dated January 2026, and the
author presents the feature landscape as still in flux. Its categories — instructions versus
guidance, context interfaces, and who decides to load context — are the author's own framing for
organising the features, and its recommendations (build context up gradually, beware copied setups)
rest on her own experience rather than on measurement.
