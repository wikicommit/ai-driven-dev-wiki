---
title: "소프트웨어 3.0 시대를 맞이하며"
type: "schema:BlogPosting"
lang: en
tags: [claude-code, agent-architecture, harness-engineering, context-engineering, agent-skills]
sources:
  - type: url
    url: 'https://toss.tech/article/software-3-0-era'
    hash: sha256:6ac790bc800795959fea60814b1851fc12e9c37dd9fa189851b56547a5076740
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Toss Payments developer's argument that a coding agent such as Claude Code is a harness around a model whose parts map onto familiar layered architecture — slash commands as controllers, sub-agents as a service layer, skills as single-responsibility components, MCP as an adapter, CLAUDE.md as package.json — so that existing design principles and anti-patterns carry over, with human-in-the-loop questioning and token limits as the points where the analogy breaks."
  author: ["김용성"]
  datePublished: "2026-01-26"
  publisher: "토스테크"
---

The post opens with Andrej Karpathy's division of software into three stages, which it attributes
to a talk he gave at Y Combinator's AI Startup School: Software 1.0, where developers write explicit
logic describing *how*; Software 2.0, where data and training produce neural-network weights that
become the program; and Software 3.0, where one tells a large language model in natural language
*what* is wanted and the prompt is the program. It then argues that in practice a model on its own
cannot read files, call APIs or reach a database, and that what makes it useful is a harness — named,
the author explains, after the tack that lets people use a horse's strength. The post tabulates the
model's limits against the harness element that compensates for each: memory management for the
context window, fact grounding and retrieval for hallucination, a knowledge base for missing domain
knowledge, sessions and orchestration for statelessness, and tools and MCP for access to external
systems ([[DefinedTerm/software-3-0]], [[DefinedTerm/agent-harness]]).

Its central claim is that [[SoftwareApplication/claude-code]] is essentially such a harness for the
Claude model, and that its parts line up with the layered architecture developers already know.
From there it argues that familiar anti-patterns and design principles apply to agent design, that
the analogy fails at one important point — an agent can stop and ask — and that it also hides a
practical limit, since tokens behave like memory. The author closes that the centre of gravity in
development is shifting from writing code towards assembling and directing it, that the principles
of that assembly are not very different from familiar ones, and that one should "start building by
refactoring your mindset".

## Key Points

- The post maps Claude Code's components onto layered architecture: slash commands as controllers,
  the entry point for a user request ([[DefinedTerm/custom-slash-commands]]); sub-agents as a service
  layer that combines skills into a workflow, each with its own context and running independently
  like a separate thread; skills as domain components following the single-responsibility principle
  ([[DefinedTerm/agent-skills]]); MCP as the infrastructure or adapter layer that connects to external
  systems ([[DefinedTerm/model-context-protocol]]); and CLAUDE.md as the equivalent of
  `package.json` or `pom.xml`, holding stable project principles ([[DefinedTerm/claude-md]]).
- It advises that if CLAUDE.md is being edited often, what is being edited probably does not belong
  there, and that changing information such as the current issue or the day's priorities should be
  passed in conversation or through a sub-agent's context.
- Layered-architecture anti-patterns are given agent equivalents: a "God Skill" that handles
  everything in thousands of lines, a "Spaghetti CLAUDE.md" with instructions mixed together without
  structure, hard-coding API calls instead of going through MCP as tight coupling, a sub-agent that
  knows an MCP's internal implementation as a leaky abstraction, and circular calls between skills as
  circular dependency. Code smells such as feature envy, duplicated prompts across skills and a
  sub-agent calling ten skills in a row are carried over the same way.
- The difference the analogy does not explain is that a traditional service layer must define every
  branch in advance, whereas an agent can hand a decision back to the user mid-task through a
  question tool — in the post's phrase, the exception becomes a question
  ([[DefinedTerm/human-in-the-loop]]). The author contrasts all-or-nothing automation with partial
  automation and rollback after a mistake with confirmation before one.
- A good agent is described as one that knows when to ask: it should ask before hard-to-reverse
  actions such as deletion, deployment or external API calls, when there are several options with no
  right answer, and for costly or risky decisions, and proceed on its own for safely repeatable work,
  work covered by agreed conventions and easily reversed work.
- Tokens are treated as memory: the context window is working memory and token use is memory
  occupancy. The post gives rough figures — 500 to 2,000 tokens for a well-organized CLAUDE.md per
  project, 300 to 1,500 for each skill whenever it loads — and suggests asking Claude which files a
  workflow would read before running it, narrowing the instructions if the answer is more than
  expected.
- Deterministic logic such as a branch-naming convention should be moved into scripts, so that the
  model runs a script rather than interpreting the convention and spending tokens on it each time.
- Because Claude loads every skill's name and description into the system prompt at startup, the
  author warns against a "skill explosion" analogous to class explosion, and recommends applying the
  Law of Demeter: SKILL.md as a single entry point, like a facade, with detailed knowledge delegated to
  files under `references/` that are loaded only when needed ([[DefinedTerm/progressive-disclosure]]).
- A setup-and-config pattern is proposed for slash commands, by analogy with `npm init` and
  `npm config set`: a `/setup` command that analyses the repository, generates the structure and asks
  only where the choice is ambiguous, and a `/config` command for later adjustments.

## Context

The post is framed as advice to developers trained in Software 1.0: what to drop is the compulsion to
write every piece of logic explicitly, the attempt to define every exception in advance and the view
of a model as a smart autocomplete; what to keep is layer separation, single responsibility,
abstraction, dependency management, interface design, testability and code review. The author later
wrote [[BlogPosting/raising-productivity-floor-with-harness]] on the same blog, which the post lists
among the author's other writing. The post states that all its images were produced with generative
AI.

The comment thread is largely appreciative of the analogy. One commenter asks whether the author has
actually designed and run skills and sub-agents along these lines, observing that applying
architectural principles and getting an agent to behave reliably proved to be quite different
problems. Another suggests that because Software 3.0 differs from earlier paradigms so sharply, a
1.0-style mapping may help early understanding but could constrain thinking in the long run.
