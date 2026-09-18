---
title: "Trusted Execution Environment (TEE)"
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
  description: "A hardware-backed isolation mechanism that runs sensitive code in a protected area and can produce a cryptographically signed statement describing the exact code and configuration that ran, allowing a remote party to check what executed without inspecting the machine."
---

A Trusted Execution Environment (TEE) is a hardware-backed isolation mechanism that lets sensitive code run in a protected area of a machine. Beyond keeping the data inside it confidential, a TEE can support remote attestation: it executes code in a hardware-enforced isolated environment — an enclave — and produces a cryptographically signed statement describing the exact code and configuration that ran, so a remote party can be convinced the program is running as expected rather than in a modified form, even though that party cannot inspect the machine directly. When a program is loaded, the TEE records an enclave measurement, a hash derived from the program binary, which is what later identifies to a verifier exactly which code executed.

## Usage

TEEs are already in wide use outside AI: mobile devices use them for biometric authentication and for protecting cryptographic keys, and cloud providers offer them under the name confidential computing to protect customer workloads. Within AI, their confidentiality property has been applied to multi-party and federated learning and to confidential model inference, keeping inputs, training data and model weights secret. A separate line of work leans on their integrity property instead, developing verifiable and unforgeable model property cards that cryptographically prove a model's performance, fairness or safety metrics — presented as a computationally efficient alternative to zero-knowledge proofs.

In agent systems the same integrity property is what [[DefinedTerm/proof-of-guardrail]] builds on: a wrapper program containing the guardrail is loaded into an enclave and measured, the developer's agent is supplied afterwards as a secret input, and the resulting attestation lets any user confirm which guardrail code ran. Using a TEE this way means trusting the platform vendor — in the implementation reported in [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]], AWS Nitro Enclaves was used and the authors state they trust the provider's hypervisor to measure code correctly and to protect the TEE's private keys. The isolation also has a practical cost, since the enclave must hold the whole runtime it executes, including a kernel and dependencies, in memory.

## Related Terms

[[DefinedTerm/remote-attestation]], [[DefinedTerm/proof-of-guardrail]], [[DefinedTerm/sandboxing]], [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]]
