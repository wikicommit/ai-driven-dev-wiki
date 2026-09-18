---
title: "AI-Native Software Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agentic-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A proposed paradigm in which software engineering shifts from authoring deterministic code to governing probabilistic autonomous behavior, characterised along three axes: the unit of work, the correctness model, and the accountability model."
---

AI-native software engineering is the term
[[ScholarlyArticle/from-determinism-to-delegation]] gives to the paradigm it argues is emerging as
large language models acquire the capacity for sustained, multi-step, tool-mediated execution. Its
claim is that this is not an incremental tooling upgrade applied within existing practice but a change
in how software work is structured, how system quality is evaluated, and how responsibility is
assigned. The paper argues the three changes are connected — a change in one tends to influence the
others — and together describe a transition from deterministic implementation toward engineering
centred on delegation, supervision and probabilistic behaviour.

## Usage

The paradigm is characterised along three axes.

**The unit of work.** Classically the primary unit is deterministic code implementing a feature,
service, API or platform component, and the process emphasises decomposing systems into modules with
specified behaviour and verifying each artifact. In this paradigm the unit becomes the supervised agent
workflow. The design questions shift to what an agent can perceive, which tools it may access, how it
reasons about tasks, what modifications it is allowed to make, how outputs are evaluated, and under
which conditions human intervention becomes necessary. Rather than prescribing every computational
step, the engineer shapes the operating environment in which the system acts — so engineering effort
moves from constructing individual behaviours toward constructing the conditions under which desirable
behaviours are likely to arise.

**The correctness model.** Classical systems rely on binary correctness verifiable locally through
assertions, tests and formal specifications. Agentic systems often operate where many tasks admit no
single deterministic output, so correctness becomes statistical and system-level, measured through
evaluation pipelines reporting task success rate, faithfulness, tool-use accuracy and hallucination
frequency. The paper's illustration is that a 94% task success rate may be entirely acceptable in one
setting and unusable in another, so the central question shifts from "is the system correct?" to "is
the system sufficiently reliable under realistic operating conditions, and are its failure modes
acceptable?".

**The accountability model.** In specification-driven development accountability follows from
authorship. Here, agents may generate code, review pull requests, summarise incidents, identify defects
or propose modifications, but do not assume responsibility for outcomes; human engineers retain
ownership and remain accountable for quality, security and production readiness. The paper's
formulation is that responsibility does not disappear as autonomy increases — it becomes concentrated
around oversight and outcome ownership, which is why governance mechanisms such as auditability,
approval workflows and intervention policies become architectural requirements rather than operational
afterthoughts.

The proposition the paper compresses all this into is that software engineering builds the system while
agentic engineering builds the agentic system that helps build, operate and evolve the system.

## When It Applies

The paradigm as described assumes agents capable of sustained multi-step execution against real tools,
and a setting where outcomes can be evaluated statistically rather than asserted. It does not claim to
displace classical practice: the paper is explicit that autonomous systems still depend on
deterministic foundations — reliable interfaces, secure infrastructure, high-quality data, verifiable
testing environments — and frames the relationship as complementary and mutually dependent rather than
successive.

Its own evidence is where the paper sets the limits, and it foregrounds the disagreement rather than
resolving it. Against a lab experiment reporting 55.8% faster completion on a bounded task, and three
field experiments across 4,867 developers reporting 26.1% more completed tasks with the largest gains
for less experienced developers, it sets a randomized controlled trial of 16 experienced open-source
developers working on their own mature repositories, which found early-2025 AI tools *increased*
completion time by 19% — while those same developers had forecast a 20–24% speedup. The reading the
paper draws is that gains concentrate on well-scoped tasks and lower-context cohorts while high-context
expert work can incur net costs, which is the basis for its thesis that oversight and calibrated
judgment rather than raw automation are the load-bearing competencies. It treats the gap between
perceived and actual benefit as itself a risk to be managed.

Two further limits are structural rather than empirical. [[DefinedTerm/compositional-reliability]]
means multi-step autonomy degrades multiplicatively, so high per-step accuracy does not carry over long
horizons. [[DefinedTerm/behavioral-drift]] means there is no terminal state: an agent requires
permanent stewardship, so "done" is obsolete as a concept and the cost model of continuous monitoring
and re-alignment is, the paper says, not yet well understood at portfolio level.

As a term it rests on a single position paper that presents itself as such — a synthesis of a rapidly
evolving literature into an argument and a set of falsifiable predictions, drawing its quantitative
findings from the studies it cites rather than from measurements of its own. The paper notes its
controlled-evidence base is small, recent and tied to specific tool generations, and asks that the
effect sizes be read as time-stamped snapshots rather than stable constants.

## Related Terms

- [[ScholarlyArticle/from-determinism-to-delegation]] — the paper that proposes this term
- [[DefinedTerm/agentic-engineer]] — the professional archetype this paradigm is argued to produce
- [[DefinedTerm/supervised-agency-spectrum]] — how the oversight this paradigm centres on is graduated
- [[DefinedTerm/compositional-reliability]] — one of the two structural limits above
- [[DefinedTerm/behavioral-drift]] — the other
- [[DefinedTerm/agentic-engineering]] — an adjacent and separately-sourced term for the discipline
