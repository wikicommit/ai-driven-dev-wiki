---
title: "Tool creation"
type: "schema:DefinedTerm"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://aclanthology.org/2025.acl-long.1266.pdf'
    hash: sha256:e540f7778ba7b71c57f3614b2a333278db9a340b0b059328649725e9e89f3eab
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The problem of enabling LLMs to create their own tools so that they can dynamically expand their capabilities at runtime, as opposed to tool learning, which teaches LLMs to use human-crafted tools more effectively."
---

Tool creation is the problem of enabling large language models to create their own tools — external pieces of software they can then execute — so that an agent's capabilities can be dynamically expanded at runtime rather than being fixed by whatever tools human developers implemented in advance. As framed in [[ScholarlyArticle/llm-agents-making-agent-tools]], it is not to be confused with tool learning: teaching LLMs to make more effective use of appropriate, human-crafted tools, which that paper describes as having been studied extensively.

## Usage

The term is used for work in which the model, not a developer, produces the tool. That paper characterises earlier tool-creation methods — it names CRAFT, CREATOR and LATM — as limited to very simple, narrowly scoped tools, for two reasons: each tool is crafted from scratch, and the systems cannot interact with the operating system by running bash commands or reading and writing files. It likewise describes tool-creation benchmarks as extending code-generation benchmarks by letting the LLM choose the Python function's signature as well as its implementation, while remaining limited to simple functions that cannot install dependencies.

The same paper pushes the term toward creating tools from existing code. Its [[SoftwareApplication/toolmaker]] framework wraps the public repository behind a scientific paper as a tool, which means setting up the environment the function runs in — installing dependencies, downloading models, configuring for the system and hardware — as well as implementing the function itself. Its benchmark, [[Dataset/tm-bench]], asks for a reusable tool that can be applied to different inputs, rather than a solution to one task instance.

## Related Terms

- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/tool-use-design-pattern]]
