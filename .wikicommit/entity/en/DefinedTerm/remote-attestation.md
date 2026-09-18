---
title: "Remote Attestation"
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
  description: "A procedure by which a prover convinces a remote verifier that a public program executed inside a Trusted Execution Environment on given inputs and produced a given output, by way of a hardware-signed attestation document carrying the program's measurement and a commitment to the inputs and output."
---

Remote attestation is the procedure by which a prover convinces a verifier that a public program ran inside a [[DefinedTerm/trusted-execution-environment]] on a public input and optional secret inputs, and produced a particular output. It rests on three steps. When the program is loaded, the TEE records an enclave measurement — a hash that depends on the program binary. When proof is requested, the TEE's hardware- or firmware-backed attestation service produces an attestation document containing that measurement and a custom data commitment covering the input and the output, signed with a platform-protected attestation key whose certificate chain roots in the platform's trust anchor. The verifier then checks the signature chain using a verification key published by the TEE platform, confirms the reported measurement matches the measurement it computes itself for the open-source program, and confirms the commitment matches the hash of the input and output it was given.

## Usage

What a verifier learns from a valid attestation is threefold: the program that executed must be the exact one covered by the measurement; the input and output must be the genuine ones, because the program commits them into the attestation; and the document itself cannot be modified or fabricated by the prover, because it is signed under the platform's attestation key. Together these establish the integrity of the reported output under the attested program — without the verifier having to inspect the machine or trust the prover.

In AI the procedure has been applied to unforgeable model evaluation, to training-data valuation in marketplaces, and to verifiable inference that binds an output to a specific input and model. [[DefinedTerm/proof-of-guardrail]] applies it to agent safety: the measured program is a wrapper containing an open-source guardrail, so an attestation binding a response to that program is evidence the guardrail ran before the response was produced. What remote attestation does not establish is anything about the quality of the attested program — a correctly attested guardrail can still be wrong or jailbroken, which is why [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]] is explicit that proof of execution is not proof of safety.

## Related Terms

[[DefinedTerm/trusted-execution-environment]], [[DefinedTerm/proof-of-guardrail]], [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]]
