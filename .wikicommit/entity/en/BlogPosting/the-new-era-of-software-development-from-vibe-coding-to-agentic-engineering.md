---
title: "A Nova Era do Desenvolvimento de Software: do Vibe Coding à Engenharia Agêntica"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, agentic-engineering, context-engineering, sdlc]
sources:
  - type: url
    url: 'https://elisaterumi.substack.com/p/a-nova-era-do-desenvolvimento-de'
    hash: sha256:71ba07035b825f6f88ef48134eb16acd915eb8d9d41a8ab62e823dcceff1f7dd
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Portuguese-language essay arguing that AI has shifted the developer's value from implementation to technical judgement, and tracing the move from vibe coding to agentic engineering, in which developers design the constrained environment that agents work within."
  author: ["Elisa Terumi"]
  datePublished: "2026-07-04"
  publisher: "Explorando a Inteligência Artificial"
---

This post, whose title translates as "The New Era of Software Development: from Vibe Coding to Agentic Engineering", argues that code has stopped being the product. Because tools such as Claude Code, Codex, Gemini CLI, Cursor, Windsurf and GitHub Copilot can generate thousands of lines in minutes, writing code is no longer the main bottleneck; the challenge becomes making sure that code is correct, secure, sustainable and aligned with the project's goals. The author condenses the shift into two lines — the AI writes, the developer decides — and calls it perhaps the largest transformation in software engineering since high-level languages appeared.

The essay then follows a progression. [[DefinedTerm/vibe-coding]] is described as the phase most people pass through first, well suited to prototypes and low-risk work but reaching its limits in production systems, and [[DefinedTerm/agentic-engineering]] as the new paradigm that emerges at that point: a way of developing software in which agents work inside an environment the developers have deliberately designed. The author credits a document on the new SDLC by authors from Google as the inspiration for its ideas, and presents the post as the author's own interpretation and analysis of the transformations AI is bringing to software engineering.

## Key Points

- Vibe coding is defined as describing what you want in natural language, accepting the code the AI produces, and pasting any error message back into the chat for the AI to fix. The post calls it extremely productive for prototypes, personal projects, proofs of concept, simple automations and trying out new technology.
- Its limit, as the post frames it, is production: there, more structured validation, architecture and automated testing become necessary.
- Agentic engineering is described as more than using AI agents. Agents work inside an environment the developers have designed — architectural documentation, development rules, authorised tools, isolated execution environments, automated tests, CI/CD pipelines and security policies — so the focus moves from generating code to building a reliable process for generating code.
- In the post's factory analogy, the developer used to be the worker assembling each part and is now closer to the factory manager, who defines the specifications, the agents responsible for implementation, the tests, the quality criteria and the validation mechanisms.
- The post describes an "80% problem": the first 80% of development tends to be very fast, while the final 20% — edge cases, error handling and integration subtleties that need deep contextual knowledge — still takes considerable effort, which is why it holds that human supervision remains indispensable.
- It summarises an agent as "Agent = Model + Harness": the model supplies reasoning, and the [[DefinedTerm/agent-harness]] supplies tools, memory, instruction files, sandboxes, permission control and guardrails. The post holds that when an agent misbehaves, the problem usually lies in how that environment was designed rather than in the model.
- [[DefinedTerm/context-engineering]] is presented as the new core skill, with the central difficulty being the balance between static context — rules that are always loaded and costly in tokens, such as an [[DefinedTerm/agents-md]] file — and dynamic context, meaning skills and documents loaded only on demand.
- The post names two working modes for the developer ([[DefinedTerm/conductor-and-orchestrator-modes]]): the conductor, who works side by side with the agent inside the IDE, continually reviewing its suggestions; and the orchestrator, who sets high-level goals for several agents running autonomously in the background and reviews only final deliverables such as pull requests.
- On cost, the post contrasts vibe coding's very low barrier to entry but high token consumption, rework and maintenance over time with agentic engineering's larger initial investment in documentation, architecture, tests and processes, which it says significantly reduces future operating cost.

## Context

The essay presents itself as the author's interpretation and analysis rather than as original research. Its subtitle cites a figure of 41% of all new code being generated by AI, which the body does not return to or source.

Its conclusion restates the thesis for the profession: AI increasingly solves code generation without reducing developers' importance, moving their focus to architecture, decision-making, validation, context and governance. Its conclusion states that the interface of the future will not be the programming language but intent, and that the professionals who learn to design systems, coordinate agents and build reliable architectures will lead the next generation of software development.
