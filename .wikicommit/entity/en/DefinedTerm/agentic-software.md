---
title: "Agentic Software"
type: "schema:DefinedTerm"
lang: en
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
  description: "As formalized in one 2026 paper: software whose decision logic is generated at runtime by a language model rather than written in advance by human engineers, so that the agent is the system and the code it produces is a transient instrument rather than the artifact being delivered."
---

Agentic software is the term
[[ScholarlyArticle/agentic-software-restructuring-paradigm]] formalizes for software in which the
decision logic is generated at runtime rather than pre-written. That paper does not claim to have
coined it; what it presents as its own contribution is formalizing the distinction between
deterministic and agentic software. The contrast is drawn formally. A traditional software system is characterised there as a triple — computational resources, a
set of deterministic decision rules encoded in source code, and an execution environment that evaluates
those rules against inputs — whose critical property is that the rules are static with respect to
execution: every one of them must be written by a human engineer before the system encounters any
input. An AI agent system is characterised instead as a language model serving as reasoning engine, a
set of executable tools, a memory subsystem, and a planning mechanism that decomposes user intent into
action sequences.

The consequence that gives the term its point is what happens to code. In this account the model can
dynamically produce code, invoke tools and adjust its behaviour on intermediate results, none of it
pre-programmed — so the code it writes is not the system but a transient artifact, produced and
discarded as needed. The paper's compressed statement of the shift is that "AI → Software → Result"
collapses into "Agent → Result": not because software disappears, but because the agent is
simultaneously the software system and its execution engine, removing the need for a separate,
statically coded artifact in between.

## Usage

The term names a kind of software rather than a way of building it, which is what distinguishes it from
the adjacent vocabulary in the same paper's framing: there, [[DefinedTerm/agentic-engineering]] names
the discipline of building, deploying and governing such systems and
[[DefinedTerm/agent-as-a-service]] the commercial model under which they are delivered, leaving agentic
software as the artifact itself. That three-way division is that paper's own.

The paper positions it against Karpathy's "Software 2.0", which it reads as replacing hand-crafted
program logic with learned weights, and argues agentic systems go a step further because the network
does not merely replace the program but writes programs on demand, using code as a tool in service of
broader reasoning goals. It connects the pattern to the ReAct framework's interleaving of reasoning
traces with tool-use actions and to chain-of-thought prompting.

The paper's argument for why this scales differently is a complexity one. Under the traditional
paradigm a human engineer must mentally traverse a task's solution space, encode the path as a static
program, and is bounded by a fixed cognitive capacity — so a task whose space exceeds that capacity is
infeasible at any realistic cost. Under the agentic paradigm the model traverses the space with a
capacity the paper argues scales with model size and training compute, the plan decomposes the task
into independently handled subproblems, and code is generated only for the specific solution path
rather than for all contingencies. The claim drawn from this is not a percentage improvement but a
qualitative change in which problems become economically tractable.

## When It Applies

Read off the paper's formal definition, the concept applies where a system's behaviour emerges at
runtime from the interaction between a model, its tools, its memory and its planning, rather than from
a pre-specified sequence of instructions — which presupposes a reasoning engine able to decompose a
task and select actions, and tools it can act through. The paper states the definition rather than
these applicability conditions.

Its stated failure conditions are where the paper is least triumphal. It reports the
[[Dataset/evoclaw]] benchmark's finding that agent success rates fall from above 80% on isolated tasks
to at most 38% under continuous software evolution, and reads four challenges out of that: context
drift as codebases outgrow the effective context window; error propagation, where a small early error
cascades and agents lack robust recovery; absent technical-debt awareness, since agents optimise for
immediate task completion without modelling long-term costs; and verification fidelity, since an agent
can pass tests while introducing semantic errors that surface only on novel inputs. Its own conclusion
is that the paradigm is real and transformative today as an augmentation paradigm but that fully
autonomous software development remains a multi-year research problem.

How well established the term is: it rests on one paper, argued from first principles and from results
cited from other work rather than from any measurement of its own. That paper presents the formalisation
of the distinction as its own contribution, and does not say where the term itself comes from. The
underlying observation — that a model generating and discarding code at runtime is a different kind of
artifact from a program — is not contested in that source; the three-generation framing built around it
is that paper's own.

## Related Terms

- [[ScholarlyArticle/agentic-software-restructuring-paradigm]] — the paper that formalizes this
  distinction
- [[DefinedTerm/agentic-engineering]] — the discipline of building and governing these systems
- [[DefinedTerm/agent-as-a-service]] — the delivery model the same paper places at the end of its
  three-generation arc
- [[DefinedTerm/four-stage-evolution-of-agentic-engineering]] — that paper's roadmap for how far this
  kind of software has to go
- [[DefinedTerm/react-prompting]] — the reasoning-and-acting pattern the paper names as consistent with
  this account
