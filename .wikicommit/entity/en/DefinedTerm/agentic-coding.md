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
  - type: url
    url: 'https://www.anthropic.com/research/claude-code-expertise'
    hash: sha256:1c729c8632d41020cb46941b451021196758377dbc5b749dc33500941ab4506f
  - type: url
    url: 'https://sourcegraph.com/blog/agentic-coding'
    hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c
review_status: pending
generated_at: "2026-08-21"
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

### What the division of labor looks like in measured practice

[[Report/agentic-coding-and-persistent-returns-to-expertise]] gives the mode a quantitative shape from roughly 400,000 [[SoftwareApplication/claude-code]] sessions between October 2025 and April 2026. Its central structural finding is that the split between human and agent falls along a consistent line: people make about 70% of the *planning* decisions — what to do, which approach, what counts as done — and about 20% of the *execution* decisions — which files to change, what to write, which commands to run. The report's own compact phrasing is that "people decide what to build, and the agent decides how to build it." Böckeler's "supervised agent" mode above describes the same relationship from the practitioner's side; this report is the measurement of how widely it holds.

Its second finding bears on who can work this way at all. The report separates *domain expertise at the task* from coding background, and finds the two behave differently: in code-producing sessions every one of the ten largest occupation groups lands within seven percentage points of software engineers on success, and that gap neither widened nor narrowed over seven months — but the person's rated expertise at the task strongly predicts both how much the agent does per instruction (about five actions and 600 words per prompt for novice-rated sessions against about 12 actions and 3,200 words for expert-rated ones) and whether the session succeeds. Most of that gain is at the low end: the step from novice to intermediate is larger than the step from intermediate to expert. The authors' reading is that agentic coding is "making a coding background less relevant to successful programming" while rewarding command of the problem domain — a claim about this vendor's own product and users, derived from transcript classifiers rather than observed outcomes.

### The loop, and the line against vibe coding

[[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]] states the definition operationally: software development where an autonomous agent plans, writes, tests, and iterates on code with limited human intervention, using tools — a shell, a test runner, code search, version control — to complete tasks across the development environment. Its test for the category boundary is what each kind of tool does when told "fix the failing build": autocomplete does nothing, because it needs you to start typing; chat reads a pasted error and suggests a fix you apply by hand; an agent opens a terminal, runs the failing test, reads the stack trace, greps for the broken function, edits the file, re-runs the test, and reports back when green. What it identifies as the behavioural leap is autonomous tool use — the agent deciding what to do next from what it just observed.

The loop it sets out has seven steps: prompt, context gathering, plan, execute, test, refine, output. Its claim about where quality comes from is that "what makes one agent better than another is rarely the model," since many tools draw on the same frontier model families — leaving retrieval, tool use, planning, sandboxing, and review as the differentiators, and context gathering as the step where most output quality is won or lost.

That guide also draws the sharpest available line between this term and [[DefinedTerm/vibe-coding]]: "vibe coding is a posture: trust the model, don't read the diff, keep prompting until it works," while "agentic coding is an architecture: the model is wired into tools, runs in a loop, and produces code that a human reviews against a definition of done." Its one-line reduction is that "the difference is who owns correctness," and its rule of thumb is that vibe coding works when the cost of being wrong is zero while agentic coding has to work when the cost of being wrong is a customer outage. The failure mode it identifies as characteristic of the practice at scale is [[DefinedTerm/eighty-percent-problem]].

## Related Terms

Agentic coding sits under [[DefinedTerm/ai-assisted-software-development]] and is carried out by tools covered under [[DefinedTerm/coding-agent]]. Named methodologies that structure it include [[DefinedTerm/agentic-engineering]], [[DefinedTerm/vibe-engineering]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/subagent-driven-development]], and [[DefinedTerm/ralph]]. Its central engineering constraint is covered under [[DefinedTerm/context-engineering]], and the coordination of several agents at once under [[DefinedTerm/multi-agent-orchestration]].
