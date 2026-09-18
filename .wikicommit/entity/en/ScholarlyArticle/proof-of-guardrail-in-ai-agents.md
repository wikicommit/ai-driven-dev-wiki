---
title: "Proof-of-Guardrail in AI Agents and What (Not) to Trust from It"
type: "schema:ScholarlyArticle"
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
  description: "A workshop paper proposing proof-of-guardrail, a system that uses a Trusted Execution Environment and remote attestation to give users cryptographic, offline-verifiable proof that an agent response was generated after a declared open-source guardrail executed, while keeping the developer's agent implementation private."
  author: ["Xisen Jin", "Michael Duan", "Qin Lin", "Aaron Chan", "Zhenglun Chen", "Junyi Du", "Xiang Ren"]
  datePublished: "2026"
  keywords: ["proof-of-guardrail", "trusted execution environment", "remote attestation", "AI agent safety", "guardrails", "confidential computing"]
---

This paper addresses a trust gap that appears when users access an AI agent deployed remotely by someone else — a bot on an online platform, for example. Such users cannot verify whether the agent actually runs the safety guardrail its developer claims, which the authors describe as a threat where safety measures are falsely advertised. Two existing remedies are argued to be unworkable: mandating that developers run agents openly for public audit conflicts with agent implementations such as system prompts being proprietary knowledge, and relying on a trusted third-party auditor does not hold in decentralized or cross-platform deployments where no universally trusted auditor exists.

The proposal, [[DefinedTerm/proof-of-guardrail]], is a system that lets a developer produce cryptographic proof that a response was generated after a specific open-source guardrail ran. A wrapper program bundles the public guardrail and its configuration and mediates all of the agent's inputs, outputs and tool calls; it is loaded into a [[DefinedTerm/trusted-execution-environment]] and measured at initialization, and the developer's private agent is then supplied to it as a secret input. For each user input the wrapper runs the guarded agent and obtains a signed attestation document containing the enclave measurement and a commitment to the input and response, which any user can verify offline against the open-source wrapper and the TEE platform's verification key. Because the agent itself is a secret input rather than part of the measured program, it stays private; because the attestation is signed by the platform's [[DefinedTerm/remote-attestation]] key, it cannot be forged or tampered with even when the input, response and attestation are all public.

The authors implement the system for [[SoftwareApplication/openclaw]] agents on AWS Nitro Enclaves and report it to be feasible but costly: guardrail execution and response generation inside the TEE carry a 25% to 38% latency overhead, attestation generation adds roughly 100ms, and the instance type required is 18.5 times more expensive per hour than a non-TEE instance they consider adequate for the same agent. Their central caution is that the property proved is narrower than it sounds — a valid proof establishes that the guardrail executed, not that the response is safe — and they argue the system should not be interpreted or advertised as proof-of-safety.

## Key Points

- The threat model is a developer who skips or misconfigures a guardrail while claiming to run it, returning a response generated without the declared guardrail or with a modified version of it.
- The system's three stated desiderata are computational integrity of guardrail execution, confidentiality of the developer's agent, and no assumption that the user input or the response is confidential from the developer.
- The developer's agent is passed to the measured wrapper program as a secret input, so the attestation covers the guardrail and wrapper without exposing the agent implementation.
- Trust is anchored in the cloud provider already used for deployment — the authors state they trust the AWS Nitro hypervisor to measure code correctly and protect the TEE's private keys — which they present as removing the need to trust an additional third-party auditing organization.
- Three simulated attacks were all detected during verification: modifying a line of the claimed guardrail's code produced a measurement mismatch (10 of 10 runs), modifying a random byte of the attestation document produced an invalid signature (100 of 100), and modifying the response shown to the user produced a commitment hash mismatch (100 of 100).
- Measured latency overhead against a non-TEE baseline ranged from 24.8% to 38.0% across the four tasks tested, with attestation generation adding 97.8ms and user-side verification taking 5.1ms.
- The cost comparison rests on one pairing: an m5.xlarge instance at $0.192 per hour against a t3.micro at $0.0104 per hour, the larger instance being needed because the Nitro Enclave requires the entire guardrail runtime to reside in memory.
- The two guardrails used to obtain these figures were themselves imperfect on the datasets tested — a content-safety guardrail scored 0.56 F1 on its unsafe class, and a fact-checking guardrail scored 0.76 and 0.67 F1 on its non-factual and factual classes — which the authors offer as direct evidence that proof of execution is not proof of safety.
- Because the system requires the guardrail to be open-source, the authors note that a malicious developer can mount jailbreak attacks against that guardrail, and give the example of a financial-news agent presenting a valid proof while still misleading users with false advice.
- The authors state that the measured wrapper program must itself be free of vulnerabilities that would let the unmeasured agent bypass the guardrail, and suggest restricting the late-injected agent to non-executable prompt artifacts as one mitigation.

## Notes

The authors position the work against attestable audits, which they describe as the most relevant prior work and as ensuring that a model a user communicates with has provably passed security audits; they claim proof-of-guardrail's advantage is flexibility, since developers can adopt empirically validated guardrails without rerunning full audits while still producing cryptographic proof of enforcement. They are explicit that improving guardrail accuracy is out of scope and complementary to proving guardrail execution.

To reduce the residual risks they identify, the authors advocate that verifiers require proofs for best-practice open-source guardrails and wrapper programs, and argue that establishing what counts as best-practice is a community process driven by research, shared benchmarks and red-teaming results — on the reasoning that most casual agent users will not evaluate guardrail quality from an implementation alone. Their impact statement frames the system as benefiting honest developers in a low-trust market while acknowledging it can introduce a misalignment of trust, since a valid proof establishes guardrail execution but not actual agent safety.
