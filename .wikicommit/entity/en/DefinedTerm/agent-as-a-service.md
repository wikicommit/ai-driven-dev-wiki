---
title: "Agent-as-a-Service (AaaS)"
type: "schema:DefinedTerm"
lang: en
aliases: ["AaaS"]
tags: [agents, agentic-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.05608'
    hash: sha256:0793091fcad2dc48f9eb6412001558cc2e993e5d5904e18d8fd0c943453879be
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A proposed third generation of software delivery in which an agent operates autonomously in the cloud and the customer specifies the result they want rather than how to produce it, shifting the work of understanding, building and running the system to the agent and pricing to outcomes."
---

Agent-as-a-Service (AaaS) is the term
[[ScholarlyArticle/agentic-software-restructuring-paradigm]] gives to what it argues is the third
generation of commercial software delivery. Its reading of that history is that each generation
transfers complexity away from the end user and to whoever is best positioned to absorb it: locally
installed licensed software left installation and maintenance with the customer; SaaS moved
infrastructure and updates to the vendor in exchange for a subscription; AaaS moves the understanding,
building and running of the system to the agent, priced on outcomes.

What the paper claims distinguishes this step from the last is the *kind* of complexity being
transferred. SaaS liberated businesses from server rooms — operational complexity. AaaS, on the paper's
argument, liberates them from having to specify *how* a result should be produced at all: they need
only specify what result they want.

## Usage

In the interaction model the paper sets out, a human articulates intent and constraints to an agent;
the agent autonomously plans, executes (generating code as needed), validates and delivers the result;
and the human audits the outcome and provides feedback. The agent may generate thousands of lines of
code, execute database queries, call external APIs and produce visualisations, all ephemerally — what
persists is not the intermediate code but the agent's capability.

The term sits at the end of a chain of related concepts from the same source rather than standing
alone. [[DefinedTerm/agentic-software]] names the artifact, [[DefinedTerm/agentic-engineering]] the
discipline that builds and governs it, and AaaS the commercial arrangement under which it reaches a
customer. The paper's compressed statement of the shift — from "AI → Software → Result" to "Agent →
Result" — is the same one it uses for agentic software, read from the delivery side.

## When It Applies

It applies where a result can be specified and audited without specifying the route to it — which is
also the condition under which it fails. The paper's own list of what organisations should start with
is the practical version of that boundary: tasks with clear success criteria, well-defined scope and
existing test infrastructure. It states directly that not all software work is equally amenable to
agent automation.

It assumes an evaluation signal good enough to judge the delivered outcome, since under this model the
customer is buying a result rather than inspecting an implementation. The paper is explicit that the
quality of agent output depends critically on the quality of the evaluation signal, and recommends
building test suites that go beyond correctness to measure robustness, maintainability and alignment
with business intent.

The paper leaves the economics open rather than settled. It lists pricing as one of the open problems
it considers urgent: outcome-based pricing — per resolved issue, per deployed feature — may replace
subscription and usage-based models, but it states that the incentive structures and risk allocation
need careful analysis. As a term, AaaS is this paper's own framing of a trajectory it argues is
underway, rather than an established category with agreed boundaries. It names exemplars for each
generation without saying how they were chosen.

## Related Terms

- [[ScholarlyArticle/agentic-software-restructuring-paradigm]] — the paper that proposes this term and
  the three-generation arc
- [[DefinedTerm/agentic-software]] — the artifact this delivery model delivers
- [[DefinedTerm/agentic-engineering]] — the discipline that builds and governs it
- [[DefinedTerm/four-stage-evolution-of-agentic-engineering]] — the same paper's roadmap for how far
  agent capability has to advance for this model to hold
