---
title: "Agent interoperability protocols compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/model-context-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent2agent-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-communication-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-network-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-client-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/universal-commerce-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-payments-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-to-user-interface-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/agent-user-interaction-protocol.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/ScholarlyArticle/a-survey-of-agent-interoperability-protocols.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/BlogPosting/developers-guide-to-ai-agent-protocols.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/BlogPosting/acp-protocol-and-multiple-ai-coding-agents.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/BlogPosting/build-better-ai-agents-agent-bake-off.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/BlogPosting/new-sdlc-vibe-coding.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/DefinedTerm/spec-driven-development.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/BlogPosting/agentic-engineering-swarms-of-ai-agents.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/SoftwareApplication/agent-development-kit.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
  - path: .wikicommit/entity/en/ScholarlyArticle/agentic-ai-security-threats-defenses-evaluation-and-open-challenges.md
    source_commit: 384b025f323e723811baff968a7457634ec774f0
---

The wiki holds pages on nine protocols that standardize some part of what an AI agent connects to: [[DefinedTerm/model-context-protocol]] (MCP), [[DefinedTerm/agent2agent-protocol]] (A2A), [[DefinedTerm/agent-communication-protocol]] (ACP), [[DefinedTerm/agent-network-protocol]] (ANP), [[DefinedTerm/agent-client-protocol]] (also abbreviated ACP), [[DefinedTerm/universal-commerce-protocol]] (UCP), [[DefinedTerm/agent-payments-protocol]] (AP2), [[DefinedTerm/agent-to-user-interface-protocol]] (A2UI) and [[DefinedTerm/agent-user-interaction-protocol]] (AG-UI). This page sets them side by side by what each connects, how each is described as carrying messages, and how discovery and authorization work. It also covers how different sources group them, what the sources report about their adoption, and where they are described as working together. The comparison uses only what the wiki's pages record. Most of the newer protocols are each described by a single source, so what is said about them here is that source's account.

## What each one connects

| Protocol | Connects | Transport and format, as described | Discovery, as described |
| --- | --- | --- | --- |
| MCP | An agent to external tools and data | A JSON-RPC client-server interface; servers expose tool names, input schemas and descriptions | The agent queries tool metadata across connected servers; in VS Code a server is registered in `.vscode/mcp.json` |
| A2A | An agent to other agents | Tasks, Messages, Artifacts and Parts exchanged between an A2A client and server, synchronously or by streaming | An Agent Card at `/.well-known/agent-card.json`, or by direct configuration, a fixed URI or a registry |
| ACP (Agent Communication Protocol) | Agents to one another, for general-purpose messaging | RESTful HTTP with MIME-typed multipart messages, synchronous and asynchronous | Online and offline discovery, as the survey associates with its roadmap stage |
| ANP | Agents on an open network | W3C decentralized identifiers (DIDs) and JSON-LD graphs | Open-network agent discovery |
| ACP (Agent Client Protocol) | An IDE or editor to a coding agent | JSON-RPC 2.0 over standard input and output, with the agent running as a subprocess of the IDE | Capability negotiation at session start, similar to LSP's initialization handshake |
| UCP | An agent to merchants' checkout flows | Strongly typed request and response schemas kept the same over REST, MCP, A2A or Embedded Protocols | A merchant profile at `/.well-known/ucp` |
| AP2 | A purchase to the person who authorized it | Typed mandates (`IntentMandate`, `PaymentMandate`) and a `PaymentReceipt` | Not described |
| A2UI | An agent's output to a rendered interface | Declarative JSON drawn from a fixed catalog of 18 component primitives, with structure and data sent separately | Not described |
| AG-UI | An agent framework's events to a frontend | A server-sent events stream of typed events such as `TEXT_MESSAGE_CONTENT` and `TOOL_CALL_START` | Not described |

## Two protocols called ACP

Two different protocols in the wiki share the acronym ACP, and they connect different parties.

