---
title: "Mini-SWE-Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agent-architecture, open-source, benchmarking]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00006'
    hash: sha256:b2b6be03cc43e6f9b52518921f9545373563aec224327e1bb29a30beea7b7ce0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A minimalist open-source software engineering agent in Python, roughly 100 lines at its core, built around a linear loop and a single bash tool; it serves as a research baseline and as the floor of the harness design space."
  applicationCategory: "Coding agent (minimalist research baseline)"
  softwareVersion: "2.4.5"
  featureList: "Linear while loop with no state machine, event sourcing or concurrency; a single bash tool, one command per turn; Jinja2 templates embedded in YAML configuration, rendered once at session start; LLM access through LiteLLM; unbounded linear message history with no context management; step, cost and wall-clock limits and a cap on consecutive malformed responses; pluggable execution environments (Docker, Singularity, Bubblewrap); structural typing via Python protocols as its extension mechanism"
---

Mini-SWE-Agent is a minimalist open-source software engineering agent written in Python. In
[[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]], which
examines its source at version 2.4.5, it is the "100-line research floor" of an eleven-system corpus: the
paper describes it as implementing all seven subsystems it identifies in an
[[DefinedTerm/agent-harness]] in roughly 100 lines — a while loop, one template, one tool, a message list,
two limits, no orchestration, and structural typing as its entire extension story. The paper lists it as
coming from Princeton and Stanford.

The paper frames the minimalism as deliberate: the design isolates model capability from scaffolding
complexity to see how much of one can substitute for the other. It is used throughout that study as the
minimal form against which the other systems' implementations of each subsystem are compared.

## Capabilities

The loop is a linear `while True` that queries the model and executes the returned actions, with no state
machine, no event sourcing and no concurrency. The message list grows without bound and relies entirely on
the model's native context window, which the paper says makes trajectories perfectly reproducible and easy
to analyse. It has one tool, bash, run as a subprocess call, and its prompt asks for exactly one bash
command per turn, so directory and environment changes have to be prefixed inline because each call runs
in a new subshell. Prompts are Jinja2 templates embedded in YAML configuration and rendered once at
session start, and model access goes through LiteLLM.

Its safety mechanisms are resource limits — a step limit and a cost limit, joined in the 2.4 line by a
wall-clock limit and a cap on consecutive malformed responses — plus an opt-in interactive confirm mode.
The paper calls this sufficient for benchmark evaluation but inadequate for production use, and notes that
even this floor has acquired a minimal stuck detector. Execution can run in pluggable environments
including Docker, Singularity and Bubblewrap. Extension works through Python protocols: any class
implementing the Model, Agent or Environment protocol can be substituted without inheritance, which the
paper calls the lightest-weight extensibility mechanism in its corpus.

## Adoption & Ecosystem

The paper uses Mini-SWE-Agent as the main evidence for its observation that loop sophistication does not
predict benchmark performance, citing results the project reports on SWE-bench Verified that fall in the
same range as far larger systems. It is explicit that such figures are self-reported, obtained on
different models and dates, and not a head-to-head comparison. The same study cites it as the model for
its own first design recommendation — start with a linear loop — and its 90-line minimum-viable-harness
scaffold names Mini-SWE-Agent as the source of the linear loop it combines with other systems' patterns.
For the separate SWE-agent project, see [[SoftwareApplication/swe-agent]].
