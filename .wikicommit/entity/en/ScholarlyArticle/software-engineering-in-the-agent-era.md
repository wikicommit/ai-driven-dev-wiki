---
title: "Software Engineering in the Agent Era: From Trustworthy Change to Human–Agent Software Organizations"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-software-engineering, software-engineering, governance, theory]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.04630'
    hash: sha256:b89995b073da21f1e6d786f61dc056209cbca90ea6c15505e774483a51c9963e
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A theory-building preprint arguing that once coding agents make digital execution elastic, software engineering should govern the software change itself; it introduces Trustworthy Change, Responsibility Topology and the Human–Agent Cell, and states falsifiable propositions for testing them."
  author: ["Zhongjie Wang", "Mingyi Liu"]
  datePublished: "2026-09-04"
  abstract: "Software agents make digital execution unusually elastic while problem framing, semantic commitment, verification, integration, attention and acceptance of residual risk remain bounded by human cognition, organizational authority and economic capacity. The paper develops a testable framework around two primary constructs — Trustworthy Change and Responsibility Topology — and one execution abstraction, the Human–Agent Cell, derives consequences for change state, shared engineering facts, verification and flow control, and treats Progressive Specification and bounded-capacity analysis as hypotheses to be tested."
  keywords: ["Agent Software Engineering", "Trustworthy Change", "Human–Agent Cell", "Responsibility Topology", "Progressive Specification", "Human–Agent Software Organization"]
---

This preprint starts from an asymmetry: coding agents let digital execution — repository analysis, code
generation, testing, migration, tool use and parts of operations — be replicated and parallelized
without a matching growth in headcount, while problem framing, semantic commitment, verification,
integration, human attention and the acceptance of residual risk remain bounded by human cognition,
organizational authority and budget. The authors argue that this moves software engineering's object of
control away from human activity and toward the software change itself, a shift they summarize as moving
from human process control to trusted change governance.

To organize that shift the paper proposes two primary constructs and one execution abstraction.
[[DefinedTerm/trustworthy-change]] is the engineering object that follows a change from intent through
delegation, verification, integration, acceptance and operation. [[DefinedTerm/responsibility-topology]]
classifies a software organization by how independent authority to accept residual risk is distributed,
distinguishing a single-center form with one final responsibility anchor from a multi-anchor form that
requires joint acceptance across independently governed domains. The
[[DefinedTerm/human-agent-cell]] is the execution unit — a human with their agents, context, tools,
permissions and budget — which produces candidates, proposals and evidence but does not by executing
gain authority to accept them. A running example, splitting an order system's `cancelled` status into
user cancellation and payment-timeout `expired`, is used throughout to show that a small artifact change
can carry a large semantic, verification and responsibility scope.

The authors describe their contribution as theory construction and operationalization rather than
empirical validation, and state explicitly that responsibility, accountability, change management,
specification, verification and human oversight all predate the paper; their narrower claim is that
agent-scaled execution changes how these concerns fit together.

## Key Points

- The paper represents a change's governance as five loops — intent, delegation, verification,
  integration and operation — with specification as the refinement that makes intent delegable, evidence
  as the main output of verification, and responsibility cutting across all five.
- It separates a change's progression into Candidate, Eligible and Accepted states, so that finishing
  implementation, passing engineering qualification and formally accepting residual risk are not
  collapsed into one notion of "done"; only an accepted change may modify the authoritative baseline.
- It lists six conditions that stop a candidate from becoming eligible — failures of intent/specification,
  delegation/resources, change/provenance, evidence, integration/operation and responsibility — and
  treats a change whose required approver exists but has not yet signed off as acceptance-pending rather
  than as a responsibility failure.
- It argues that Responsibility Topology is independent of headcount: a founder running twenty concurrent
  agents can remain single-center, while two engineers can form a multi-anchor organization if each holds
  a non-revocable acceptance right over an affected domain.
- It distinguishes pressures created by distributed execution (context divergence, stale context) from
  those created by distributed authority (joint acceptance, responsibility closure), and proposes Context
  Invalidation — each in-flight task choosing to continue, mark stale, refresh, replan, reverify or stop
  when an authoritative fact changes — as the response to the first.
- It proposes a Minimum Sufficient Specification hypothesis: that for a given class of change there may
  be a level of specification rigor beyond which added rigor no longer repays its lifecycle cost; the
  cost curves it draws are labelled as illustrative and not fitted to data.
- It treats a task given to an agent as a contract covering goal, context, scope, permission, budget,
  acceptance, stop condition and handoff, and makes the stop condition first-class so that an agent
  escalates rather than proceeding when it needs unauthorized data, wider write access, an irreversible
  migration or a larger budget.
- It frames agent security around containment: a compromise of an agent's interpretation, for example by
  prompt injection, should not become an unbounded compromise of its actions, which permission
  boundaries, sandboxes, tool hooks and egress policies should limit.
- It argues that when generation outpaces verification a verification queue forms, and that as it grows
  the responsible person is pushed toward relying on summaries and rapid approvals; it proposes counting
  accepted changes, rather than lines of code, commits or agent tasks, as the accounting boundary for
  trustworthy output.
- It states eight propositions with observable expectations and falsification signals — among them that
  agent concurrency saturates against fixed verification capacity and that Responsibility Topology keeps
  explanatory power after controlling for headcount — and proposes an "augmented Conway" hypothesis that
  agent delegation and context dependency add explanatory power for software co-change beyond human
  communication.

## Notes

The paper positions itself against SE 3.0 and [[DefinedTerm/structured-agentic-software-engineering]],
which it describes as examining changes to actors, processes, tools and artifacts, and against
[[DefinedTerm/spec-driven-development]] and harness engineering, whose primitives — repository
instruction files, skills, hooks, MCP tools, sandboxes and sub-agents — it maps onto its own constructs
rather than claiming as new. It also describes adjacent 2026 work on human–agent responsibility
protocols and graduated oversight as specifying how responsibility is constrained or oversight
calibrated, rather than classifying organizations by independent acceptance centers.

The authors note that their running example is illustrative and not a case study, that their capacity
bounds are schematic rather than calibrated laws, that the empirical commitments cover only the
single-center and multi-anchor forms and not hierarchical, federated or platform-mediated
responsibility, and that any of their central distinctions may fail to survive measurement.