- The **Agent Communication Protocol** is one of the four protocols in [[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]]. It is a protocol for agents to message each other over HTTP.
- The **Agent Client Protocol** comes from [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]]. It sits between an IDE and a coding agent, and that post compares it to the Language Server Protocol, calling it "LSP for AI agents".

When "ACP" appears in a source, the parties it connects show which of the two is meant.

## How the sources arrange them

Several sources group some of these protocols, and they use different schemes.

- **A four-stage adoption roadmap.** The survey compares MCP, ACP (Agent Communication Protocol), A2A and ANP by interaction mode, discovery mechanism, communication pattern and security model. It orders them as adoption phases:
  1. MCP, for tool access
  2. ACP, for structured, session-aware messaging
  3. A2A, for collaborative task execution
  4. ANP, for decentralized agent marketplaces
- **Six layers in one agent.** Google's [[BlogPosting/developers-guide-to-ai-agent-protocols]] treats MCP, A2A, UCP, AP2, A2UI and AG-UI as layers rather than competitors. Its example is an [[SoftwareApplication/agent-development-kit]] agent in which a single request uses all six:
  - MCP and A2A gather information.
  - UCP and AP2 complete the transaction.
  - A2UI and AG-UI present the result.

  The guide is a tutorial for Google's own framework, and every code sample in it uses ADK. A second post by Google staff, [[BlogPosting/build-better-ai-agents-agent-bake-off]], names the same six protocols as the current landscape. It advises adopting open agent protocols rather than writing custom API wrappers per tool, and argues that mastering this landscape is what separates prototypes from production systems.
- **A two-protocol stack.** A handbook chapter cited on the A2A page says the industry is settling into "MCP connects tools, A2A connects agents". Together, the chapter says, the two form the protocol base of a multi-agent system. [[BlogPosting/new-sdlc-vibe-coding]] describes the same division in an example: Google's Agents CLI coordinates with other agents over MCP for tools and over A2A for handing off work.
- **Three layers for platform governance.** The Agent Client Protocol post proposes a three-layer model for governing enterprise AI platforms. MCP and Skills carry reusable enterprise capabilities, ACP is the interaction layer between developers and assistants, and A2A is the collaboration network among agents.
- **Three layers that make AI a member of the system.** A handbook chapter on spec-driven development, recorded on [[DefinedTerm/spec-driven-development]], describes a three-layer protocol stack: MCP defines how the AI interacts with tools, A2A lets agents collaborate, and AG-UI establishes real-time visible interaction between user and agent.

MCP and A2A appear in every one of these groupings. The survey's roadmap has no layer for commerce, payments or user interfaces. Google's two posts do not include ANP or either ACP.

## Where they differ

### Who talks to whom

MCP links an agent to tools. A2A, the Agent Communication Protocol and ANP link agents to other agents. They differ in how they are described:

| Protocol | Described as |
| --- | --- |
| A2A | Peer-to-peer task delegation through capability-based Agent Cards |
| Agent Communication Protocol | Lightweight, runtime-independent HTTP messaging |
| ANP | Discovery on an open network through decentralized identifiers |

The remaining five protocols each face one specific counterpart:

| Protocol | Counterpart |
| --- | --- |
| Agent Client Protocol | The developer's editor |
| UCP | A merchant |
| AP2 | The person who authorizes a purchase |
| A2UI | A rendering client |
| AG-UI | A frontend listening to a stream |

### Discovery

The sources describe discovery in different forms:

- **A2A** publishes Agent Cards at a well-known URL. A whitepaper chapter cited on the A2A page also describes Nacos acting as an A2A registry.
- **UCP** publishes a profile at `/.well-known/ucp`, which Google's guide calls the same discovery pattern A2A uses.
- **ANP** relies on decentralized identifiers on an open network.
- **MCP** discovery works through tool metadata on the servers an agent is connected to.
- **The Agent Client Protocol** starts a session with capability negotiation between the IDE and the agent. JetBrains also offers an ACP Agent Registry for installing agents from inside the IDE.
- **AP2, A2UI and AG-UI** have no discovery step in the pages that describe them.

