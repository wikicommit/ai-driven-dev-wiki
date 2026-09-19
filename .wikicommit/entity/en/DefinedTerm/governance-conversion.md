---
title: "Governance Conversion"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agentic-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01087'
    hash: sha256:8090aa5b3991512f26cd76d8d9f7894401756bc4b97c5ba42d641852854dd0bc
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The conversion of observed agentic failure patterns into explicit, durable governance that constrains subsequent agent work — an ex-post process of discovering controls from failures that only become visible once agents are working at speed."
---

Governance conversion is the process by which recurring failures produced by AI coding agents are turned into explicit, durable governance that constrains subsequent agent work. The term is proposed by Davis and colleagues in [[ScholarlyArticle/cheap-code-costly-judgment]], where it names the central mechanism of a candidate middle-range theory: agentic velocity exposes a structural failure class, a human interprets it as a structural problem rather than an isolated defect, and that interpretation is encoded into the engineering environment so that later agents inherit a narrower and more explicit action space. The paper's shorthand for the loop is "failure → governance", and it is described as non-terminating, because rising velocity keeps surfacing failure classes that prior governance did not address.

## Usage

The paper sets the term against *ex-ante* governance, which it attributes to existing governance-centric accounts: controls deduced in advance from obligations that are already known, such as regulations translated into runtime guardrails. Governance conversion is presented as the complementary *ex-post* axis — inducing controls from failures discovered during agentic work — and the authors are explicit that they found ex-ante controls necessary but not sufficient, and that both are needed.

The authors describe a five-step process: velocity exposes failure; the architect distinguishes local defects from recurring structural failure classes; governance is encoded, either probabilistically (an agent harness) or deterministically (a type system); subsequent agent work is constrained by it; and governability compounds, as repeated conversions increase the environment's capacity to absorb future agent work. Two worked examples are given from the case. In one, agent-run architectural audits stopped scaling as the codebase grew, and the response was architectural: the audit zones were reified as a typed component catalog, converting agent-mediated audit into deterministic enforcement. In the other, agents repeatedly violated constraints they had never been told about, and the response was a control: dispatch-time constraint slicing that injected the rules governing a change's target files into the agent's brief before it edited code.

## When It Applies

The process presupposes that agents are already producing changes fast enough for failures to recur and cluster — the paper observes that agentic velocity surfaced related failures in dense succession that would conventionally have appeared far apart in time, and that this proximity was itself what let the architect perceive an architectural gap. It also assumes the human has the standing to act: the paper names *authority* as a moderator, arguing that where authority is divided across teams, owners, review boards and deployment processes, the same failure signal may produce only local patches rather than shared governance. A second moderator, *capability-fit*, holds that outcomes depend on the match between agent capability and human judgment.

Its characteristic failure is to read a failure as a local defect and patch it, rather than as evidence of a missing abstraction or an underspecified interface. The paper frames the discriminating judgment as not merely whether an agent-produced change is acceptable, but whether a failure reveals missing governance — and offers, as an engineering disposition drawn from one incident, that an engineer should "assume that you are the problem", relocating the locus of difficulty from model competence to their own capacity to frame, decompose and constrain.

The term is not an established or widely agreed one: it is proposed in a single 2026 paper, on the evidence of a single 12-week, one-person case study, and the authors present it explicitly as theory-building rather than theory-testing, offering falsifiable propositions for others to test rather than claiming prevalence.

## Related Terms

[[DefinedTerm/governed-engineering-environment]], [[DefinedTerm/agentic-se-process-models]], [[DefinedTerm/guardrails]], [[DefinedTerm/harness-engineering]]
