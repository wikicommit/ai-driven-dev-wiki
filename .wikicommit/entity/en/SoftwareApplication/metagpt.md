---
title: "MetaGPT"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, agent-frameworks, open-source]
sources:
  - type: url
    url: 'https://github.com/geekan/MetaGPT'
    hash: sha256:19c986a40702497bbf0024ec704205be182610f7a73078ac208fc1428bd5527e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source multi-agent framework that assigns LLMs the roles of a software company — product manager, architect, project manager, engineer — and coordinates them through standard operating procedures, so that a one-line requirement comes out as user stories, requirements, designs, documents and code."
  applicationCategory: "Multi-agent framework"
---

MetaGPT is an open-source, MIT-licensed multi-agent framework built on the idea of giving different
LLMs different roles and having them work together "as a collaborative entity for complex tasks". Its
README models that entity on a software company: MetaGPT takes a one-line requirement as input and
produces user stories, competitive analysis, requirements, data structures, APIs and documents, with
product managers, architects, project managers and engineers as the roles inside it. The project sums
up its philosophy as `Code = SOP(Team)` — standard operating procedures, made concrete and applied to
teams composed of LLMs — and describes the software-company schematic as being implemented gradually.
It is an instance of an [[DefinedTerm/llm-based-multi-agent-system]], and its repository is now
published under the `FoundationAgents` organization on GitHub.

## Capabilities

MetaGPT is a Python package, installed with `pip install metagpt`, that also needs Node.js and pnpm at
run time. Model access is configured in a YAML file under `~/.metagpt/`, which names the API type
(OpenAI, Azure, Ollama, Groq and others), the model, the endpoint and the key. It can be driven from
the command line — `metagpt "Create a 2048 game"` generates a repository in a local workspace — or
used as a library that returns the generated project repository. Alongside the software-company
pipeline the project ships a **Data Interpreter** agent that writes and runs code for tasks such as
data analysis, and its documentation walks through building single agents and multi-agent systems,
with use cases including a debate between agents, a researcher and a receipt assistant.

## Adoption & Ecosystem

The same team runs a hosted natural-language programming product, MGX (MetaGPT X), which the README
announces as launched on 19 February 2025 and describes as "the world's first AI agent development
team". The README also points to further research papers from the team, and asks those who use MetaGPT
in publications to cite the team's paper describing it.
