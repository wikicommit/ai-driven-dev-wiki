---
title: "Model Context Protocol"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, terminology]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/model-context-protocol'
    hash: sha256:e33f7635c7066ce5080d114a7e486537f8686757e5de41c7f480e0acd0b28da4
  - type: url
    url: 'https://modelcontextprotocol.io/docs/2026-07-28/getting-started/intro'
    hash: sha256:d00ecc4badcc348fb73f085a87978282ee31c71d9bc0c061f463b031f05efafb
  - type: url
    url: 'https://modelcontextprotocol.io/specification/2025-11-25'
    hash: sha256:ba34900db35b2b5c7a1c1a00b70996aa4a6221f75965f70b770811ffaf304f21
  - type: url
    url: 'https://github.com/modelcontextprotocol/modelcontextprotocol'
    hash: sha256:d1d561c4ad5035e4f236db33e497f73d2d3238f0a31f6ee29b37d5ac87c1d11c
  - type: url
    url: 'https://en.wikipedia.org/wiki/Model_Context_Protocol'
    hash: sha256:f114caf967b13aa97382a0bea6ed771c920c8c79930883437e9a34df46e9c542
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8
  - type: url
    url: 'https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/'
    hash: sha256:75eb803ce303bb04ab925d41277a47055f64ccef01e15cfc3d3a0ed89110bbe6
  - type: url
    url: 'https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf'
    hash: sha256:d5ea586dbd65785c34ba7afa769d56a4d1bcc77eb7876b7578edff5516c979a5
  - type: url
    url: 'https://arxiv.org/pdf/2503.23278'
    hash: sha256:e52e1f7bad32e6035ad5681f8775fce15eb345973f746db48783914ded82c6ab
  - type: url
    url: 'https://arxiv.org/pdf/2512.08290'
    hash: sha256:41c224d999eee798d882744ca794c7590e437175f2cbba1d8a6ca07317125f28
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open standard, introduced by Anthropic in November 2024, that defines a single protocol for connecting AI applications to external data sources, tools and workflows in place of a custom integration per pairing. Its official documentation likens it to a USB-C port for AI applications; the protocol distinguishes hosts, clients and servers communicating over JSON-RPC 2.0."
---

The Model Context Protocol (MCP) is an open standard for connecting AI applications to external systems — data sources such as local files and databases, tools such as search engines and calculators, and workflows such as specialized prompts. [[Organization/anthropic]] announced it on 25 November 2024, framing the problem as one of isolation: even sophisticated models are "trapped behind information silos and legacy systems", and every new data source "requires its own custom implementation, making truly connected systems difficult to scale" — the problem the Wikipedia account renders as the "N×M" data integration problem it says Anthropic described. MCP replaces those fragmented integrations with a single protocol, so that a developer implements MCP once in an agent and gains access to an entire ecosystem of integrations. The official documentation's analogy is a USB-C port for AI applications: just as USB-C provides a standardized way to connect electronic devices, MCP provides a standardized way to connect AI applications to external systems.

## Usage

### Architecture

The protocol distinguishes three roles. **Hosts** are the LLM applications — AI assistants, IDEs, workflow automation tools — that initiate connections; for each server it needs, a host creates a dedicated **client** that communicates with that server; **servers** are the services that expose capabilities. Host and clients typically run on the same machine while servers may be local or remote. Each client–server connection is a dedicated, stateful session beginning with initialization and capability negotiation, and messages use JSON-RPC 2.0. Transport is stdio for local processes and Streamable HTTP for networked communication; Server-Sent Events over HTTP was deprecated in the 2025-06-18 revision of the specification.

The specification groups capabilities by which side offers them. Servers may offer **Resources** (context and data for the user or the model), **Prompts** (templated messages and workflows for users), and **Tools** (functions for the model to execute). Clients may offer **Sampling** (server-initiated agentic behaviours and recursive LLM interactions), **Roots** (server-initiated inquiries into the URI or filesystem boundaries to operate in), and **Elicitation** (server-initiated requests for more information from users). Additional utilities cover configuration, progress tracking, cancellation, error reporting and logging.

