---
title: "Proof-of-Guardrail"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05786'
    hash: sha256:88932db1701d24427b3c99749daed01d7948095ccb89ce4e1db8c125b09b160f
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A system, proposed by Jin et al., in which an AI agent developer produces a cryptographic attestation that a response was generated after a specific open-source guardrail executed, verifiable offline by any user without the developer revealing the agent implementation."
---

Proof-of-guardrail is a system, proposed by Jin et al. in [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]], that lets the developer of a remotely deployed AI agent produce cryptographic proof that a given response was generated after a specific open-source guardrail executed. A wrapper program bundles the public guardrail and its configuration and mediates all of the agent's inputs, outputs and tool calls; that wrapper is loaded into a [[DefinedTerm/trusted-execution-environment]] and measured at initialization, and the developer's private agent is supplied to it afterwards as a secret input. For each user input the wrapper runs the guarded agent and requests an attestation document that carries the enclave measurement together with a commitment to the input and the response, and returns both the response and that document to the user, who can verify it offline using the open-source wrapper, the input and response, and the TEE platform's verification key. The property this establishes is deliberately narrow: it shows that the declared guardrail ran, not that what the guardrail let through is safe.

## Usage

The term names a response to a specific trust gap — a user interacting with an agent someone else operates, such as a bot on a messaging platform, cannot tell whether the [[DefinedTerm/guardrails]] the operator advertises were actually applied. Proof-of-guardrail is intended for that setting rather than for agents a user runs themselves. It is designed so that the developer's agent implementation, which the paper treats as proprietary knowledge, never has to be disclosed to users or to a third-party auditor, and so that no universally trusted auditor is required — which the authors argue matters in decentralized or cross-platform deployments where no such auditor exists. A fresh attestation is generated for each user input, and in the authors' demonstration the user requests one through the chat itself.

## When It Applies

The system assumes a guardrail that is open-source, since users verify the attestation by computing the expected measurement of that code themselves, and it assumes the TEE platform's hardware and firmware are trustworthy — the authors state they trust the cloud provider to measure code correctly and to protect the TEE's private keys, and present anchoring trust in the provider already used for deployment as removing the need to trust an additional auditing organization. It is a system whose cost is real rather than nominal: the authors measure a 25% to 38% latency overhead on guardrail execution and response generation, about 100ms more for attestation generation, and an 18.5-fold increase in hourly instance cost, because the enclave must hold the entire guardrail runtime in memory.

Two failure modes are identified by the authors themselves. Because the guardrail must be open-source, a malicious developer can jailbreak it and still present a valid proof — their example is a financial-news agent that attests correctly while giving misleading advice — and the guardrails used in their own evaluation were measurably imperfect. Separately, the measured wrapper program must contain no vulnerability that would let the unmeasured agent bypass the guardrail, for instance by executing arbitrary commands inside the enclave; restricting the late-injected agent to non-executable prompt artifacts is offered as a mitigation. For these reasons the authors state that proof-of-guardrail should not be interpreted or advertised as proof-of-safety, and that there remains a gap between it and true safety. The proposal rests on a single paper with an end-to-end implementation and runtime measurements rather than on established practice, and its authors advocate that verifiers require proofs for best-practice open-source guardrails, while treating the definition of best-practice as an open community process.

## Related Terms

[[ScholarlyArticle/proof-of-guardrail-in-ai-agents]], [[DefinedTerm/trusted-execution-environment]], [[DefinedTerm/remote-attestation]], [[DefinedTerm/guardrails]]
