---
title: "Implicit Tool Poisoning"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, security, agents, prompt-injection]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.07395'
    hash: sha256:02a5d5f74b794c1e19fa444390d6ae855747ee58de6120b249b03b5680f40bfc
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A variant of tool poisoning in which the poisoned tool is never invoked; instead, instructions in its metadata induce an agent to call a different, legitimate but high-privilege tool to carry out a malicious operation."
---

Implicit tool poisoning (ITP) is a variant of [[DefinedTerm/tool-poisoning]] in which the poisoned tool itself is never executed. As described in [[ScholarlyArticle/mcp-itp]], an adversary publishes a tool whose description is crafted to exploit weaknesses in an LLM agent's contextual reasoning; once the tool's metadata is loaded into the agent's context during [[DefinedTerm/model-context-protocol]] registration, it misleads the agent into invoking an existing, legitimate but high-privilege target tool to perform the malicious operation. The paper's illustration is a user asking the agent to read a file, and the agent ignoring the request and instead calling a file-writing tool to modify sensitive assets such as an SSH private key. What distinguishes it from explicit tool poisoning — where the agent is induced to call the poisoned tool directly — is that the attack trigger is decoupled from the tool that is eventually invoked, which the paper argues keeps the attack stealthy and difficult to detect through mechanisms that monitor tool execution.

## Usage

The term is used in LLM-agent security research on the MCP ecosystem. [[ScholarlyArticle/mcp-itp]] names it as a particularly stealthy threat variant and contrasts it with prior tool-poisoning work, which it describes as concentrating on explicit poisoning or on manually crafted poisoned tools. The same paper's threat model places the attacker in a black-box position: able to inspect the tools a benign MCP server exposes, choose an original tool and a high-privilege target tool from among them, and publish a poisoned tool through an attacker-controlled server, but without access to users' queries or the agent's internal parameters.

That paper's MCP-ITP framework generates such poisoned tools automatically. Its tool descriptions pair a camouflage passage, which presents the poisoned tool as functionally equivalent to the original tool, with a passage phrased in the tone of a compliance policy — for example, stating that before the original tool can perform its core function the target tool must first be called for compliance reasons. Its case studies distinguish three outcomes: the agent is manipulated into calling the target tool (success), the agent calls the original tool as the user intended (ignored), or the agent calls the poisoned tool itself (direct).

## Related Terms

- [[DefinedTerm/tool-poisoning]] — the broader attack class of which this is a variant
- [[DefinedTerm/indirect-prompt-injection]] — the attack family [[ScholarlyArticle/mcp-itp]] places tool poisoning within
- [[DefinedTerm/model-context-protocol]] — the protocol whose tool-registration phase the attack exploits
