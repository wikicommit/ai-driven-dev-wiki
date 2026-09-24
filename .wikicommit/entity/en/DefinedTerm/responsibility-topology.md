---
title: "Responsibility Topology"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-software-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.04630'
    hash: sha256:b89995b073da21f1e6d786f61dc056209cbca90ea6c15505e774483a51c9963e
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A classification proposed by Wang and Liu that sorts software organizations by how independent authority to accept residual risk is distributed — single-center, with one final responsibility anchor, or multi-anchor, where independently governed domains must jointly accept a change — independently of how many people or agents do the work."
---

Responsibility Topology is an organizational classification proposed in
[[ScholarlyArticle/software-engineering-in-the-agent-era]]. It describes how the authority to accept or
reject residual risk for a software baseline is distributed under an organization's currently effective
governance rules. Its unit is the **responsibility anchor**: a node traceable to a natural person or an
institutional role that has formal authority to accept or reject residual risk for a baseline or a key
responsibility domain, such as a product, security or architecture owner or a release authority. In the
paper's model an agent may be granted operational authority and recorded as an auditable executor, but
acceptance of residual risk stays with an identifiable human or institutional subject.

## Usage

The paper defines two basic forms. An organization is **single-center** when one final anchor can accept
or reject residual risk for the current baseline and can revoke or override the engineering authority of
other participants without changing the governance rules; a one-person company is given as a common
instance, but the form is not defined by headcount. An organization is **multi-anchor** when a baseline
has at least two anchors, each holding an acceptance right over a key domain that another anchor cannot
unilaterally revoke under normal governance; a change touching several such domains is accepted only
when all of the required anchors accept it.

Its central claim is that the classification is independent of how many humans, agents or
[[DefinedTerm/human-agent-cell]] units an organization has. A founder moving from one coding agent to
twenty concurrent ones changes the execution graph but not where final risk acceptance sits; adding
contractors, reviewers or specialists does not by itself create a new responsibility center; and two
engineers can form a multi-anchor organization if each holds an independent, non-revocable acceptance
right. The paper argues the distinction changes engineering behavior: under a single center, conflicting
evidence can ultimately be settled by one anchor, whereas under multiple anchors no single participant
can close all affected domains, so the organization must make explicit which facts are authoritative,
which changes invalidate other work and which anchors a given change requires. It also holds that
execution can finish while responsibility is not closed — every agent task done, yet one required anchor
not having accepted.

The paper says the topology cannot be read off job titles, repository write access or who merges most
changes, and proposes identifying it from three sources together: formal (de jure) governance, technical
enforcement such as CODEOWNERS, branch protection and deployment permissions, and de facto practice.
Where these disagree, the disagreement should be recorded rather than collapsed. It treats role matrices,
change-approval boards, CODEOWNERS and separation-of-duty rules as adjacent antecedents rather than
substitutes, since several approval steps can still sit under one final responsibility center.

## When It Applies

The classification is proposed for agentic software organizations in which execution capacity has become
elastic but risk acceptance has not. The paper separates two routes to a multi-anchor form: hard
governance triggers — regulation, professional qualification, separation of duties or independent
safety, security or compliance acceptance — which mandate it directly, and economic pressure, where a
new anchor becomes attractive only when the verification queue, attention load and continuity risk of a
single center justify an independently responsible domain. It warns that a shortage of mechanical review
capacity alone can be met by adding agents or reviewers without changing the topology. The construct is
one research group's proposal; the paper covers only the single-center and multi-anchor forms, leaves
hierarchical, federated and platform-mediated responsibility outside its claims, and states as a
falsifiable proposition that the topology may add no explanatory power once team size and risk are
controlled. It also notes that the phrase "responsibility topology" appears in an earlier design note
with a different, broader meaning.

## Related Terms

[[DefinedTerm/trustworthy-change]], [[DefinedTerm/human-agent-cell]]
