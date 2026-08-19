---
title: "agentic coding"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://en.wikipedia.org/wiki/AI-assisted_software_development'
    hash: sha256:f4657a94008a181fc7fcb677deb754a02e6645300e34672335697956c63b365b
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/13-role-of-developer-skills.html'
    hash: sha256:3e83946dbe5213c00520e761c6664ebc2bacfbf1f9f9a291ba8e521c4cdccf5c
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The use of AI agents for software development — tools that autonomously interact with a development environment, run commands and tests, and iterate on code toward a goal, rather than only responding to a prompt with text."
  termCode: ""
  inDefinedTermSet: ""
---

Agentic coding is the use of AI agents for software development, as distinct from AI that only responds to a prompt with generated text. It is a subset of [[DefinedTerm/ai-assisted-software-development]] in which the tool takes actions in a development environment — reading files, running commands and tests, reacting to the results, and iterating — which is what makes an unattended or partly-attended session possible at all.

## Usage

In practice the term names a mode of working rather than a specific tool. Böckeler's account in [[BlogPosting/the-role-of-developer-skills-in-agentic-coding]] describes what the IDE-integrated agentic modes she used could do as of early 2025: execute tests and other development tasks and try to immediately fix the errors that occur, automatically pick up on and try to fix linting and compile errors, do web research, and in some cases use browser preview integration to read console errors or inspect DOM elements. She characterises the way she actually worked with them as a "supervised agent" mode, in which she intervened, corrected and steered constantly — and argues that the developer skills this requires are the ones worth preserving and training for. Her taxonomy of what goes wrong when that supervision is absent is covered under [[DefinedTerm/impact-radius]].

Anthropic's [[Report/2026-agentic-coding-trends-report]] describes a different vantage point on the same practice, from a vendor forecasting the year ahead. Its central framing is that the engineer's role moves from implementer to orchestrator: the value of a contribution shifts to system architecture design, agent coordination, quality evaluation, and strategic problem decomposition, with the primary human role being to orchestrate agents that write code, evaluate their output, and ensure the system solves the right problems. The report also reports a tension it calls the collaboration paradox — developers using AI in roughly 60% of their work while reporting they can "fully delegate" only 0–20% of tasks — which it resolves by arguing that agentic coding is collaborative by nature rather than a handover, with engineers delegating easily-verifiable, well-defined, or repetitive work and keeping design-dependent judgment for themselves.

The two accounts agree on the shape of the practice while differing in tone: one arrives at constant human steering as a limitation to design around, the other as the intended operating model.

## Related Terms

Agentic coding sits under [[DefinedTerm/ai-assisted-software-development]] and is carried out by tools covered under [[DefinedTerm/coding-agent]]. Named methodologies that structure it include [[DefinedTerm/agentic-engineering]], [[DefinedTerm/vibe-engineering]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/subagent-driven-development]], and [[DefinedTerm/ralph]]. Its central engineering constraint is covered under [[DefinedTerm/context-engineering]], and the coordination of several agents at once under [[DefinedTerm/multi-agent-orchestration]].
