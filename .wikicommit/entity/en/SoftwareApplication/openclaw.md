---
title: "OpenClaw"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture, governance, agent-safety, vibe-coding]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05786'
    hash: sha256:88932db1701d24427b3c99749daed01d7948095ccb89ce4e1db8c125b09b160f
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
  - type: url
    url: 'https://simonwillison.net/2026/Sep/27/2026-in-llms-so-far/'
    hash: sha256:385452beca91e7fc01c6dedad958d7ec1fa6f8605175db68befe2a8961aec188
  - type: url
    url: 'https://www.infoq.cn/article/D8E3q93kBviq8Z8mu0Ao'
    hash: sha256:a19a7c7520ea6086e1939c2775ea090be3cbbe7f9aaa86c470b64ba576357da7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An open-source, local-first AI assistant gateway that connects messaging surfaces to an embedded agent runtime, executing tools and communicating on behalf of the developer, with a manifest-first plugin system and a structured long-term memory subsystem."
  applicationCategory: "AI agent"
  featureList: "Tool execution; messaging across WhatsApp, Telegram, Slack, Discord and Signal; manifest-first plugin system with a central registry; separate skills layer with a public registry; built-in MCP server and outbound client; structured long-term memory with optional hybrid retrieval"
  author: "Peter Steinberger and OpenClaw Contributors"
---

OpenClaw is an open-source AI agent that can execute a variety of tools and communicate openly on behalf of the developer on online platforms, with human users or with other AI agents. Its capabilities can be extended by registering a named skill, which the agent may then invoke as a tool call.

[[ScholarlyArticle/dive-into-claude-code]] describes it more specifically as a local-first WebSocket gateway that connects messaging surfaces — WhatsApp, Telegram, Slack, Discord, Signal and others — to an embedded agent runtime, with companion apps on macOS, iOS and Android, and characterizes it as a persistent control plane for multi-channel personal assistance rather than a repository-bound coding tool. It runs as a persistent daemon owning all messaging surface connections and coordinating clients, tools and device nodes over a typed WebSocket protocol.

The agent is also used as the implementation target in [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]], which deploys it inside a [[DefinedTerm/trusted-execution-environment]] so that users can verify which guardrail was applied to its responses. In that reported deployment its model calls were served by external LLM APIs with GPT-5.1 as the backend model, and it was packaged for an enclave alongside a minimal Linux kernel and Node.js and Python dependencies.

## Capabilities

OpenClaw plans, invokes tools, and responds to new messages on online communication platforms. Its model access is configurable enough that it can be pointed at a single local endpoint: the [[DefinedTerm/proof-of-guardrail]] implementation launches a local proxy LLM server inside the enclave and configures it as the only available LLM option for OpenClaw, so that every input, tool call and output passes through that proxy. The same work notes that response streaming was disabled in its setup for ease of guardrail execution.

Capabilities can be registered as named skills, which the agent can then decide to invoke. Registering the enclave's attestation service as an "attestation skill" let the agent proactively offer an attestation when it received a high-stakes question, rather than only on explicit request. The paper's example conversation is a different case: a user asks whether to put their savings into a newly launched token, explicitly asks the bot to attest its answer, and receives both a cautionary answer and an attestation of it.

The architectural study describes the runtime as an embedded agent core sitting inside a larger gateway dispatch layer: the gateway's agent RPC validates parameters, resolves sessions and returns immediately, while the embedded runner executes the agentic loop and emits lifecycle and stream events back through the gateway protocol. Runs are serialized through per-session queues and an optional global lane, which prevents tool and session races across the multi-channel surface.

Extension is manifest-first. Plugins register capabilities into a central registry across twelve capability types — including text inference, speech, media understanding, image, music and video generation, web search and messaging channels — and the gateway reads that registry to expose tools, channels, provider setup, hooks, HTTP routes, CLI commands and services. A separate skills layer draws from workspace, project, personal, managed, bundled and extra directories, with workspace skills taking highest precedence, alongside a public registry; MCP is supported through built-in server and outbound-client commands.

Memory is handled as its own subsystem rather than as a by-product of context management. Workspace bootstrap files are injected into the system prompt at session start, and the memory system manages long-term durable facts, date-stamped daily notes, and an optional file for background consolidation summaries. Where an embedding provider is configured, memory search combines vector similarity with keyword matching, and an experimental background process scores candidates and promotes only qualified items from short-term recall into long-term memory. Before compaction the agent is automatically reminded to save important notes to memory files.

## Safety posture

The architectural study contrasts OpenClaw's security model with per-action approval systems: it assumes a single trusted operator per gateway instance, and begins with identity and access control — direct-message pairing codes, sender allowlists and gateway authentication — rather than per-action safety classification. Tool policy uses configurable allow and deny lists per agent rather than a centralized classifier. Sandboxing is available as an opt-in feature with multiple backends and configurable scope, but is not active by default, and the project's security documentation explicitly states that hostile multi-tenant isolation on a shared gateway is not a supported security boundary.

Multi-agent behaviour is split into two separate concerns. A single gateway can host multiple fully isolated agents, each with its own workspace, authentication profiles, session store and model configuration, routed to channels or senders by deterministic binding rules. Separately, within a single agent, background runs can be spawned with configurable nesting depth and thread-bound sessions. The study notes that the project's own vision explicitly rejects agent-hierarchy frameworks as a default architecture.

