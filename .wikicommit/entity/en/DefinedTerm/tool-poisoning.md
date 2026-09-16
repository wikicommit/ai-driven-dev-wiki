---
title: "Tool Poisoning"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, security, agents]
sources:
  - type: url
    url: https://arxiv.org/pdf/2603.21642
    hash: sha256:fd0ab75587fb77f1a54e766576e9fc710b36a78afe06ff29d7801b5a329367eb
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A prompt-injection attack against agentic AI systems in which an attacker embeds malicious instructions in a tool's description, metadata, or configuration exposed through the Model Context Protocol, causing the agent to misuse the tool for data exfiltration, unauthorized command execution, or behavior hijacking."
---

Tool poisoning is a prompt-injection attack in which an attacker hides malicious instructions
inside the metadata of a tool exposed to an AI agent — its description, parameter schema, or
configuration — rather than in the code the tool executes. Because agents read tool descriptions to
decide how to use them, a model can be tricked into executing an unintended sub-task, such as
reading and exfiltrating a sensitive file, before anyone realizes a tool has been misused. The
attack is a structural risk of [[DefinedTerm/model-context-protocol]] specifically, since MCP
clients connect models to tools capable of file access, command execution, and API calls, and the
protocol does not by itself constrain how much of that tool metadata is trusted. A related pattern
is the "rug pull," where a tool that behaved benignly when first approved later activates hidden
malicious instructions once it has been used a certain number of times or otherwise gained trust.

## Usage
[[ScholarlyArticle/are-ai-assisted-development-tools-immune-to-prompt-injection]] empirically tested
seven MCP clients against four tool-poisoning attack patterns: instructing an agent to read
sensitive local files (such as MCP client configuration containing credentials and a local SSH
credentials file) and pass their contents as a hidden tool parameter; claiming false execution
priority to make a tool log all subsequent tool usage for silent surveillance; embedding a hidden
instruction that causes a tool to generate a phishing link with a benign-looking display text; and
instructing a tool to download and execute a remote script under the guise of routine maintenance.
No client blocked all four attacks: even the best-performing clients had at least one non-safe
result, and one client failed all four.

## When It Applies
The same study traced most of the tool-poisoning vulnerabilities it found to a small set of
structural gaps: the absence of static validation of tool descriptions before registration,
incomplete visibility of tool parameters to the end user before execution, missing execution
sandboxing, and an implicit trust in server-provided tool metadata with no reputation system for
MCP servers. The risk is highest when an agent has broad authority to act autonomously, tool calls
are not gated behind human approval, and the system does not separate the model's own instructions
from retrieved tool metadata and tool output into distinct trust contexts.

## Related Terms
- [[DefinedTerm/model-context-protocol]] — the protocol whose tool-exposure model tool poisoning
  exploits
- [[ScholarlyArticle/are-ai-assisted-development-tools-immune-to-prompt-injection]] — an empirical
  evaluation of tool-poisoning resistance across seven MCP clients
