---
title: "agentic code review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, multi-agent, human-in-the-loop, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A proposed end-to-end model of code review in which specialised agents handle each stage of the pull-request lifecycle and carry context across stage boundaries, while the human reviewer moves from manual inspector to supervisory operator at human-controlled quality gates."
  termCode: ""
  inDefinedTermSet: ""
---

Agentic code review is the model proposed in [[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai]] in which reviewers "transition from manual inspectors into supervisory operators of agents." Its defining move is scope: rather than automating one stage of review, it treats review effectiveness as an outcome of the full pull-request lifecycle and builds a framework that carries context across stage boundaries. This is a vision proposed by that paper, not an implemented or evaluated system.

The argument for taking the whole lifecycle at once is that stage-level improvements do not compose. A helpful review comment still depends on a PR whose rationale was written down; reviewer matching relies on behavioural context reaching the reviewer; future changes depend on lessons from prior reviews having been recorded. Those dependencies cross tool boundaries, so improving any single stage in isolation leaves the chain broken elsewhere.

## Usage

**Five stages, each with a human gate.** PR Creation generates the title, description and issue links and runs a first automated pass, with the author verifying before formal submission. PR Augmentation runs four analyses concurrently — requirement alignment, bug proneness, sandboxed runtime execution, and cross-module impact — and synthesises them into a structured summary of verifiable claims. Reviewer Selection ranks candidates on expertise, review history, current workload and familiarity with the change. AI-Assisted Code Review puts a PR Review Agent in front of the reviewer as a natural-language interface to those analyses. PR Retrospective captures review summaries as repository memory and computes process metrics.

**The stated purpose of the human gates is error containment, not ceremony.** Because outputs of upstream agents feed downstream tasks, an early hallucination or misclassification propagates: the paper's worked example is a misread authorisation change producing a wrong description, which leads reviewer selection to assign a backend rather than a security specialist. The gates are described as "natural firewalls against error accumulation," with the author's verification of a generated description breaking the chain early.

**The paper is explicit that those gates are not self-sufficient.** It argues that assuming human-in-the-loop mechanisms are inherently robust is a fundamental flaw, because automation bias makes an author likely to accept an authoritative-looking artefact without checking it — and one unverified issue link then cascades through augmentation into reviewer assignment. Its stated requirement is explicit quality indicators surfaced to the human rather than assumed reliance.

**Two mechanisms distinguish it from a chatbot bolted onto review.** The [[DefinedTerm/diff-map]] anchors every reviewer-visible claim to a source-code location and to the report that produced it, which the paper describes as turning review from a memory exercise into a verifiable retrieval task. And two measurement agents operate on the *reviewer's own* output rather than the code: a Toxicity Measurement Agent evaluating feedback as it is composed, on the grounds that toxic comments deter future contribution, and a Usefulness Measurement Agent identifying superficial remarks to mitigate bikeshedding.

**Its named risk to team capability** is that review's non-defect purposes erode. The paper notes that knowledge transfer and team awareness are equally critical outcomes of review, and that routing explanation through an agent can incentivise reviewers to bypass manual inspection and displace implicit mentoring between senior and junior developers. Its proposed mitigation is a mandatory human critique checkpoint before merge is unblocked.

## Related Terms

Agentic code review is a specific architecture for deploying a [[DefinedTerm/code-review-agent]] across a whole workflow rather than at one stage, and it is proposed as a response to the [[DefinedTerm/verification-bottleneck]]. Structurally it is an instance of [[DefinedTerm/multi-agent-orchestration]] with [[DefinedTerm/subagents]] under a coordinating agent, and its accumulated-error concern is the same failure mode that discipline generally guards against.
