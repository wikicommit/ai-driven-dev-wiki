---
title: "Trustworthy Change"
type: "schema:DefinedTerm"
lang: en
aliases: ["TC"]
tags: [agentic-software-engineering, governance, change-management]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.04630'
    hash: sha256:b89995b073da21f1e6d786f61dc056209cbca90ea6c15505e774483a51c9963e
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A construct proposed by Wang and Liu for agentic software engineering: a single engineering object that follows one consequential software change across intent, delegated execution, verification, integration, acceptance and operation, so that it can be governed as a whole even when many agents, tasks and commits carry it out."
---

Trustworthy Change (TC) is the engineering object proposed in
[[ScholarlyArticle/software-engineering-in-the-agent-era]] to span the full lifecycle of one consequential
software change. The paper argues that no existing artifact does this once agents do the work: a commit
records code history but not the intent behind it, a pull request gathers discussion and tests but not
the resource envelope or authority under which the change is accepted, a change request records intent
but may be detached from the implementation's provenance, and a release comes too late to structure
delegation and verification. A TC acts as a cross-artifact identity for the change, answering what was
intended, under what authority and resources it was executed, what changed and where it came from, what
evidence supports the claims made about it, how it enters and survives operation, and who can accept the
remaining risk.

## Usage

The paper organizes a TC into six working dimensions — intent and specification, delegation and resource
envelope, change and provenance, evidence, integration and runtime state, and responsibility — and
stresses that these are traceable closure dimensions rather than six new documents; the information need
not live in one record so long as it stays traceable to the same change. It maps established change and
configuration management onto them: a change request becomes intent and specification, impact analysis
becomes specification refinement and risk analysis, review and testing become evidence, and change
approval becomes responsibility acceptance.

A TC moves through three states. The output of agent execution is a **Candidate**. A candidate becomes
**Eligible** once none of six failure conditions holds — undecided intent or specification, exceeded
authority or uncontrolled resources, untraceable provenance, a material claim without sufficient
evidence, insufficient integration or operational readiness, and a missing or invalid responsibility
path. It becomes **Accepted** only when it is eligible and every responsibility anchor whose acceptance is
mandatory for it has formally accepted its residual risk; only an accepted TC may modify the
authoritative baseline. A change that is eligible and whose required anchors exist but have not yet
signed off is described as acceptance-pending, not as a responsibility failure. Acceptance is relative to
a version, an evidence set and a time: if an authoritative fact the change depends on changes,
eligibility must be revalidated, and runtime facts that undermine the acceptance assumptions start a new
TC.

The paper also proposes using accepted TCs as an accounting boundary within a project — for example,
tokens or human attention per accepted change — on the argument that lines of code, commits, pull
requests and agent-task counts drift further from actual value once agents make producing them cheap. It
presents this as a within-project lifecycle measure, not a cross-project score of software value.

## When It Applies

The construct is aimed at settings where one semantic change is spread across many agent trajectories,
commits, tool calls, generated tests and state proposals, so that governing any single local artifact
loses the relationship between production, verification, configuration and responsibility. It assumes an
organization can name who holds authority to accept residual risk for a given domain, which the paper
handles through [[DefinedTerm/responsibility-topology]]. The paper's own framing is that it reorganizes
long-established change-management and accountability concerns rather than introducing them, that the
six-way decomposition is not claimed to be exhaustive or uniquely minimal, and that the framework is
theory construction whose empirical validity remains open; it states falsifiable propositions for testing
it but reports no evaluation.

## Related Terms

[[DefinedTerm/responsibility-topology]], [[DefinedTerm/human-agent-cell]],
[[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/spec-driven-development]]
