---
title: "设计流动摩擦：AI 原生团队的核心能力"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, software-process, code-review, coding-agents]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/ai-native-team-flow/'
    hash: sha256:69bb9a1bcd9dee1d4c27cb833a7801d667aff4479dcd6677e97b0e0f1238f4cd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A July 2026 Chinese-language blog post by Phodal Huang arguing that AI speeds up the roles of a software team unevenly, so that an AI-native team's real constraint shifts from producing code to the flow of change through the whole value stream, and proposing four ways to optimize that flow."
  author: ["Phodal Huang"]
  datePublished: "2026-07-18"
---

This post, written in Chinese by Phodal Huang, starts from an observation about how the effect of AI on
software development is usually discussed: in terms of individual productivity — how quickly a feature is
built, how many tasks one developer can push forward, how much code a coding agent generates. He accepts that
AI has sharply lowered the cost of execution, but argues that a faster developer does not make the team
proportionally faster: code, pull requests and tests all increase, while the time from a request being raised
to users receiving value does not shrink in proportion, because requirements, design, review, merging, testing
and release still queue up.

His thesis is that AI is moving software development from a problem of production capacity to one of flow
capacity. Once the marginal cost of generating code falls, what limits a team is whether requirements, design,
verification and feedback can move through the whole system at a matching pace.

## Key Points

- The author argues that AI accelerates different kinds of work very unevenly: it is good at generating text,
  code, pages and test skeletons, but cannot speed up customer interviews, organizational decisions, business
  trade-offs, user validation or cross-team coordination to the same degree.
- He argues that product work is limited by decision-making rather than by writing documents: developers and
  agents can now consume ready tasks within hours, faster than the team produces validated decisions, and AI
  used by product managers can add more requirements and hypotheses without adding requirements that are safe to
  build.
- He argues that design work is limited by experience judgment rather than drawing speed: when developers and
  agents fill in missing design decisions from existing components to avoid waiting, those decisions scatter
  across agents and branches, and the designer later has to review and correct them as rework.
- In his account, development can suffer upstream starvation (not enough mature requirements and designs) and
  downstream congestion (generated code queuing for review, merging and testing) at the same time. He
  illustrates this with hypothetical rates — requirement decisions at 1.2×, design at 1.5×, code production at 5×
  and review and testing at 1.3× — comparing development to a suddenly widened highway with too few cars at the
  entrance and an exit that cannot take the traffic.
- He describes how local speed-ups turn into system rework: agents resolve ambiguous requirements by picking a
  plausible interpretation and fixing it in code, as in his example of "administrators can export the member
  list", where front-end, back-end and test agents might each make a locally reasonable but different decision.
- He argues that more parallel development raises merge and ownership costs beyond Git conflicts, because agents
  can introduce different abstractions, naming and error handling in neighbouring modules, and that code review
  becomes context recovery when the reviewer sees only the final diff.
- He argues that more tests do not mean more verification capability, since tests generated from an
  implementation tend to show that the code runs as written rather than that the system implements the right
  business behaviour.
- He proposes four practices for optimizing the flow of change: form a minimal decision (business semantics,
  core path, risk boundaries and completion conditions) before much code is produced; absorb development
  capacity with small batches rather than larger requirements and pull requests; deliver context and evidence —
  goals, key assumptions, scope of impact, verification results and remaining unknowns — together with the code;
  and use backpressure to control parallelism, reducing concurrent new features or redirecting agents to
  verification and context work when review, testing or integration is saturated.

## Context

The post is an argument from the author's own perspective rather than a report of measurements; the rates it
gives for different roles are illustrative. Its description of generated code queuing at review overlaps with
what this wiki calls the [[DefinedTerm/review-bottleneck]]. The author closes by arguing that the
competitiveness of an AI-native team lies not in how many agents it can start at once, but in how much change it
can move, with little waiting, conflict and rework, from an unconfirmed idea to value users can perceive.
