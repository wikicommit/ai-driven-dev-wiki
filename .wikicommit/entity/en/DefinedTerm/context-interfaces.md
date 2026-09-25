---
title: "Context interfaces"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, context-window]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html'
    hash: sha256:5d6208219888475f13564a3c1495a0291ee1a06c40a75c10315de16798f766b5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A term proposed by Birgitta Böckeler for the descriptions given to a coding agent's LLM of how it can obtain more context should it decide to, such as built-in tools, MCP servers and skills."
---

Context interfaces are, in the words of the memo that introduced the term, descriptions for the LLM
of how it can get even more context, should it decide to. Birgitta Böckeler proposed the name in
[[BlogPosting/context-engineering-for-coding-agents]], saying she could not find an established term
for the category, and used it to distinguish this kind of context configuration in coding agents
from reusable prompts — instructions and guidance — that are placed in the context directly.

## Usage

The memo lists three kinds of context interface: **tools**, the built-in capabilities of a coding
agent such as running bash commands or searching files; **MCP servers**
([[DefinedTerm/model-context-protocol]]), custom programs or scripts running locally or on a server
that give the agent access to data sources and other actions; and **skills**
([[DefinedTerm/agent-skills]]), descriptions of additional resources, instructions, documentation or
scripts that the LLM can load on demand when it judges them relevant. It singles out file reading
and searching in the workspace as the most basic and powerful context interfaces, since they are how
the agent understands the current codebase.

Because each configured interface's description takes up space in the context, the memo advises
thinking strategically about which context interfaces a particular task actually needs. The memo
notes that letting the LLM decide when to load context — its example is skills — is what allows
agents to run unsupervised, but leaves some uncertainty about whether the context will actually be
loaded when expected.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-skills]]
