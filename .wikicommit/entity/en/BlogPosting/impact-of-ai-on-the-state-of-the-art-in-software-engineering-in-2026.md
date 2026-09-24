---
title: "Impact de l'IA sur l'état de l'art de l'ingénierie logicielle en 2026"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, context-engineering, spec-driven, agent-skills]
sources:
  - type: url
    url: 'https://eventuallycoding.com/2026/02/context-driven-engineering/'
    hash: sha256:2af38c61949d6c58913e8b63fdf818bcf71314f01f14f330e3346f3ee531f9ff
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A French-language survey of how development teams industrialised AI coding assistants in 2025, built on testimony from engineers at several tech companies, which argues that vibe coding has given way to Context Driven Engineering organised around a spec/plan/act workflow."
  author: ["Hugo"]
  datePublished: "2026-02-06"
  publisher: "Eventuallycoding"
---

This post, whose title translates as "The impact of AI on the state of the art of software engineering in 2026", argues that 2025 turned AI-assisted development from an individual habit into something whole teams must industrialise. The author traces a progression from autocompletion with GitHub Copilot in 2021, through browser-based use requiring copy and paste, to coding assistants such as [[SoftwareApplication/claude-code]], Windsurf and Cursor running on the developer's machine in 2025, and compares the resulting change to the way automated test frameworks and CI/CD reshaped how software was built in the early 2000s.

Its method is a synthesis of conversations: engineers at several tech companies — among them Doctolib, Malt, ManoMano, Brevo, Ilek and Alan — contributed accounts that the post quotes throughout. It is organised around five themes: [[DefinedTerm/context-driven-engineering]] as the new paradigm, the spec/plan/act workflow, the ecosystem of AI rules, governance and industrialisation, and the human challenges.

## Key Points

- The post holds that where "vibe coding" dominated early 2025, people now speak rather of Context Driven Engineering or agentic engineering: instead of giving a prompt, you provide a complete context that includes the intent and the constraints, such as coding guidelines. It presents this as aimed at reducing the non-deterministic part of the process and making the quality of the output more reliable.
- Under this approach, it says, the specification becomes a first-class citizen again and a prerequisite before any code. It supports this with quoted practitioners, including one recommending that the plan and the implementation go into two separate pull requests so reviewers can focus on architecture and trade-offs at the plan stage.
- The reference workflow it identifies is spec, plan, act. The spec gathers the use cases and intent (whether called an RFC, ADR or PRD) and is usually reviewed by product experts; the plan lists every step needed to implement it, each doable by an agent autonomously, and is usually reviewed by senior engineers; the act step is implementation, done either in a copilot mode that validates each change or an agent mode that states the intent and checks the result.
- Having tried both [[SoftwareApplication/bmad]] and Spec Kit ([[SoftwareApplication/github-spec-kit]]), the author reports from that experience that they can easily lead to verbose over-documentation and a slower development cycle. The author adds, as an intuition, that digitally reproducing human processes that were already flawed should be avoided — questioning whether all the roles BMAD proposes are needed — and states as certain that a specification written for an AI must be simple and unambiguous, because verbosity can hurt a coding assistant's effectiveness.
- The "AI rules" ecosystem is described as context files read in addition to the spec — each assistant's own file, with [[DefinedTerm/agents-md]] as an attempt to harmonise them into a kind of README for AI, usable hierarchically per directory — plus skills that explain how to perform an operation, dedicated agents for specific tasks, and MCP servers that extend the agent's toolbox. Splitting context across several files is said to let each agent work with a reduced context.
- Several companies are described as pooling their skills, agents and rules in internal marketplaces or shared repositories to standardise AI-generated code, with contributions reviewed by internal guilds in one case; the post warns that anything installed from a public marketplace must be read first.
- Because instructions are regularly ignored or misread, teams are reported as making linting, test harnesses and code review mandatory around the agents, with human review still required by everyone interviewed. Whether a change to a context file is actually an improvement is presented as an open question; one engineer describes plans to run evaluations of skills in CI with prompt-testing tools, checking programmatically that a skill is triggered and judging the output with an LLM.
- Reported monthly costs per developer fall into three bands: about €20 for teams still adopting or using AI on a best-effort basis, about €200 for strong adoption, and €200 to €1,000 for multi-agent use integrated throughout CI, with most teams in the first two. The usual sequence described is adoption first, cost optimisation second.
- On the human side, the post reports that junior developers are at risk because much of the work once given to them is now done by AI, that all teams recognise the need to keep bringing juniors in, and that the author saw no initiative specifically adapting their training. It also reports hiring interviews being redesigned to allow AI tools, and onboarding made easier by up-to-date documentation and explicit guidelines.

## Context

The post is a practitioner's survey rather than a study: its evidence is quoted testimony from the companies that took part, and the cost bands are the author's synthesis of those conversations. It links out to other writing for several of its framings, including the terms it prefers to vibe coding.

Its conclusion welcomes the return of systems thinking — if you cannot explain what you want to do (the spec) and how you intend to do it (the plan), the author writes, AI will not save you but will produce technical debt at industrial speed — and suggests an unexpected side effect could be the end of "ego coding", the emotional attachment to one's own code. It closes by listing what remains open: sovereignty, local models, testing the reproducibility and quality of prompts, rising costs and the changing role of juniors.
