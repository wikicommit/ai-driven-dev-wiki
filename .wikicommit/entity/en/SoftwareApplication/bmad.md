---
title: "BMAD (Breakthrough Method for Agile AI-Driven Development)"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent-systems, spec-driven-development, agent-skills]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
  - type: url
    url: 'https://github.com/bmad-code-org/BMAD-METHOD'
    hash: sha256:94658f1b099fdfd9a13035cb23b43dabcfde0183189e7264e6b28882487bb37e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A multi-agent framework, published on GitHub, that organizes AI agents into specialized software-development roles — its own documentation naming default agents for analysis, product, architecture, development, UX and technical writing — and tackles projects through up-front planning, task sharding into focused 'story files,' and parallel agent execution."
  applicationCategory: "Multi-agent AI development framework"
  featureList: "Up-front agentic planning producing PRDs and designs; Scrum-like sharding into story files with focused context; parallel execution by specialized role agents; phased flow with optional analysis, planning, solution and implementation stages plus a quick flow for smaller tasks; installation via npx"
---

BMAD (Breakthrough Method for Agile AI-Driven Development) is a multi-agent framework, published on GitHub, that [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites repeatedly: among other places as "a more comprehensive example" of engineered multi-agent teams than Anthropic's Claude Code (whose architecture shifted from a monolithic agent to spawning specialized sub-agents), as "a comprehensive industry example" of its [[DefinedTerm/ai-teammate-lifecycle-engineering]] (Lifetime Teammates) principles, and in a dedicated subsection on multi-agent and agile-inspired frameworks. That paper gives agile roles by example — Product Owner, Architect, Developer, Tester — and BMAD takes the "team" metaphor literally to tackle complex projects within a full-fledged agile structure.

The project's own repository, `bmad-code-org/BMAD-METHOD`, describes BMad Method as "the agile way"
to do what it calls Ai Driven Development (AiDD) — a term it uses for the whole effort rather than
only the code: what to build, how it holds together, and how it changes as the team learns. Its
tagline is to turn an idea or change request into working software "without giving up the thinking",
and its stated reason for existing is that coding assistants, effective at implementation, often turn
unstated assumptions into code; BMad's agents and workflows are meant to make the important decisions
explicit and preserve them as context for later work while the developer stays in control. The method
is free and open source under the MIT license, with no paywalled workflows, and the names BMad and
BMAD-METHOD are trademarks of BMad Code, LLC.

## Capabilities

Up-front agentic planning yields PRDs and designs; a Scrum-like sharding step then creates "story files" holding focused context for a task; specialized agents execute these in parallel. The paper credits BMAD's role specialization, task sharding, and high parallelism as mapping well to [[DefinedTerm/structured-agentic-software-engineering]] (SASE)'s own N-version programming and orchestration.

The README frames the method around process that sizes itself to the work: small changes go straight
to build, while complex work gets the planning depth it needs, and the same method is meant to serve
both a weekend prototype and a system with years of history. Its delivery loop has entry points to
match — a vague notion starts at Clarify, a big clear idea at Plan, and a small change at Build and
verify, with a Learn and adjust step looping back to Plan — and briefs, specifications and architecture
can be carried into an existing delivery workflow instead of using BMad end to end. Among the benefits
it lists are durable context carried forward instead of re-explained in every chat, specialized
perspectives (product, architecture, UX, development and testing), and structured workflows and
multiple-agent discussions that do not hand over judgment; it can also start on an inherited codebase
by first establishing verified context on what is actually there.

[[ScholarlyArticle/from-prompt-to-process]] describes the same framework from its own documentation and
adds detail on both the roles and the flow. Its unit of organisation, that study says, is not the
individual agent but an ecosystem of modules, workflows, skills and artifacts, with a phased flow
covering optional analysis, planning, solution and implementation, plus a quick flow for smaller tasks;
installation is via `npx bmad-method install`. The default agents it names represent classic software
development functions — analyst, product manager, architect, developer, UX designer and technical
writer — and each role triggers workflows that produce documents or decisions for the next phase. That
progression is what the study identifies as the point: the architecture informs stories, stories inform
implementation, and reviews and readiness checks act as gates, which that study says prevents the
implementation agent from operating only on a short instruction.

The install command above is the one that study gives. The repository's current README describes a
different set of install routes: the method is distributed as [[DefinedTerm/agent-skills]] installed
with `npx skills add bmad-code-org/BMAD-METHOD`, or as a Claude Code or Codex plugin from the
project's plugin marketplace, and it needs an AI coding tool that supports skills plus the `uv` tool
for setup. After installation a `bmad` hub skill runs setup and gives guidance on what to do next, and
a `bmad-build` skill is invoked with the change the developer wants.

## Adoption & Ecosystem

Beyond the core method, the project publishes official modules: BMad Builder (for building skills,
workflows and agents), a Creative Intelligence Suite of creative-thinking partners, BMad Test
Architect as an enterprise testing add-on, BMad Loop, which builds, verifies and runs retrospectives on
a whole epic unattended, and BMad Game Dev Studio for games in engines such as Unity, Unreal, Godot and
Phaser. Selected workflows are also packaged as "web bundles" — Google Gemini Gems and ChatGPT Custom
GPTs — so that planning can happen in an existing web subscription and the resulting artifacts be
brought into a coding tool for implementation.

The paper contrasts BMAD with its own proposed SASE, stating SASE goes further by converting review feedback into persistent [[DefinedTerm/mentorscript]] rules ("mentorship-as-code") and by specifying dedicated environments and disciplines — the [[DefinedTerm/agent-command-environment]] for human coaching and orchestration, the [[DefinedTerm/agent-execution-environment]] for agent execution, and [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] for memory, lifecycle, and agent-native tooling.

Under the [[DefinedTerm/six-dimension-process-taxonomy]], BMAD scores 2 on specification, 2 on context,
2 on roles, 1 on execution, 2 on validation and 1 on portability — a total of 10 out of 12, the highest
of the six frameworks that study assessed. It is one of the two frameworks there that treat roles and
validation as central rather than leaving them weak, and one of the two named as giving partial answers
to the tension between agent autonomy and governance by inserting human review points. That study calls
the opposition between process depth and portability its most informative pattern and gives BMAD as its
deepest-process case, where that depth comes with reduced portability and execution. The scores express that study author's judgement
from official documentation rather than an independent empirical measurement.

The strength that study credits BMAD with is turning human-AI collaboration into a process recognisable
by software teams — making PRDs, architecture, epics, stories and reviews consumable by agents instead
of replacing agile practices. Its stated fragility, from a research standpoint, is that effectiveness
depends on usage discipline and remains without independent empirical evaluation: the framework offers
structure, but when that structure improves quality, time, cost, maintenance and alignment has still to
be measured. The dominant risk it records is process cost and the need for that discipline.
