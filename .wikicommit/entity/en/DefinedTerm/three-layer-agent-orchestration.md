---
title: "Three-Layer Agent Orchestration"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, multi-agent, agent-orchestration]
sources:
  - type: url
    url: 'https://techblog.openwork.co.jp/entry/ai-code-review-3-layer-architecture'
    hash: sha256:b4d6c939c7b4971dd50b6e2277243cbceb4d415eaf799742f1d75acf18a48570
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A code review architecture, named and described by an engineer at OpenWork, in which a parent agent routes a change to per-perspective review agents, each perspective is reviewed by several agents drawn from different model families, and only findings two or more of them raise independently are kept."
---

Three-layer agent orchestration is the name an engineer at OpenWork gives to the code review architecture described in [[BlogPosting/three-layer-agent-orchestration-ai-code-review]]. Work is divided across three tiers of agent: a first-layer parent agent that determines which technical domains a change touches, launches the appropriate sub-agents in parallel and consolidates their output into a pull-request comment; a second layer holding a context-collection agent, static-analysis agents and per-perspective scrutiny agents; and a third layer of review agents each confined to a single review perspective. The arrangement is a response to a specific observed failure of single-agent review — unstable finding quality, trivial findings and hallucinations, and the same point raised again on every round — rather than a general orchestration pattern.

## Usage

The term is used by its author to name one concrete system, and this wiki holds only that account of it. Two mechanisms carry most of its weight.

The first is dividing the review task. Rather than asking one agent to review from every angle, perspectives are separated in advance — architecture, business logic, clarity, code quality, performance, security, frontend specifics, test design — and a dedicated agent is assigned to each. The author's argument is the same one that applies to human reviewers: a smaller, bounded task yields more accurate output, and an agent given the whole surface at once loses precision. Which perspectives run is derived from the extensions of the changed files, so a change spanning backend and frontend launches both sets.

The second is agreement filtering. Each perspective is reviewed independently by four agents, and a scrutiny agent keeps only those findings that two or more agents raise about the same location for the same reason. A finding raised by a single agent is discarded as likely hallucinated, overreaching or trivial. The four agents are deliberately split across two model families so that biases particular to one vendor's model do not simply reproduce themselves four times; the author treats agreement across vendors as stronger evidence than agreement within one. The assessing role is itself an agent — the scrutiny agent's whole job is to compare the four outputs and adopt only what they agree on — but the criterion it applies is agreement among peers rather than a judgement of its own, which distinguishes it from the [[DefinedTerm/agent-as-a-judge]] techniques that assess an agent's execution directly.

A third element concerns the loop rather than the architecture: a context-collection agent reads the pull request's prior review comments and replies, separating points already raised from points an engineer has explicitly declined, and passes both forward so that neither is raised again. A declined point is treated as applying to the whole review rather than only to the location where it was declined.

## When It Applies

The account states the conditions under which the approach was viable. It assumes an existing body of agent-readable project documentation — skills and instructions the per-perspective agents are pointed at for project-specific rules — and the author notes that review precision depends on the quantity and quality of that documentation, making continuous monitoring necessary rather than a one-time build. It also assumes a billing arrangement under which launching many sub-agents is not separately charged; the author is explicit that this is why a design running dozens of agents could be adopted without weighing cost, which means the approach does not transfer unchanged to an arrangement that bills per agent invocation.

The approach is deliberately narrowed by four prohibitions placed on the review agents: no praising good points, no proposing implementations, no findings that violate YAGNI, and no findings about pre-existing code outside the change. The author singles out two of them — the ban on proposing implementations and strict adherence to YAGNI — as the ones effective against noise specific to AI review, reporting that without those constraints agents drift into detailed implementation suggestions and speculative future-proofing, away from identifying problems. Reviewing and fixing are kept separate on the same reasoning — fixing is the job of whichever coding agent performs it.

How well established the approach is: this is one engineer's system, reported by its author, in production with qualitative team feedback but without quantitative evaluation. The post sets out three criteria the author intends to measure — whether repeated reviews of the same pull request converge, whether findings are judged valid by engineers, and whether the agents match what a human reviewer would raise — each with an 80% pass line, and treats meeting them as a precondition for delegating review work to agents. None of those figures are reported as achieved. The author also frames the architecture's value as outlasting this particular application, arguing that agent orchestration is a promising direction independent of the tool or task, while allowing that this specific review system may cease to be worthwhile.

## Related Terms

- [[DefinedTerm/agentic-code-review]] — the broader practice this is one implementation of
- [[DefinedTerm/sub-agent-architecture]] — the general pattern of delegating to nested agents
- [[DefinedTerm/agent-as-a-judge]] — the related idea of using agents to assess agent output
- [[DefinedTerm/orchestration-tax]] — the cost side of coordinating many agents
