---
title: "Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions"
type: "schema:ScholarlyArticle"
lang: en
tags: [mcp, security]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2503.23278'
    hash: sha256:e52e1f7bad32e6035ad5681f8775fce15eb345973f746db48783914ded82c6ab
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A systematic study of the Model Context Protocol from architectural and security perspectives, which defines a four-phase MCP server lifecycle decomposed into 16 key activities and builds a threat taxonomy of 16 scenarios across four attacker types, validated with proof-of-concept servers."
  author: ["Xinyi Hou", "Yanjie Zhao", "Shenao Wang", "Haoyu Wang"]
  datePublished: "2025-10"
  keywords: ["Model Context Protocol", "security", "threat taxonomy", "agentic AI"]
---

This paper, by Xinyi Hou, Yanjie Zhao, Shenao Wang and Haoyu Wang of Huazhong University of Science and Technology — with Haoyu Wang as corresponding author — presents what its authors describe as the first analysis of the [[DefinedTerm/model-context-protocol]] landscape, its emerging ecosystem, and its security risks. Its stated motivation is a gap rather than a dispute: MCP "has gained rapid adoption in the industry" but "is still largely unexplored in academia."

Its method is architectural first and security second. The authors define the full lifecycle of an MCP server from the server's perspective — derived, they say, from the official protocol documentation and a systematic analysis of actual MCP operational workflows — and then build the threat taxonomy on top of that lifecycle. The lifecycle has four sequential phases: **creation**, where the developer defines metadata, declares capabilities and implements the server; **deployment**, where the developer releases it to a public platform and users deploy it to a host while the client connects; **operation**, the runtime period of active user interaction; and **maintenance**, covering version iteration, configuration updates and continuous optimization.

## Key Contributions

- **A lifecycle-grounded threat taxonomy.** Sixteen threat scenarios are mapped across four attacker types. *Malicious developers*: namespace typosquatting, tool name conflict, preference manipulation, tool poisoning, rug pulls, cross-server shadowing and command injection. *External attackers*: installer spoofing and indirect prompt injection. *Malicious users*: credential theft, sandbox escape, tool chaining abuse and unauthorized access. *Security flaws*: vulnerable versions, privilege persistence and configuration drift.
- **Origin-based rather than phase-based classification.** The authors argue explicitly against assigning each risk to a single lifecycle phase, because "attacks like tool poisoning and rug pulls are introduced at the creation stage but triggered at operation." Analysing origins instead, they say, supports mitigation at the source.
- **Proof-of-concept validation.** The authors built PoC MCP servers for each identified risk type in an isolated environment, plus a custom MCP host on the official SDK to connect to them. They are explicit about the limits of this: the goal was to demonstrate feasibility, not to measure attack success rates or behavioural differences across base LLMs, which they leave to future work.
- **What distinguishes MCP from prior approaches.** The paper argues MCP "incorporates access control, capability negotiation, and schema discovery as protocol primitives, which distinguishes it from conventional function-calling mechanisms", addressing the limitations of manual API wiring, plugin interfaces and agent frameworks.
- **An ecosystem snapshot.** Adoption is tabulated by category and updated to September 2025, compiled by manual inspection of official documentation from the earliest MCP supporters and extended via community discussions and repository mining; the authors state it favours mature products with verifiable integration and acknowledge it is not exhaustive, and say the dataset will be maintained as a public repository. Official SDKs are recorded for TypeScript, Python, Java, Kotlin and C#, alongside community frameworks and server-generation platforms.
- **Lifecycle-specific recommendations by role.** Developers are advised to implement provenance verification, use version-controlled releases, and apply static analysis or digital signing before server registration; users to prefer trusted MCP collections, verify digital signatures at installation, and rely on sandboxed hosts; ecosystem maintainers to integrate automated version checks, integrity auditing and mandatory configuration validation into registries and collections.

## Notes

The paper's diagnosis of why the ecosystem is exposed is structural rather than technical. It identifies a **lack of centralized security oversight**: because servers are managed by independent developers there is no central authority to audit baselines or enforce compliance, producing inconsistent patching and irregular vulnerability management, and the absence of an official package management mechanism leads to version inconsistency and unverified updates. It also identifies **authentication and authorization gaps**, stating that MCP "currently lacks a standardized framework for authentication and authorization across clients and servers."

Two of its named threats extend the account this wiki records elsewhere. It places [[DefinedTerm/tool-poisoning]] under capability declaration by a malicious developer, alongside **rug pulls** — where a server's declared capabilities change after users have come to trust it — and **cross-server shadowing**, where malicious functionality is hidden behind another server's presence. Its treatment of **namespace typosquatting** notes that while typosquatting is familiar from package managers, plugin systems and cloud frameworks, it manifests differently under MCP, because both users at deployment and hosts at runtime select servers primarily on textual name and description rather than through an explicit manual choice.

The paper is a preprint carrying an ACM publication-rights notice with a publication date of October 2025, and states its ecosystem table was updated to September 2025 — both figures worth carrying forward, since the landscape it describes is explicitly a snapshot. See also [[Report/model-context-protocol-security]] and [[ScholarlyArticle/sok-security-and-safety-in-the-mcp-ecosystem]].
