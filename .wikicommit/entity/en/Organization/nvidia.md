---
title: "NVIDIA"
type: "schema:Organization"
lang: en
tags: [security, ai-vendors]
sources:
  - type: url
    url: 'https://developer.nvidia.com/blog/mitigating-indirect-agents-md-injection-attacks-in-agentic-environments/'
    hash: sha256:12ff9c9af90eba6dbc268a3eab17b477eca5b0dc3c223d5537d795ba8b206089
  - type: url
    url: 'https://developer.nvidia.com/blog/securing-llm-systems-against-prompt-injection/'
    hash: sha256:3586be2459ba07a9385bba9fe13f4902a44075110ce0e0594535f80200bc5848
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The organization behind the NVIDIA AI Red Team, which tests AI and agentic systems adversarially, discloses what it finds to the affected vendors, and publishes the results on the NVIDIA Technical Blog alongside tooling for evaluating and constraining LLM behaviour."
  url: "https://developer.nvidia.com/"
---

NVIDIA enters this wiki through its AI security work. The team responsible is the NVIDIA AI Red Team, which tests AI and agentic systems adversarially and publishes what it finds on the NVIDIA Technical Blog.

## Activities & Products

The Red Team's practice, as visible in the work summarized here, is to construct a working attack against a real deployed system, disclose it to the affected vendor, and publish the finding together with the disclosure timeline and the vendor's response — including where the vendor declined to make changes. Its report of an [[DefinedTerm/indirect-agents-md-injection]] attack against [[SoftwareApplication/openai-codex]] followed that pattern, running from the initial report through the vendor's conclusion that the attack did not materially raise risk beyond compromised-dependency scenarios.

An earlier disclosure followed the same shape against [[SoftwareApplication/langchain]]: the Red Team identified and verified three vulnerabilities in that library's chains, all reachable through [[DefinedTerm/prompt-injection]], and published them once the affected components had been removed from the core library and with the maintainers' approval. That write-up records NVIDIA requesting a CVE itself after what it describes as a lack of immediate mitigation, and sets out the reasoning behind publishing — that the issues were severe but confined to specific chains, and that the technique was by then widely understood. It also generalizes beyond the finding, arguing that all model output should be treated as potentially malicious, which is the position developed under [[DefinedTerm/control-data-plane-confusion]].

Alongside the research, NVIDIA publishes tooling that its own security recommendations point to: garak, described there as an LLM vulnerability scanner for evaluating models against known prompt injection weaknesses, and NeMo Guardrails, for filtering and protecting LLM inputs and outputs. It also publishes training material in this area, including a self-paced course on adversarial machine learning, and has run AI red team training at Black Hat. Its NeMo offering is also named in that earlier write-up as a service for supporting LLM applications and integrations.
