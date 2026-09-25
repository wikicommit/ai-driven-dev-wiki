---
title: "LlamaFirewall"
type: "schema:SoftwareApplication"
lang: en
tags: [security, prompt-injection, guardrails, agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.03574'
    hash: sha256:0900d1fe1156d88f445d11ba287178f12bfb25c5db87cc4a10cea036ac7a7ac5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source, system-level guardrail framework from Meta for LLM-powered agents, combining a jailbreak classifier, a chain-of-thought alignment auditor and a static analyzer for generated code in one policy engine."
  applicationCategory: "Security guardrail framework for LLM agents"
  featureList: "PromptGuard 2 jailbreak detection (86M and 22M models); AlignmentCheck chain-of-thought auditing for goal hijacking and indirect prompt injection (experimental); CodeShield static analysis of generated code with Semgrep and regex rules; custom regex and LLM-prompt scanners; custom pipelines and conditional remediation"
---

LlamaFirewall is an open-source, security-focused guardrail framework designed to serve as a final
layer of defense against security risks associated with AI agents, such as
[[DefinedTerm/prompt-injection]], agent misalignment and insecure code. It is introduced in
[[ScholarlyArticle/llamafirewall-an-open-source-guardrail-system-for-building-secure-ai-agents]],
which states that it is used in production at Meta and releases it as open-source software so that
others can use and extend it. Its code is published in Meta's PurpleLlama repository at
<https://github.com/meta-llama/PurpleLlama/tree/main/LlamaFirewall>.

## Capabilities

LlamaFirewall brings several scanners together in a unified policy engine, in which developers can
construct custom pipelines, define conditional remediation strategies and plug in new detectors. It
ships three guardrails:

- **PromptGuard 2** is a lightweight classifier, built on DeBERTa models, that detects explicit
  [[DefinedTerm/jailbreaking]] techniques such as instruction overrides and token injection in user
  prompts and untrusted data. It comes in an 86M-parameter version based on mDeBERTa-base and a
  lower-latency 22M-parameter version, and can run locally on CPU or GPU.
- **AlignmentCheck** is an experimental auditor that uses a capable LLM with a few-shot prompt to
  compare an agent's selected action, and its reasoning so far, with the user's original goal, and
  flags actions that suggest [[DefinedTerm/indirect-prompt-injection]] or other goal hijacking.
- **CodeShield** is an online static-analysis engine for LLM-generated code that supports Semgrep
  and regex-based rules, uses a fast pattern-matching tier and escalates flagged inputs to a deeper
  analysis, and covers over 50 Common Weakness Enumerations. It was previously released as part of
  the Llama 3 launch.

The framework also includes customizable scanners that let any developer who can write a regular
expression or an LLM prompt update an agent's guardrails. In the paper's scenarios, PromptGuard
drops injected web content before it enters the agent's context, AlignmentCheck halts execution when
the agent's behavior drifts from the user's task, and CodeShield rejects a patch containing an
insecure SQL query until the agent adopts a secure pattern.

## Adoption & Ecosystem

The paper describes LlamaFirewall as used in production at Meta and presents it as a collaborative
foundation for sharing policies and detectors, in the way Snort, Zeek or Sigma are used in
traditional security. It compares the framework with [[SoftwareApplication/nemo-guardrails]],
[[SoftwareApplication/guardrails-ai]] and Invariant Labs' framework, and evaluates it on
[[Dataset/agentdojo]]. The authors plan to extend it to multimodal agents, reduce AlignmentCheck's
latency and broaden its threat coverage to behaviors such as malicious code execution and unsafe
tool use. It is one implementation of the broader practice of [[DefinedTerm/guardrails]] for
agents.