The guide lists discovery through well-known URLs, typed schemas and standard event streams as patterns the protocols it covers share.

### Control and authorization

The protocols put the check on an agent's actions in different places:

- **MCP:** one account names an MCP Host that manages consent and policy. The same account says Tools are gated by human approval.
- **Agent Client Protocol:** every file read, edit or command goes through a tool call the IDE can see and audit. Sensitive operations need the IDE's permission, which it may grant automatically under a user-configured policy, ask the user about, or present as a diff.
- **AP2:** an order over the owner's configured limit leaves its `PaymentMandate` unsigned until a manager approves it. Intent, authorization and payment are recorded as a chain.

### Security as a subject of study

The sources also treat the protocols as a source of risk:

- The framework cited on the A2A page gives the example of an untrusted MCP server that exfiltrates a user's data.
- The MCP page records GitHub's advice to vet third-party servers as supply-chain dependencies.
- [[ScholarlyArticle/agentic-ai-security-threats-defenses-evaluation-and-open-challenges]] makes "multi-agent and protocol-level threats" one of its five threat categories. It restricts its protocol-level discussion to MCP and A2A. It names ANP and the Agent Communication Protocol but does not cover them.

### Stated maturity and adoption

Some pages record where a protocol stood when their sources were written:

- AP2 was at v0.1 in Google's guide.
- A handbook chapter reports that a 2026 update to A2A added an agent directory, and lists MCP as having become the de facto standard.
- The survey calls all four of its protocols emerging.

One source counts adoption directly. [[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]] reads the source code of eleven coding-agent systems pinned to July 2026 releases. It reports:

- MCP in eight of the eleven systems. Skills in the SKILL.md format appear in nine, so the paper concludes that skills now lead MCP in adoption.
- The Agent Client Protocol in six systems.
- A2A as a capability of Gemini CLI alone within that corpus.

These counts cover only coding-agent harnesses, not the other settings the protocols are described in.

## Where they overlap

The protocols are described as running over or alongside one another:

- UCP can use MCP or A2A as its transport.
- AP2 is an extension of UCP.
- The Agent Client Protocol post says ACP handles interaction between agent and IDE while MCP extends the agent's reach to external systems. It lists native support for MCP servers among ACP's features, and says JetBrains provides MCP integration for agents running under ACP.
- A deployment described in [[BlogPosting/agentic-engineering-swarms-of-ai-agents]] has its worker agents communicate over A2A. It reaches agents without A2A support through an MCP wrapper, and connected a coding agent with no native A2A support through an MCP adapter. The authors say this makes the system IDE-agnostic, and they list interoperability across agentic communication protocols among their criteria for choosing a framework.

### Roles beyond the original one

The Agent Client Protocol is reported doing more than connecting an editor to an agent:

- The harness-engineering paper says it has acquired a third role, hosting whole harnesses. Its example is OpenHands running Claude Code, Codex or Gemini CLI as interchangeable backends.
- The Agent Client Protocol post describes AutoDev's integration as bidirectional: AutoDev can act as both an ACP server and an ACP client. Agents that do not speak ACP, such as Claude Code, are adapted by parsing their own streaming output.

### Support in one framework

The [[SoftwareApplication/agent-development-kit]] page records how one framework handles several of these protocols, as shown in Google's guide:

| Protocol | ADK support, as described |
| --- | --- |
| MCP | `McpToolset` for MCP servers; the MCP Toolbox for Databases |
| A2A | A utility turns an ADK agent into an A2A service; `RemoteA2aAgent` routes to one remote agent per turn, and the guide uses the `a2a-sdk` directly for queries that span several |
| A2UI | The `adk web` interface renders A2UI components natively |
| AG-UI | The agent is wrapped with the `ag_ui_adk` package and mounted on a FastAPI app |
| AP2 | Its types ship as a separate package rather than in ADK core |

The ADK page does not describe how the framework supports UCP.
