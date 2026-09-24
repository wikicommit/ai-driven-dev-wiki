---
title: "Agent-Spec Driven Development"
type: "schema:DefinedTerm"
lang: en
aliases: ["ASDD", "Agent Spec Driven Development"]
tags: [spec-driven, agentic-coding, software-process, methodology]
sources:
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251201-pj-double-towards-ai-native-development/'
    hash: sha256:759a8657a3547ccd879fd3b7b260a4e7eda5e4cbc7fbb559a4b86aabecb602c4
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251225-mercari-ai-native-company/'
    hash: sha256:ed22a2b68e6e9e11d985d3ca79f7337bec6642349f4634d9b3bf2e9810a83cae
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A development method from Mercari's pj-double (Double) project in which a detailed, implementation-oriented specification — the Agent Spec — is produced first and agents then implement against it, with further agents checking the plan and the implementation."
---

Agent-Spec Driven Development (ASDD) is the name [[Organization/mercari]] gives to a development method it describes as its own optimised form of [[DefinedTerm/spec-driven-development]]. It has two steps: first, agents read the relevant material, research the technology and analyse the codebase to produce an implementation plan called the Agent Spec; second, agents implement against that Agent Spec. The Agent Spec lists the tasks and, for each one, its detailed design — which existing implementation to take as reference, which file to change and what change to make — and is meant to be unambiguous for the AI while remaining readable for humans. The project's account also characterises ASDD as a method that aims to generate even the SDD specification automatically.

## Usage

The term comes from Mercari's pj-double project, which proposed ASDD as a company standard in September 2025 ([[BlogPosting/pj-double-mercari-development-productivity]]). The two company accounts describe the Agent Spec with different emphasis. The project's own account describes it as a plan that agents generate and check. The company's CTO, in [[BlogPosting/choosing-ai-native-mercari-guiding-principles]], describes ASDD as an AI-friendly specification format — a template for an implementation-oriented design document that fits the existing codebase and the project's conventions. In the plan-generation step, an agent tuned to the company's knowledge base gathers primary information and drafts the plan, while a second agent checks whether the plan follows the service's coding conventions and clears set security criteria; the two alternate between revising and evaluating, and whatever uncertainty remains in the requirements or specification is put to the developer as questions. In the implementation step, an implementing agent, an agent that runs tests and static analysis, and an agent that verifies the result against the Agent Spec work together until the task is complete.

The project's account lists four benefits: the AI holds only the information needed for planning or for implementing, so its context stays dense; the plan can be reviewed, which makes the result predictable; implementation follows declaratively from the plan, which makes it reusable and transparent; and contributions to each step accumulate company-wide knowledge. Because implementation becomes a process that can be delegated to AI and run asynchronously, the account credits ASDD with the scalability it sees as the source of its productivity gains. Tasks are split at Agent Spec generation into the smallest reasonable working units, with one pull request per task; developers who adopted this reported that they no longer felt stressed reviewing AI-written code, and the project's current conclusion is that AI-written and human-written code show no significant difference in review effort.

In the CTO's account, the template defines API definitions, data models, database schema, processing flow, test scenarios, concrete implementation steps and dependencies between microservices. Its purpose is to make clear who implements which task, in which file and in which code style, so that anyone using an AI agent implements to the same quality and conventions; small task granularity is built into the template so that agents can code accurately. That account also presents the Agent Spec as the base for agents across processes beyond coding: backend, frontend and mobile development, QA test-case generation, AI review, customer-support specification research, risk management and compliance checks. It is also used as the specification for PJ Aurora, a UI-generating agent. The CTO contrasts ASDD with intuitive [[DefinedTerm/vibe-coding]]: its point is an agentic approach that gives anyone a reproducible development regulation, and the Agent Spec is meant to be grown continuously from best practices collected inside the company.

## When It Applies

ASDD is designed for the phase after a specification and design have been settled — what the pj-double account calls the downstream work of implementation. It assumes that the primary information the agents need is available to them, which in Mercari's case means a knowledge base the plan-generating agent is optimised for, and in practice it splits work at Agent Spec generation into the smallest reasonable units that can run. The CTO's account makes that assumption explicit: ASDD's quality depends heavily on the quality of the context supplied when the Agent Spec is written, and without suitable context it does not work as expected — which is why the company runs a knowledge-management effort alongside it to organise past specifications and decision history.

The pj-double account reports how it went wrong upstream. Because ASDD will generate an implementation even from a low-confidence request nobody has agreed to, the AI fills the gaps itself and produces work that is "technically correct but agreed by no one". Developers reported that reaching agreement among stakeholders was what took the most time, that auto-generated documents carry no rationale and so do not work as a medium for agreement, and that reviewing an Agent Spec rewritten from scratch each time could take longer than writing it by hand. The post's author adds their own analysis: long generated Agent Specs exceed developers' cognitive load, and they often mix primary information with generated content of uncertain accuracy. The project's own diagnosis was that it had treated work that needs thinking and deciding together with AI as work to hand over to AI.

How well established it is: ASDD is one company's internal method, described by the team that built it and by the company's CTO. The evidence offered is that team's own measurement — projects that adopted spec-driven development, which ASDD builds on, averaged more than a 150% speed improvement against their effort estimates, a figure gathered from subjective comparisons of estimated and actual effort — together with qualitative feedback from developers. No separate figure for ASDD itself is given.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/spec-driven-agentic-development]]
- [[DefinedTerm/review-bottleneck]]
- [[DefinedTerm/sub-agent-architecture]]
