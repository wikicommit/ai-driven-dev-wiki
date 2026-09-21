---
title: "The future of agentic coding: conductors to orchestrators"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, agents, coding-tools]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/future-agentic-coding/'
    hash: sha256:b6fa751c05fa1595dabeb21c14458cf4c51a1dd2997ce1edb3920fd3cebddf4a
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An argument that the software engineer's role is moving from implementer to manager of AI coding agents, distinguishing the conductor who guides one agent in real time from the orchestrator who delegates to a fleet of autonomous agents working in parallel."
  author: "Addy Osmani"
  datePublished: "2026-01-02"
---

This post argues that the role of the software engineer is shifting from implementer to manager, and names two points along that path: the **conductor**, who works closely with a single AI agent on a specific task, steering it in real time; and the **orchestrator**, who sets high-level goals for multiple autonomous agents, lets them carry out the implementation independently, and reviews and integrates what they produce. The change is framed as one in the question an engineer asks — from "How do I code this?" to "How do I get the right code built?"

Most of the post maps current tooling onto the two modes. CLI and in-editor assistants are presented as conductor tools, where the developer triggers each action and reviews the output immediately and the interaction is largely ephemeral. Cloud and background agents that clone a repository, branch, edit, run tests and open a pull request are presented as orchestrator tools, where the work lands as a reviewable artifact in version control rather than as suggestions in a chat window. The post then contrasts the modes directly on scope of control, degree of autonomy, synchronicity, the artifacts each leaves behind, and how a developer's effort is distributed across a task.

It closes by extending the orchestrator role beyond implementation to a pipeline of specialized agents covering planning, coding, testing, review, documentation and deployment, and by setting out the open problems that come with delegating at that scale. The author is explicit that this is a trajectory rather than a description of current practice.

## Key Points

- The engineer's role is described as moving from implementer to manager — "from *coder* to **conductor** and ultimately **orchestrator**" — with developers increasingly guiding agents to build the right code rather than writing it themselves.
- Conductor mode is characterized as a tight feedback loop with one agent: synchronous and interactive, typically in an IDE or CLI, with the developer verifying or modifying each suggestion and still performing manual steps such as creating branches, running tests and writing commit messages.
- Most conductor-mode interaction is described as ephemeral — once the session ends, any context or decisions not captured in code may be lost.
- Orchestrator mode is characterized by agents with enough agency to clone a repository, create branches, edit multiple files, compile and run tests, and iteratively refine a solution before presenting it, usually as a pull request.
- The post argues that orchestrator workflows leave a persistent trail — branches, commits and pull requests in version control, often linked to an issue — where conductor-style work leaves little explicit record unless the developer commits intermediate changes.
- The two modes are contrasted on five axes: scope of control, degree of autonomy, synchronous versus asynchronous interaction, artifacts and traceability, and the human effort profile.
- On the effort axis, the post's claim is that a conductor is actively engaged nearly the whole time the agent works, while an orchestrator's effort is front-loaded (writing the task description and setting up context) and back-loaded (reviewing and testing), with little needed in between — which is what allows one person to manage more work in parallel.
- Autonomous coding agents are framed as the next abstraction layer in a sequence running from assembly, to high-level languages, to frameworks and libraries, to AI autocompletion.
- The post argues the roles are fluid rather than rigid categories: a developer may act as conductor and orchestrator at different moments or simultaneously, and tools are blurring the line by supporting both real-time collaboration and async delegation.
- It sketches a future "AI team" of specialized agents — planning, coding, testing, code review, documentation, and deployment or monitoring — coordinated by a human who approves plans, resolves conflicts and gives final approval to deploy, and presents this as on the horizon rather than in place.
- Challenges named for the orchestrator model include quality control and trust, coordination and conflict between agents on a shared codebase, context and state that does not travel between agents, dependence on specification quality, debugging an agent that has gone astray, and accountability for license compliance and security in AI-written code.
- The post states that the human orchestrator or their organization ultimately carries responsibility for what ships, and recommends practices such as security scanning of AI-generated code and verifying dependencies.
- The post opens on the claim that up to 90% of software engineers use some kind of AI for coding, and gives no source for that figure.
- It reports that some developers delegate 10 or more pull requests per day to AI, treating the agent as an independent teammate rather than a smart autocomplete; this is offered as a report about early adopters, not as measured data.
- The author states an explicit caveat that not all or most code will be agent-driven within a year or two, while maintaining that this is the direction of travel.

## Context

The post sits alongside the author's other writing on the same shift and is largely a synthesis: it describes a change in working posture and then reads current tools against it, rather than reporting new measurements. Where it characterizes individual tools it draws on those vendors' own positioning, including quoted product descriptions, so its account of what any one tool does is a restatement of that vendor's claims rather than an independent evaluation.

Two of the author's stated interests bear on how the argument reads. The post's biography note describes Addy Osmani as a Member of Technical Staff at Anthropic working on Claude Code, after more than 14 years at Google leading developer experience across Chrome and, latterly, AI — and several of the tools the post surveys are made by those two companies. The post also promotes the author's own O'Reilly book on AI-assisted engineering.

The author adds a caution of his own alongside the productivity argument: that the code review loop is where human skill will continue to be applied, and that it needs work if the volume of generated code is not to become slop.
