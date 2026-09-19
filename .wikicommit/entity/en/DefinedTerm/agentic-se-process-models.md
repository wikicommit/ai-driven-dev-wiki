---
title: "Process Models for Agentic Software Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agentic-engineering, governance, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01087'
    hash: sha256:8090aa5b3991512f26cd76d8d9f7894401756bc4b97c5ba42d641852854dd0bc
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Davis and colleagues' three-way organization of prior accounts of how agentic software work is arranged — velocity-centric, oversight-centric and governance-centric — distinguished by what each prioritizes and how each handles reliability."
---

"Velocity-centric", "oversight-centric" and "governance-centric" are the three process models into which Davis and colleagues organize prior accounts of agentic software engineering in [[ScholarlyArticle/cheap-code-costly-judgment]]. They are distinguished by what each prioritizes and how each handles reliability: the first organizes agent labour to increase throughput while leaving its reliability mechanisms underspecified, the second puts human attention inside the implementation loop, and the third defines a governed engineering environment before agent work begins. The framing is introduced to state a shared problem — how to ensure quality using fast, unreliable tools — and to argue that the dominant models trade velocity against quality rather than resolving the tension.

## Usage

The **velocity-centric** model gives agents autonomy and may orchestrate multi-agent workflows to increase throughput, for example by assigning agents engineering roles such as planner, developer and tester. The paper's objection is that process resemblance is not control: agents can imitate the form of software work without producing quality output, and lack accountability, organizational context and professional judgment. Its reliability mechanisms are left underspecified, amounting at most to soft guardrails around the agents.

The **oversight-centric** model treats agents as useful but unreliable assistants, so human engineers stay near the implementation loop, prompting bounded work and inspecting output. The paper credits it with recognizing that agentic output requires oversight, but identifies its limitation as the control mechanism itself being human attention: at high implementation volume, oversight becomes the throughput bottleneck. The authors group trace-based agent improvement — analyzing execution histories to distill reusable lessons into skills and harness changes — as a related line of work.

The **governance-centric** model, which the paper describes as emerging, holds that agents create product, organizational and legal risks as they act, and proposes policy-to-control methods: starting from known obligations such as regulations and deducing corresponding agent controls, for instance as runtime guardrails. The paper adopts this model's framing but argues it is incomplete because its techniques are *ex ante*, deriving controls from obligations known before agents act; its own contribution, [[DefinedTerm/governance-conversion]], is offered as the complementary ex-post process of inducing controls from failures discovered during agentic work.

The authors' own position sits within the third model while extending it: they report using ex-ante controls — conformance checkers, content preservation and provenance for auditability, commodity lints — and finding them necessary but not sufficient. In the case they study, the engineer at its centre deliberately departed from the oversight-centric model, inspecting almost no agent-produced code and relying instead on a [[DefinedTerm/governed-engineering-environment]].

## Related Terms

[[DefinedTerm/governance-conversion]], [[DefinedTerm/governed-engineering-environment]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/guardrails]]