In operation, a client asks its server for the list of tools and resources it provides; the server replies with a natural-language description of each capability and the expected call format; that information is given to the LLM, and when the model needs a tool the host instructs the relevant client to call it, injecting the returned result into the conversation.

The specification states that it takes some inspiration from the Language Server Protocol, which standardized how support for programming languages is added across a whole ecosystem of development tools — MCP standardizing, in the same way, how additional context and tools are integrated into the ecosystem of AI applications. Earlier stop-gap approaches, according to the Wikipedia account, solved similar problems but required vendor-specific connectors: [[Organization/openai]]'s 2023 function-calling API and the ChatGPT plug-in framework.

### Distribution and ecosystem

Anthropic's announcement shipped three components: the specification and SDKs, local MCP server support in the Claude Desktop apps, and an open-source repository of MCP servers, with pre-built servers for Google Drive, Slack, GitHub, Git, Postgres and Puppeteer. The protocol was released with SDKs in languages including Python, TypeScript, C# and Java, together with example server implementations. The `modelcontextprotocol/modelcontextprotocol` repository holds the specification, the protocol schema and the official documentation, is licensed under the MIT License, and defines the schema in TypeScript first while also publishing it as JSON Schema for wider compatibility; the documentation site is built using Mintlify.

The named early adopters in the announcement were Block and Apollo, alongside development tools companies Zed, Replit, Codeium and Sourcegraph. Dhanji R. Prasanna, Chief Technology Officer at Block, was quoted describing open technologies like MCP as "the bridges that connect AI to real-world applications". Later adoption reported on Wikipedia includes OpenAI officially adopting MCP in March 2025 after integrating it across its products including the ChatGPT desktop app, and adding MCP support to ChatGPT apps in September 2025; integration with Microsoft Semantic Kernel and Azure OpenAI; and deployment of MCP servers to Cloudflare. The official documentation lists Claude, ChatGPT, Visual Studio Code, [[SoftwareApplication/cursor]] and MCPJam among supporting clients. In [[DefinedTerm/ai-assisted-software-development]] specifically, IDEs, coding platforms such as Replit and code intelligence tools such as Sourcegraph adopted MCP to give AI coding assistants real-time access to project context.

Wikipedia records two governance and scale developments. In December 2025 Anthropic donated MCP to the [[Organization/agentic-ai-foundation]], a directed fund under the Linux Foundation co-founded by Anthropic, Block and OpenAI with support from other companies. In April 2026 that foundation held the MCP Dev Summit North America in New York City, drawing approximately 1,200 attendees; the same month Salesforce's Headless 360 platform began routing customer and agent interactions via MCP, and in late May Salesforce reported 4.5 million MCP calls processed since launch. MCP Apps, an official extension built on mcp-ui, standardizes delivery of interactive user interfaces such as dashboards, forms and data visualizations from servers to host applications, which the base specification — restricted to text and structured data — does not cover.

By November 2025 Anthropic's own characterisation was that the community had built thousands of MCP servers, that SDKs existed for all major programming languages, and that the industry had adopted MCP as the de-facto standard for connecting agents to tools and data.

### Security

The specification is explicit that MCP "enables powerful capabilities through arbitrary data access and code execution paths" and sets out four key principles for implementors: user consent and control, data privacy, tool safety, and LLM sampling controls. Under tool safety it states that tools represent arbitrary code execution and that "descriptions of tool behavior such as annotations should be considered untrusted, unless obtained from a trusted server". It also concedes that MCP itself cannot enforce these principles at the protocol level, and instead says implementors **SHOULD** build robust consent and authorization flows, document security implications, implement access controls and data protections, follow security best practices, and consider privacy implications in feature design.

Independent analysis followed quickly. Wikipedia records that in April 2025 security researchers released an analysis concluding there were multiple outstanding security issues with MCP, including prompt injection and poisoned tools allowing data exfiltration through other connected tools. Microsoft's own guidance frames the two named risks as [[DefinedTerm/indirect-prompt-injection]] and, as a subset of it, [[DefinedTerm/tool-poisoning]]. [[Report/model-context-protocol-security]], approved by the CoSAI Project Governing Board on 8 January 2026 and still marked "Status: Draft", organises nearly forty threats into twelve categories across three tiers, and argues MCP needs a different threat model from existing AI risk frameworks because those frameworks assume components behave predictably according to predefined logic, whereas MCP "places an LLM, an agent whose behavior is shaped by natural language input, at the center of security-critical decisions."