[[TechArticle/model-ai-governance-framework-for-agentic-ai]] describes it more briefly, as an
open-source AI agent platform that acts as an autonomous personal assistant through common chat
interfaces such as Telegram and Slack, automating everyday tasks such as compiling research,
handling customer enquiries or debugging code. That framework's own application of its four
dimensions to OpenClaw deployments states that the platform was launched with limited security
controls and that deploying it safely is non-trivial, listing as concerns its lack of maturity and
hardening, access control and authentication gaps, exposure of sensitive data, supply chain risks
from third-party skills, and memory poisoning risks. IMDA reports drawing on the practical
experience of GovTech, CSA, Grab and Microsoft in reaching that assessment.

Its recommendations for deploying OpenClaw and similar agents responsibly are stated as avoidances
and enforcement points rather than as configuration values. Under bounding risk upfront: do not
deploy it as-is in mission-critical environments, including systems handling sensitive data or
financial transactions; do not create a single all-powerful agent with unrestricted access, using
instead multiple agents with narrow, clearly defined rules; and do not install it on primary work
or personal devices containing sensitive data with unrestricted access to files and applications.
Under human accountability: set the level of agent autonomy by a risk-based assessment of data
sensitivity and task criticality, and enforce human approval through system-level controls where
possible rather than prompt-layer guardrails, which the framework says may be bypassed or
"forgotten". Under technical controls: review and tighten OpenClaw configurations, which it
characterises as permissive by default — restricting messaging channel access and using dedicated
identities and credentials for the agent — verify before deployment that safety controls and
[[DefinedTerm/human-in-the-loop]] work as intended by attempting disallowed actions, and after
deployment ensure all agent actions are logged and attributable and avoid leaving the agent
unsupervised for extended periods. Under end-user responsibility: provide personnel training on
autonomous agent risks and on the user's own responsibility to prevent careless misuse.

## Adoption & Ecosystem

In the authors' demonstration, OpenClaw ran as an AI bot on Telegram, responding automatically to user messages, with other users in the chat able to request an attestation document at any time through a chat command. The authors characterize the agent as powerful and open-source, and exemplify their implementation with it.

The architectural study reports that OpenClaw can host [[SoftwareApplication/claude-code]], OpenAI Codex and Gemini CLI as external coding harnesses through its Agent Client Protocol integration, which it offers as evidence that gateway-level systems and task-level harnesses compose rather than compete. It is used in that paper, alongside [[SoftwareApplication/hermes-agent]], as an independent point of comparison for Claude Code's design choices.

[[BlogPosting/2026-in-llms-so-far]] traces the project's history and the category it started.
According to Simon Willison, it began as an obscure GitHub repository called Warelay whose first
commit, on 24 November 2025, added an MIT license file; by the end of January 2026 it had renamed
itself in turn to CLAWDIS, CLAWDBOT, Moltbot and finally OpenClaw. He reports that it had about 8,300
commits less than two months after it started and over 100,000 by September 2026, and calls it "the
most vibe-coded piece of software in existence" (see [[DefinedTerm/vibe-coding]]). On his account it
effectively defined a new category of software, for which he uses the generic name
[[DefinedTerm/claw]]. Apple stores in the Bay Area sold out of Mac minis because so many people
bought them to run OpenClaw, and in March 2026, which he calls peak OpenClaw, companies in China hosted
install parties at which people who were not technical queued for help installing Claws on their own
devices. He reads
that demand as proof that ordinary people want a personal AI agent that can do useful things on their
behalf.

## Practitioner reports

Practitioners in China describe OpenClaw from hands-on use in [[NewsArticle/behind-openclaws-rise-agents-ai-coding-and-team-collaboration]], an InfoQ China roundtable published in March 2026. One participant, from NetEase CodeWave, describes its architecture as a single lightweight core agent called Pi, which keeps only capabilities such as memory retrieval and tool calling, behind a gateway that receives requests from different channels and forwards them to it, with concrete capabilities living in skills. He locates its innovation in connecting a desktop agent to chat tools through that channel gateway, and attributes its core idea to [[DefinedTerm/programmatic-tool-calling]]: when it meets a problem it cannot solve it writes a Python script and runs it in a sandbox. His team registers Claude Code as a skill on Pi for plugin development, and falls back to a stronger planning model when the main model's planning is weak.

The participants dispute that it is a low-barrier tool. The same speaker says that using it well requires familiarity with JSON configuration, troubleshooting skills and continual tuning of skills; that its configuration file is unstable and can be rewritten or corrupted on restart, so he runs a separate agent to probe it and back the file up; and that browser access is not yet stable. Speakers report heavy token consumption, which he addressed by moving to a file-based memory system modelled on ByteDance's OpenViking, and a Ping An Technology participant recounts an unclear instruction leading the agent to call a delete endpoint and erase all his comments on a review platform — one reason, he says, many people run such agents on an old computer or a dedicated Mac mini.

On a reported exposure of OpenClaw instances, the NetEase speaker says the gateway's console listens on port 18789, that some users exposed it to the public internet or bound it to the LAN, and that the console can be restricted to local access in its configuration file. The Ping An participant argues the risk remains because the agent acts with the user's permissions and its behaviour may not match the user's intent, and suggests a control layer on intent beyond conventional RBAC; the NetEase team gives each agent a tool profile with limited permissions, such as message-only or read-only with no delete rights.
