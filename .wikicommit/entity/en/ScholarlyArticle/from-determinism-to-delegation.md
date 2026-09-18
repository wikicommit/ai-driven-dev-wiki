---
title: "From Determinism to Delegation: AI-Native Software Engineering and the Evolution of the Agentic Engineer"
type: "schema:ScholarlyArticle"
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
  description: "A position paper arguing that engineering value is migrating from authoring deterministic code to governing probabilistic autonomous behavior, characterizing the shift along three axes and arguing from contested productivity evidence that disciplined oversight, not automation, is the load-bearing competency."
  author: ["Mamdouh Alenezi"]
  datePublished: "2026-06-30"
  keywords: ["AI-native software engineering", "agentic engineer", "compositional reliability", "AI governance"]
---

This paper argues that as large language models acquire the capacity for sustained, multi-step,
tool-mediated execution, the locus of engineering value migrates from authoring deterministic code
toward governing probabilistic, autonomous behavior — and that this is a paradigm shift rather than a
tooling upgrade, giving rise to a distinct professional archetype it calls the
[[DefinedTerm/agentic-engineer]]. Its central claim is one of symbiosis rather than substitution: the
agentic engineer is constructed upon, and remains accountable through, classical engineering discipline.

The shift is characterized along three axes. The **unit of work** moves from deterministic code
implementing a feature to a supervised agent workflow, so that engineering effort goes into shaping the
operating environment — what an agent can perceive, which tools it may access, what modifications it
may make, and when human intervention is required — rather than prescribing every computational step.
The **correctness model** moves from binary assertion, verifiable locally through tests and
specifications, to statistical evaluation under uncertainty, where the question becomes whether a system
is sufficiently reliable under realistic operating conditions and whether its failure modes are
acceptable. The **accountability model** moves from authorship to outcome ownership: agents may generate
code, review pull requests and propose modifications, but do not assume responsibility for outcomes, so
governance mechanisms such as auditability, approval workflows and intervention policies become
architectural requirements rather than operational afterthoughts.

The paper states its own epistemic status directly: it is a position paper whose goal is to synthesize a
rapidly evolving body of literature into a coherent argument and a set of testable predictions, drawing
quantitative findings from the studies it cites and framing forward-looking claims explicitly as
hypotheses.

## Key Points

- A fourteen-dimension comparison contrasts the software engineer with the agentic engineer across core
  paradigm, primary output, unit of work, knowledge domain, tooling, architecture, design pattern,
  lifecycle, testing, debugging, security, accountability, success metrics and mindset. The paper is
  explicit that this table is an analytical scaffold rather than an empirically validated taxonomy.
- The paper deliberately foregrounds contested evidence rather than only supportive results: a lab
  experiment reporting a 55.8% reduction in completion time, three field experiments across 4,867
  developers reporting 26.1% more completed tasks with the largest gains for less experienced
  developers, and a randomized controlled trial of 16 experienced open-source developers on their own
  mature repositories reporting a 19% *increase* in completion time — even though those developers had
  forecast a 20–24% speedup.
- It draws the argument of the paper from that juxtaposition: gains concentrate on well-scoped tasks and
  lower-context cohorts while high-context expert work can incur net costs, which is why it holds that
  oversight and calibrated judgment rather than raw automation are the load-bearing competencies, and
  why it treats the perception–reality calibration gap as itself a managed risk.
- [[DefinedTerm/compositional-reliability]] is formalized: if an agent must complete n dependent steps
  each succeeding independently with probability p, end-to-end success is p to the power n, so a
  per-step rate of 0.95 yields roughly 0.36 over twenty steps. The paper notes this is an optimistic
  upper bound, since real errors correlate and cascade.
- [[DefinedTerm/behavioral-drift]] is formalized as two distinct shifts — data drift in the marginal
  input distribution and concept drift in the conditional — and compounded by provider-side model
  updates, so that an agent has no stable terminal state and requires permanent stewardship.
- The paper reports measured attack rates for indirect prompt injection, citing a tool-integrated
  benchmark that found ReAct-prompted GPT-4 agents successfully attacked in roughly 24% of cases, and
  argues that defenses differ in kind from classical perimeter security: strict tool-permission scoping,
  output guardrails, sandboxed execution and human-in-the-loop checkpoints for destructive actions.
- It treats evaluation as the central artifact of agentic practice rather than an afterthought, while
  documenting that the dominant grading mechanism is itself imperfect — LLM judges exhibit position,
  verbosity and self-preference biases, and judge choice can reorder model rankings.
- Six predictions are advanced, each stated as a falsifiable hypothesis with the observation that would
  refute it: convergence of the two roles into a hybrid archetype; agents performing first-pass work
  across the lifecycle; effects remaining strongly heterogeneous; evaluation and reliability
  consolidating into a named discipline; the falling cost of modification turning one-way architectural
  decisions into two-way doors; and standards fluency becoming a hiring filter.

## Notes

The paper maps agentic-engineering practice onto the SFIA 9 responsibility ladder, running from
executing deterministic commands at Level 1 through constructing multi-agent state loops and evaluation
pipelines at mid-levels to leading ISO/IEC 42001 and NIST AI RMF audits and governing model portfolios
at the top. Its governance section draws on three complementary frameworks — ISO/IEC 42001 as an
auditable AI management system, the IEEE 7000 series as a value-engineering process tracing stakeholder
values to technical requirements, and the NIST AI RMF as a continuous govern–map–measure–manage life
cycle — with the throughline that governance is integrated into architecture rather than appended to it.

Its open problems are evaluation validity, since LLM-as-judge introduces circularity and documented bias
while trajectory metrics may reward spurious tool sequences; compositional reliability, since principled
methods for bounding end-to-end reliability under correlated failures are lacking; security under
agency; accountability attribution, which it describes as legally and ethically unsettled when an agent
proposes and a human approves, especially across vendor model updates that silently alter behavior;
workforce formation, where curricula and certification taxonomies lag practice; and sustained
stewardship, where the cost model of permanent monitoring and re-alignment is not well understood at
portfolio level.

The paper states its own threats to validity as a synthesis. The controlled-evidence base is small,
recent and tied to specific tool generations, so the effect sizes should be read as time-stamped
snapshots rather than stable constants; the fourteen-dimension comparison is an analytical construct;
the forecasts concern a fast-moving field and are offered as falsifiable hypotheses. It says it has
sought to mitigate selection bias by reporting disconfirming evidence, while noting a residual bias
toward published, English-language literature.
