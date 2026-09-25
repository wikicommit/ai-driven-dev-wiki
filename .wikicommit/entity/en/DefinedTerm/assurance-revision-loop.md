---
title: "Assurance-Revision Loop"
type: "schema:DefinedTerm"
lang: en
tags: [verification, assurance, outer-loop, human-in-the-loop, deployment]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.12039'
    hash: sha256:2c380af110701fb8cbb7253c833a6d4bc078b3ffc06e5f12cf37196be86ff2d0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An outer loop, proposed alongside the two-gap framework, that surrounds the implementation-verification loop and uses stakeholder judgment and deployment evidence to revise the requirements, environment model, evaluator, implementation or deployment safeguards whenever deployed behaviour is rejected."
---

The assurance-revision loop is the outer of the two loops proposed in
[[ScholarlyArticle/reality-is-the-final-verifier-on-two-key-gaps-in-agentic-software-engineering]].
The inner implementation-verification loop revises an implementation until an evaluator accepts it
against fixed requirements under a fixed environment model; the outer loop exists because, under the
[[DefinedTerm/two-gap-framework]], acceptance by that evaluator does not establish that the software meets
stakeholder intent in the real world. It builds and maintains justified confidence — assurance — as
evidence, intent and deployment conditions change, using accountable human judgment and empirical
deployment evidence to revise the artifacts responsible for a failure rather than only patching the
implementation, after which the inner loop reruns. Together the two loops are what the paper calls
software assurance.

## Usage

The paper describes the loop as reusing familiar mechanisms — code review, staged deployment, A/B testing,
production monitoring and incident response — which agentic development makes critical rather than
optional. When evidence materially weakens confidence, before or after deployment, the assurance team is
to preserve the evidence needed to reproduce the behaviour, determine whether the implementation, the
requirements, the model, the evaluator or an operational safeguard must change, revise the responsible
artifacts, rerun the inner loop, and release again gradually with bounded exposure, explicit stop
conditions and tested recovery. Its diagnosis table maps an implementation defect to revising the
implementation and adding a regression check, a requirement gap to revising the requirements and
extending the evaluator, and a model gap to revising the model, evaluator, monitors or controls.

Within the loop, agent-generated software is treated as possibly compromised until independent evidence
establishes otherwise, and established safety and security practice is organised around three
objectives: reduce the frequency of deployment misbehaviour (refining requirements with prototypes,
boundary cases and adversarial review; making environment assumptions explicit and testing them), limit
its impact (least privilege and isolation, staged exposure from replay through shadow and canary
deployment to gradual release, and runtime monitors generated for consequential requirements and
assumptions), and prevent its recurrence. The loop also maintains a versioned assurance argument linking
the top-level claim to its evidence, assumptions, approved scope, owners and invalidation conditions.

## When It Applies

- It applies whenever software produced by a developer or coding agent is deployed into an open,
  changing environment, where the paper argues the requirement and model gaps cannot be certified closed
  in advance.
- It assumes accountable human stakeholders with authority over intent. Agents are to do as much of the
  outer-loop work as evidence and risk permit, but humans retain authority over consequential decisions;
  the paper states this does not mean human review of every step, since routine bounded decisions can be
  delegated.
- Effort is meant to scale with risk: routine changes can rely on inexpensive, reusable automation, while
  changes with serious consequences, uncertain assumptions or limited reversibility call for more
  realistic evaluation and more human attention. The authors add that productivity should be measured over
  the whole workflow at the required assurance level, and that agent autonomy should be reduced if agents
  cannot improve that workflow.
- The paper names two failure modes to guard against: runtime monitors derived from the same artifacts
  as the implementation may inherit the same omissions, so operators should review them and add
  independent telemetry; and escalation designs that leave humans only the rare, difficult cases can
  erode the skill and situational awareness they need to respond.
- It is one research group's proposal, assembled from long-standing practice in security engineering,
  dependability, continuous delivery and site reliability engineering; the paper presents the individual
  defences as not new, and argues that what changes is that they become essential once agent-generated
  code is presumed possibly compromised.

## Related Terms

- [[DefinedTerm/two-gap-framework]]
- [[DefinedTerm/outer-loop]]
- [[DefinedTerm/human-in-the-loop]]
- [[DefinedTerm/sandboxing]]
- [[DefinedTerm/code-review-as-runtime-monitoring]]
