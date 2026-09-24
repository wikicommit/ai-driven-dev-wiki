---
title: "Tool Poisoning"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, security, agents]
sources:
  - type: url
    url: https://arxiv.org/pdf/2603.21642
    hash: sha256:fd0ab75587fb77f1a54e766576e9fc710b36a78afe06ff29d7801b5a329367eb
  - type: url
    url: 'https://arxiv.org/pdf/2601.07395'
    hash: sha256:02a5d5f74b794c1e19fa444390d6ae855747ee58de6120b249b03b5680f40bfc
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A prompt-injection attack against agentic AI systems in which an attacker embeds malicious instructions in a tool's description, metadata, or configuration exposed through the Model Context Protocol, causing the agent to misuse the tool for data exfiltration, unauthorized command execution, or behavior hijacking."
---

Tool poisoning is a prompt-injection attack in which an attacker hides malicious instructions
inside the metadata of a tool exposed to an AI agent — its description, parameter schema, or
configuration — rather than in the code the tool executes. Because agents read tool descriptions to
decide how to use them, a model can be tricked into executing an unintended sub-task, such as
reading and exfiltrating a sensitive file, before anyone realizes a tool has been called. The
risk is especially relevant to systems built on [[DefinedTerm/model-context-protocol]], in which MCP
clients connect models to tools capable of executing actions such as file access, command execution,
and API calls. A related pattern
is the "rug pull," where a tool that behaved benignly when first approved later activates hidden
malicious instructions once it has been approved and used a certain number of times.

[[ScholarlyArticle/mcp-itp]] classifies tool poisoning as a specialized form of
[[DefinedTerm/indirect-prompt-injection]]: where traditional indirect prompt injection plants
instructions in external data, tool poisoning in MCP embeds them directly in a tool's description
and injects them into the model's context during the MCP registration phase, so that they
influence the agent's decisions while it reasons. The same paper distinguishes two forms. In
explicit tool poisoning, the agent is induced to call the poisoned tool itself, which the paper
argues leaves the attack exposed to monitoring of tool execution. In
[[DefinedTerm/implicit-tool-poisoning]], the poisoned tool is never called; its description instead
steers the agent into invoking a different, legitimate but high-privilege tool.

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

[[ScholarlyArticle/mcp-itp]] takes the attacker's side and automates the construction of implicitly
poisoned tools, iteratively refining tool descriptions with feedback from an LLM that tests their
effect on an agent and an LLM that simulates malicious-tool detection. Evaluated on the MCPTox
dataset across 12 LLM agent settings, its generated tools achieved up to 84.2% attack success while
reducing the rate at which they were flagged as malicious to as low as 0.3%, outperforming the
manually crafted poisoned tools that dataset provides.

## When It Applies
[[ScholarlyArticle/are-ai-assisted-development-tools-immune-to-prompt-injection]] traced most of the tool-poisoning vulnerabilities it found to a small set of
structural gaps: the absence of static validation of tool descriptions before registration,
incomplete visibility of tool parameters to the end user before execution, missing execution
sandboxing, and an implicit trust in server-provided tool metadata with no reputation system for
MCP servers. In the qualitative risk scale that study used to compare clients, the risk of
prompt-injection-driven poisoning depends on the presence of untrusted inputs, the degree of
authority granted to the model, whether tool calls are gated, sandboxed or require user approval,
and whether the system keeps separate contexts or collapses them into a single one.

## Related Terms
- [[DefinedTerm/model-context-protocol]] — the protocol whose tool-exposure model tool poisoning
  exploits
- [[ScholarlyArticle/are-ai-assisted-development-tools-immune-to-prompt-injection]] — an empirical
  evaluation of tool-poisoning resistance across seven MCP clients
- [[DefinedTerm/implicit-tool-poisoning]] — the variant in which the poisoned tool is never invoked
- [[DefinedTerm/indirect-prompt-injection]] — the attack family tool poisoning is classified under
  in [[ScholarlyArticle/mcp-itp]]
- [[ScholarlyArticle/mcp-itp]] — an automated framework for generating implicitly poisoned MCP tools
