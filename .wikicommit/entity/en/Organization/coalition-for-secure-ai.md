---
title: "Coalition for Secure AI"
type: "schema:Organization"
lang: en
tags: [security, governance]
sources:
  - type: url
    url: 'https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf'
    hash: sha256:d5ea586dbd65785c34ba7afa769d56a4d1bcc77eb7876b7578edff5516c979a5
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Describes itself as an OASIS Open Project, abbreviated CoSAI, bringing together AI and security experts from industry-leading organizations to share best practices for secure AI deployment. Its Workstream 4 covers secure design patterns for agentic systems and produced a threat model for the Model Context Protocol."
  url: "https://www.coalitionforsecureai.org/"
---

The Coalition for Secure AI (CoSAI) describes itself as an OASIS Open Project "bringing together an open ecosystem of AI and security experts from industry-leading organizations", dedicated to sharing best practices for secure AI deployment and to collaborating on AI security research and product development. Its stated scope is deliberately narrow: the secure building, integration, deployment and operation of AI systems, with an emphasis on mitigating security risks unique to AI technologies.

The exclusions are explicit. CoSAI treats other aspects of trustworthy AI as important but out of scope — ethics, fairness, explainability, bias detection, safety, consumer privacy, misinformation, hallucinations, deep fakes, and content safety concerns such as hateful or abusive content, malware or phishing generation. What remains is safeguarding AI systems against unauthorized access, tampering or misuse.

## History

The source ingested here does not cover CoSAI's founding date or how it came to be an OASIS project; it documents the organization's stated purpose and one workstream's output.

## Activities & Products

Work is organised into numbered workstreams. Workstream 4, Secure Design Patterns for Agentic Systems, produced [[Report/model-context-protocol-security]], approved by the CoSAI Project Governing Board on 8 January 2026, which organises nearly forty threats to [[DefinedTerm/model-context-protocol]] deployments into twelve categories. That report states it coordinates with CoSAI's Software Supply Chain Security workstream, and routes legal and regulatory compliance questions to Workstream 3, AI Risk Governance; it also says the authors are collaborating with [[Organization/anthropic]] and the MCP maintainer community to keep recommendations implementable, and promises follow-on papers with reference implementations for specific mitigation controls.

The MCP security report names workstream leads, editors, contributors and technical steering committee co-chairs affiliated with IBM, Intel, NVIDIA, Anthropic, Google, Cisco, Red Hat, Amazon, Dell, PayPal, ServiceNow, Trend Micro, Wiz, ProCap360 and Adversa AI, among others.

The project also publishes a policy on AI-assisted drafting of its own documents. Its stated position is that contributions are actions performed by humans who remain responsible for the content under their signed OASIS contributor licence agreement; it recommends reputable AI systems to lower the risk of incorporating infringing material, places responsibility for IP clearance on the individual who prompts the system, aims to document substantial AI use including prompts and system used, and mandates human-reviewed or -edited final outputs with a quality control process checking for errors, inconsistencies and potential biases.
