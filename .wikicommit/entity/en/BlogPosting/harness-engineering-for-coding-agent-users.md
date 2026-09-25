---
title: "Harness engineering for coding agent users"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, harness-engineering, verification]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html'
    hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An April 2026 article by Birgitta Böckeler on martinfowler.com that proposes a mental model for the outer harness users build around a coding agent: guides and sensors, computational and inferential, steered by humans and distributed across the change lifecycle."
  author: ["Birgitta Böckeler"]
  datePublished: "2026-04-02"
  publisher: "martinfowler.com"
---

This article sets out a mental model for [[DefinedTerm/harness-engineering]] from the point of view
of people who use coding agents rather than build them. It starts from the problem of trust: to let
coding agents work with less supervision we need ways to increase confidence in their results, and
the author names a natural trust barrier with AI-generated code — LLMs are non-deterministic, do not
know our context, and do not really understand the code. The article states that it updates, and
supersedes, an earlier memo in which the author recorded her first impressions of harness engineering.

Taking the shorthand that a harness is everything in an AI agent except the model itself, the author
narrows the term to the bounded context of using a coding agent. Part of that harness is already
built into the agent by its builders; users add an **outer harness** of their own for their use case
and system. The article's model for that outer harness is a system of
[[DefinedTerm/guides-and-sensors]], and it goes on to discuss when to run them, what they regulate,
what makes a codebase amenable to them, and what role remains for humans.

## Key Points

- A well-built outer harness is said to serve two goals: raising the probability that the agent gets
  things right the first time, and providing a feedback loop that self-corrects as many issues as
  possible before they reach human eyes — reducing review toil, increasing system quality, and
  wasting fewer tokens.
- Guides (feedforward controls) steer the agent before it acts; sensors (feedback controls) observe
  after it acts and help it self-correct. Used separately, the author argues, one gets an agent that
  keeps repeating mistakes (feedback only) or one that encodes rules but never learns whether they
  worked (feedforward only).
- Both guides and sensors come in two execution types: computational (deterministic and fast, such as
  tests, linters and type checkers) and inferential (semantic analysis, AI code review,
  [[DefinedTerm/llm-as-a-judge]]), the latter slower, more expensive and more non-deterministic.
- Engineering a user harness is described as a specific form of
  [[DefinedTerm/context-engineering]], which provides the means of making guides and sensors
  available to the agent.
- The human's job is to steer the agent by iterating on the harness: whenever an issue happens
  multiple times, the controls should be improved to make it less likely or prevent it. Agents can
  help here too — writing structural tests, drafting rules from observed patterns, scaffolding custom
  linters.
- Drawing on continuous integration and delivery, the article argues for keeping quality left:
  sensors should be spread across the lifecycle by cost and speed, with fast checks before
  integration or even before a commit, more expensive ones (such as mutation testing or a broader
  code review) after integration, and continuous sensors watching for gradual drift in the codebase
  and for runtime signals such as degrading SLOs.
- The author distinguishes three regulation categories: a **maintainability harness** (internal code
  quality, currently the easiest because much tooling exists), an **architecture fitness harness**
  (guides and sensors for architecture characteristics, essentially fitness functions), and a
  **behaviour harness** (whether the application functionally behaves as needed), which she calls
  the elephant in the room.
- Mapping maintainability controls against coding-agent failure modes she had catalogued earlier,
  the author finds computational sensors reliably catch structural problems, LLMs partially and
  expensively catch problems needing semantic judgment, and neither reliably catches some
  higher-impact problems such as misdiagnosis, over-engineering and misunderstood instructions.
- For behaviour, the approach the author sees most among people giving agents high autonomy — a
  functional specification as feedforward and a green, high-coverage AI-generated test suite plus
  manual testing as feedback — puts, in her view, too much faith in AI-generated tests.
- Not every codebase is equally amenable to harnessing; the article calls this
  [[DefinedTerm/harnessability]], and suggests that [[DefinedTerm/harness-templates]] for common
  service topologies may emerge in the future.
- Human developers bring their skills and experience as an implicit harness, which a coding agent
  lacks. Harnesses try to externalise and make that explicit but can only go so far, so a good
  harness should aim not to eliminate human input but to direct it to where it matters most.
- Open questions the article raises include how to keep a growing harness coherent, how far agents
  can be trusted with trade-offs when instructions and feedback conflict, whether sensors that never
  fire indicate quality or poor detection, and the need for a way to evaluate harness coverage and
  quality comparable to what code coverage and mutation testing do for tests.

## Context

The author presents the model as describing techniques already happening in practice and as a way to
lift the conversation above individual features, such as skills and MCP servers, to the design of a
system of controls. The three regulation categories are offered as ones that "seem useful to me as of
now". Among examples from the current discourse she cites published
accounts from an OpenAI team and from Stripe, and stories from teams at Thoughtworks. The article's
acknowledgements say that GenAI (Claude and Claude Code) was used for research, pulling in ideas from
existing notes, and polishing the language.
