---
title: "Systematization of Knowledge: Security and Safety in the Model Context Protocol Ecosystem"
type: "schema:ScholarlyArticle"
lang: en
tags: [mcp, security]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.08290'
    hash: sha256:41c224d999eee798d882744ca794c7590e437175f2cbba1d8a6ca07317125f28
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A Systematization of Knowledge paper arguing that in the Model Context Protocol the boundary between adversarial security threats and epistemic safety hazards dissolves, so that hallucinations can become breaches and breaches can become honest-but-unauthorized actions. It taxonomises the security risks by impact and execution phase, maps its four safety categories onto MCP primitives and risk types, and analyses the Resources, Prompts and Tools primitives structurally."
  author: ["Shiva Gaire", "Srijan Gyawali", "Saroj Mishra", "Suman Niroula", "Dilip Thakur", "Umesh Yadav"]
  datePublished: "2025-12"
  keywords: ["Model Context Protocol", "Agentic AI", "LLM Security", "AI Safety", "Indirect Prompt Injection", "Tool Poisoning", "Zero Trust Architecture"]
---

This Systematization of Knowledge paper — by Shiva Gaire, Srijan Gyawali, Saroj Mishra, Suman Niroula, Dilip Thakur and Umesh Yadav, who state that all authors contributed equally, across Tribhuvan University, the University of North Dakota, Youngstown State University, the University of Missouri and the University of Toledo — takes [[DefinedTerm/model-context-protocol]] as "the de facto standard for connecting Large Language Models (LLMs) to external data and tools, effectively functioning as the 'USB-C for Agentic AI.'" Its central claim is not that MCP has bugs but that it collapses a distinction security engineering normally relies on.

That claim is the paper's own framing of the problem: in traditional software, "security protects against malicious adversaries (e.g., SQL injection), while safety protects against unintended system behaviors (e.g., race conditions). In MCP, this distinction blurs." Its worked illustration runs both ways. A security breach — an attacker injecting a malicious document into a company's knowledge base — triggers a safety failure in which "the model honestly but mistakenly believes it is authorized to delete a database". Conversely a safety failure such as hallucinating a tool's parameters can produce a security breach in which sensitive data is exfiltrated to a public log. The authors argue current defences are ill-equipped for this duality because "traditional firewalls cannot inspect the semantic intent of a JSON-RPC message, and LLM safety filters cannot see the downstream consequences of a tool execution", and conclude that securing MCP "requires a unified threat model that treats context availability and execution privilege as inextricably linked variables."

## Key Contributions

The paper states four contributions:

- **A unified vulnerability taxonomy** distinguishing *adversarial security threats* — the examples given being tool masquerading and context poisoning — from *epistemic safety hazards*, such as alignment failures in distributed tool delegation.
- **A structural analysis of MCP's primitives**, arguing that decoupling "Context" (Resources) from "Action" (Tools) creates new vulnerability classes, including **cross-primitive escalation**, where read-only access is weaponized to trigger write-actions.
- **A survey of emerging defenses**, moving beyond prompt engineering to architectural solutions, naming the Enhanced Tool Definition Interface (ETDI) for cryptographic provenance and kernel-level session isolation.
- **Forensic case studies** reconstructing real-world incidents, the Supabase data leak among them, to derive lessons for enterprise deployment.

Its scope is deliberately narrowed to risks the MCP ecosystem itself introduces: the protocol primitives, topology risks arising from distributed Host–Client–Server interactions including supply chain risks in open tool registries, and their intersection — explicitly excluding general LLM adversarial attacks such as weight poisoning unless they directly affect protocol integrity or execution flow.

The safety taxonomy is organised in four parts, each mapped to a primary primitive and a risk type: **epistemic integrity** (Resources — grounding or hallucination from fragmented or low-fidelity retrieval); **adversarial resilience** (Resources and Prompts — hidden instructions or prompt injections embedded in external data); **alignment consistency** (Host model and tool policies — policy conflicts or goal-pursuit misalignment leading to harmful delegation); and **systemic governance** (human oversight and regulation — human-in-the-loop failures, accountability gaps, dual-use misuse). Its security-side categories include cross-session contamination, supply-chain and model-switch attacks (rug pulls, server impersonation, unauthorized tool mutation), protocol abuse and name collisions (command overlap, confused-deputy access), and denial-of-service and resource exhaustion.

## Notes

The paper's account of *why* MCP amplifies these risks is architectural rather than incidental. Because MCP separates responsibilities across three primitives operating in distinct trust domains, and because those primitives interact across independent Hosts, Clients and Servers, "the traditional 'single safety perimeter' dissolves", so a failure in one primitive — low-fidelity contextual retrieval, for instance — can escalate into a harmful action executed by another. The authors draw an explicit parallel to retrieval-augmented generation, where "epistemic errors in upstream retrieval frequently propagate into downstream reasoning", and argue the propagation is amplified under MCP because the protocol can perform real-world actions, so context errors become operational harm.

Its diagnosis of the present state is that "MCP adoption is rapid, yet governance and standardization lag behind": many clients do not expose full tool specifications, request permissions transparently, or enforce strict boundaries between context and execution, while third-party installers, shared contexts, absent authentication and unverified tool updates magnify exposure. The combined safeguards it calls for are authentication, sandboxing, provenance checks, tool validation, session isolation, continuous monitoring and least-privilege enforcement.

The conclusion is a claim about how the protocol should be understood, not just secured: MCP cannot be treated "merely as an API or merely as an LLM", because the coupling of Context and Action creates a "semantic attack surface" where indirect prompt injection escalates into real-world operational damage and hallucinations can result in security breaches. The authors state that existing defenses "are necessary but insufficient", and that what is needed is cryptographic provenance, runtime intent verification and rigorous capability-based isolation — with responsibility shared between protocol designers, who "must bake identity and verification into the core specification", tool developers, who must "treat model inputs as untrusted user data", and organizations, which must monitor agentic behaviour continuously.

This is a preprint (version 2, December 2025) and its authors present it as "the first academic survey to systematize the risks of the Model Context Protocol". See also [[ScholarlyArticle/mcp-landscape-security-threats]], [[Report/model-context-protocol-security]], [[DefinedTerm/tool-poisoning]] and [[DefinedTerm/indirect-prompt-injection]].