### Academic analysis

Two peer-directed surveys treat MCP as an object of study rather than a tool to adopt, and both come at it through security.

[[ScholarlyArticle/mcp-landscape-security-threats]] (October 2025) grounds its analysis in a four-phase server lifecycle it derives from the official documentation and from operational workflows — creation, deployment, operation and maintenance — and maps sixteen threat scenarios across four attacker types onto the *origins* of each risk rather than onto a single phase, on the reasoning that attacks such as tool poisoning and rug pulls "are introduced at the creation stage but triggered at operation". Its account of what distinguishes MCP from what came before is that MCP "incorporates access control, capability negotiation, and schema discovery as protocol primitives", unlike conventional function-calling mechanisms. Its structural diagnosis is that the ecosystem has no centralized security oversight, because servers are managed by independent developers with no central authority to audit baselines, and that MCP "currently lacks a standardized framework for authentication and authorization across clients and servers."

[[ScholarlyArticle/sok-security-and-safety-in-the-mcp-ecosystem]] (December 2025) argues something stronger about the protocol's shape: because MCP separates Resources (read-only context), Tools (external actions) and Prompts (reusable templates) across independent Hosts, Clients and Servers, "the traditional 'single safety perimeter' dissolves", so a failure in one primitive can escalate into a harmful action executed by another. It calls the resulting coupling of context and action a "semantic attack surface", and its central claim is that the security/safety distinction collapses under MCP — a hallucination about a tool's parameters can produce a breach, and an injected document can leave a state in which "the model honestly but mistakenly believes it is authorized to delete a database".

### Token cost at scale

A distinct, non-security problem emerges as the number of connected tools grows. Anthropic's engineering account in [[TechArticle/code-execution-with-mcp]] identifies two patterns that increase agent cost and latency: most clients load all tool definitions upfront into context, so an agent connected to thousands of tools processes hundreds of thousands of tokens before reading a request; and every intermediate tool result must pass through the model, so data flows through context repeatedly and may exceed the context window entirely. Its proposed answer, [[DefinedTerm/code-execution-with-mcp]], presents servers as code APIs the agent writes code against rather than as direct tool calls.

### What practitioners actually use it for

[[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] reports a narrower working scope than the specification implies: "MCP servers are primarily for plugging tools into your coding agent to extend its capabilities beyond file I/O and bash commands," because the spec's additional features — resources, prompts, and elicitations — "are generally not well-supported by MCP clients and coding agent harnesses." That gap between the specified primitives and the supported ones matters for the security analysis above, which reasons from all three primitives being in play.

That post also draws the prompt-injection consequence directly from where tool metadata lands: because a server's tool list, descriptions, and argument schemas are injected into the agent's system prompt, a server can shape the agent's behaviour through its descriptions alone — so its warning is never to connect to a server you do not trust. It adds a second exposure independent of injection: STDIO servers and others that run client-side through `npx` or `uvx` can execute code on the host.

On the token-cost problem, the same post supplies the practitioner's version of the finding above and one remedy the vendor accounts do not emphasise. Its advice is to turn off any server providing a large number of tools that is not actively in use, and — where an MCP server duplicates functionality already available as a CLI well-represented in training data, its examples being GitHub, Docker, and most databases — to prompt the agent to use the CLI instead, on the reasoning that the model already knows the tool and its output composes with `grep` and `jq`. Their own worked example replaced the Linear MCP server with a small CLI wrapping the Linear API, documented as six example invocations in their context file, which they report saved thousands of tokens of tool definitions plus more from verbose MCP responses.

## Related Terms

MCP is one of the configuration mechanisms catalogued for coding tools alongside [[DefinedTerm/context-files]], [[DefinedTerm/agent-skills]] and [[DefinedTerm/subagents]] — and Anthropic published Agent Skills as a companion open standard following the same approach. The tools that consume MCP servers are covered under [[DefinedTerm/coding-agent]], and the context-budget pressure MCP tool definitions create is one of the concerns of [[DefinedTerm/context-engineering]].
