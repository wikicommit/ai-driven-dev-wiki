---
title: "Agentic Engineer"
type: "schema:DefinedTerm"
lang: en
tags: [agents, terminology, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.06310'
    hash: sha256:46f38f583fd26c851dbe000e63a827534bfc88506117ab3f9d5423e0303e5cd8
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A working definition, proposed by Aleti, Hoda, Ray, and Chen in [[ScholarlyArticle/trustworthy-ai-software-engineers]], for what qualifies an AI agent as an AI software engineer: it must handle software engineering tasks beyond coding, demonstrate agency through planning and tool use, be collaborative within human-AI teams, and respect human values, constraints, and ethical accountability."
---

An agentic engineer, as defined in [[ScholarlyArticle/trustworthy-ai-software-engineers]], is an AI agent that satisfies four conditions before it can be considered an AI software engineer rather than merely an AI coding agent. The definition is deliberately set higher than "autonomous coding": software engineering is treated as extending well beyond programming into requirements elicitation, specification analysis, architectural design, testing, and long-term maintenance, so an agent must be judged against that fuller scope of activity.

## Usage

The four conditions are: (i) the agent must be able to handle a range of software engineering tasks beyond coding, such as evolving problem statements, requirements, constraints, ethics, design, testing, and operations, under iterative refinement and partial information; (ii) the agent must demonstrate agency through planning and tool use, extending beyond code-centric tasks; (iii) the agent must be collaborative, integrating into human workflows by supporting coordination, feedback, and negotiation, since software engineering is fundamentally team-based; and (iv) the agent must respect human values, constraints, and ethical responsibility, justifying its decisions and supporting accountability and oversight.

[[ScholarlyArticle/trustworthy-ai-software-engineers]] frames this as a shift in the role of human engineers, from directly performing tasks toward supervision, orchestration, validation, and ethical oversight of agentic engineers operating within human-AI software engineering teams, rather than a model of AI replacing human engineers.

**A second and incompatible use of the same term** comes from
[[ScholarlyArticle/from-determinism-to-delegation]], where the agentic engineer is a **human**
professional archetype rather than an AI agent: the practitioner of
[[DefinedTerm/ai-native-software-engineering]], whose primary artifact is the agentic system rather
than the program. That paper's compressed statement of the distinction is that software engineering
builds the system while agentic engineering builds the agentic system that helps build, operate and
evolve the system — software engineers optimised for deterministic design and implementation, agentic
engineers for orchestrating probabilistic collaborators safely and productively. Readers should note
that the two sources use "agentic engineer" for opposite sides of the human-AI relationship, and
neither acknowledges the other.

That paper characterises the human archetype across fourteen dimensions, and along three axes it
treats as the paradigm shift itself: the unit of work moves from code implementing a feature to a
supervised agent workflow; the correctness model from binary assertion to statistical evaluation under
uncertainty; and accountability from authorship to outcome ownership. It names the scarce skill as
judgment — writing a specification precise enough for an agent to execute, then detecting the
plausible-but-wrong output a deterministic test would never flag — and is explicit that its
fourteen-dimension table is an analytical scaffold rather than an empirically validated taxonomy.

On what the role demands, that paper maps agentic-engineering practice onto the SFIA 9 responsibility
ladder, from executing deterministic commands via generative assistants at Level 1, through authoring
asynchronous integration code and configuring vector databases, to constructing multi-agent state loops
and evaluation pipelines at mid-levels, and leading ISO/IEC 42001 and NIST AI RMF audits and governing
model portfolios at the top. It decomposes competency into technical skills, soft skills, knowledge and
abilities, and reports that educators increasingly argue curricula should prioritise problem definition,
system design and debugging/evaluation over code authoring — a stance it notes is consistent with its own
evidence that value migrates toward oversight. It marks one common claim as unsettled: that senior engineers
adapt more readily is, it states, a hypothesis rather than a settled finding, and the controlled
evidence on which cohorts benefit is mixed — a lab experiment and three field experiments report
substantial gains, largest for less experienced developers, while a randomized controlled trial of 16
experienced open-source developers on their own mature repositories found a 19% increase in completion
time.

## Related Terms

[[ScholarlyArticle/trustworthy-ai-software-engineers]], [[DefinedTerm/trustworthiness-dimensions]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/craft-values-and-principles]], [[DefinedTerm/agentic-se-vocabulary-considerations]]

- [[ScholarlyArticle/from-determinism-to-delegation]] — source of the second, human-archetype account
  above
- [[DefinedTerm/ai-native-software-engineering]] — the paradigm that account says produces the role
- [[DefinedTerm/supervised-agency-spectrum]] — how the oversight it centres on is graduated
- [[DefinedTerm/compositional-reliability]] — one of the structural limits it says the role must work
  within

Not to be confused with [[DefinedTerm/agentic-engineering]], a distinct term for the discipline or
practice rather than a definition of the agent or the person; that page carries its own competing
accounts.
