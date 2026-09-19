---
title: "How we built our multi-agent research system"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, evaluation, context-engineering, agent-tooling]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:9d24a3bfa582cdeb35b5470314362e43ded1cceb6659830329c69fe72147a2e4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's engineering account of taking its Research feature from prototype to production: an orchestrator-worker multi-agent architecture, the prompt-engineering principles that made coordination work, how the team evaluated a non-deterministic system, and the production reliability problems that followed."
  author: ["Jeremy Hadfield", "Barry Zhang", "Kenneth Lien", "Florian Scholz", "Jeremy Fox", "Daniel Ford"]
  datePublished: "2025-06-13"
  publisher: "[[Organization/anthropic]]"
---

This post is an engineering account of Anthropic's Research feature, which searches across the web,
Google Workspace and integrations, and of what taking it from prototype to production taught the team
about system architecture, tool design and prompt engineering. The architecture it describes is an
orchestrator-worker one: a lead agent analyses the user's query, develops a strategy and spawns
subagents that explore different aspects in parallel, each returning condensed findings for the lead
agent to synthesise.

The post's argument for why this shape helps rests on compression and on token capacity. Search is
framed as the business of distilling insight from a vast corpus, and subagents are presented as
facilitating that by working in parallel with their own context windows before condensing what matters
for the lead agent — with the separation of tools, prompts and trajectories also reducing path
dependency. The team reports that token usage alone explains most of the performance variance it
measured on one external browsing benchmark, which it reads as validating an architecture that adds
parallel reasoning capacity rather than one that is cleverer per token.

The post is unusually direct about where the approach does not apply and what it costs, and roughly
half of it is given over to problems rather than results: coordination failures that had to be
prompted away, the difficulty of evaluating a system that never takes the same path twice, and the
production engineering needed to keep stateful, long-running agents from compounding small errors into
failures.

## Key Points

- The team reports that a multi-agent system with Claude Opus 4 as lead agent and Claude Sonnet 4
  subagents outperformed single-agent Claude Opus 4 by 90.2% on its internal research eval, and gives
  as an example a request to identify all board members of the Information Technology companies in the
  S&P 500, which the single agent failed to answer through slow sequential searches.
- On the BrowseComp evaluation, three factors are reported to explain 95% of performance variance, with
  token usage alone explaining 80% and number of tool calls and model choice the other two. The post
  adds that upgrading to Claude Sonnet 4 was a larger gain than doubling the token budget on Claude
  Sonnet 3.7.
- The cost is stated plainly: agents typically use about 4× the tokens of a chat interaction, and
  multi-agent systems about 15× — so the approach requires tasks valuable enough to justify it.
- The post names domains it considers a poor fit today: those requiring all agents to share the same
  context or involving many dependencies between agents, and most coding tasks, which it says involve
  fewer truly parallelizable subtasks than research and where agents are not yet good at coordinating
  and delegating in real time.
- The architecture is contrasted with Retrieval Augmented Generation's static retrieval — fetching
  chunks most similar to a query — in favour of a multi-step search that adapts to findings as they
  arrive.
- The lead agent saves its plan to memory because a context window exceeding 200,000 tokens is
  truncated; a separate CitationAgent processes the documents and the draft report at the end to
  locate where citations belong.
- Early coordination failures are reported concretely: agents spawning 50 subagents for simple queries,
  searching endlessly for nonexistent sources, and distracting each other with excessive updates.
- Vague delegation is identified as a specific failure: instructions as short as "research the
  semiconductor shortage" led one subagent to the 2021 automotive chip crisis while two others
  duplicated work on 2025 supply chains. Each subagent is said to need an objective, an output format,
  guidance on tools and sources, and clear task boundaries.
- Effort-scaling rules were written into the prompts because agents judge effort poorly: roughly one
  agent with 3–10 tool calls for simple fact-finding, 2–4 subagents with 10–15 calls each for direct
  comparisons, and more than 10 subagents with divided responsibilities for complex research.
- A tool-testing agent that repeatedly used a flawed MCP tool and rewrote its description is reported
  to have produced a 40% decrease in task completion time for later agents using the new description.
- Two kinds of parallelism were introduced — the lead agent spinning up 3–5 subagents at once rather
  than serially, and subagents using 3+ tools in parallel — which the post reports cut research time by
  up to 90% for complex queries.
- On evaluation, the team argues for starting immediately with small samples, reporting that it began
  with about 20 queries representing real usage patterns. Its stated reason is that early changes tend
  to have dramatic effects — the illustration given is that a prompt tweak might lift a success rate
  from 30% to 80% — and that effects that size are visible in a handful of test cases.
- Its LLM judge scored outputs against a rubric of factual accuracy, citation accuracy, completeness,
  source quality and tool efficiency; the team reports that a single LLM call with one prompt emitting
  a 0.0–1.0 score and a pass-fail grade proved more consistent and better aligned with human judgement
  than multiple judges evaluating separate components.
- Human testing is reported to have caught what automation missed, including a consistent preference in
  early agents for SEO-optimized content farms over authoritative but lower-ranked sources such as
  academic PDFs and personal blogs, which was addressed by adding source quality heuristics to the
  prompts.
- The post describes agents as stateful systems where errors compound, so restarting from the beginning
  is not viable; its approach combines resuming from the point of failure, telling the agent when a
  tool is failing and letting it adapt, and deterministic safeguards such as retry logic and regular
  checkpoints.
- Full production tracing is credited with making non-deterministic failures diagnosable, and the post
  states that the team monitors agent decision patterns and interaction structures without monitoring
  the contents of individual conversations.
- Because agents run almost continuously and may be anywhere in their process during a deploy, the team
  uses rainbow deployments, shifting traffic gradually from old to new versions while both run.
- A named current limitation is synchronous execution: the lead agent waits for each set of subagents,
  which simplifies coordination but means it cannot steer them, subagents cannot coordinate, and one
  slow subagent blocks the system.
- The appendix adds three further practices: evaluating state-mutating agents on end state rather than
  turn-by-turn, managing long-horizon conversations by summarising completed phases into external
  memory, and having subagents write outputs to a filesystem and pass back lightweight references to
  avoid a "game of telephone" through the coordinator.

## Context

The performance figures are the team's own, measured on its own internal research eval, and the post
does not describe that eval's construction; the one external benchmark it cites, BrowseComp, is used to
support a claim about which factors explain variance rather than to report a score. The token-multiple
figures (4× and 15×) are given as observations from the team's data without a stated method.

The post's stated prompting philosophy is to instil heuristics rather than rigid rules, derived from
studying how skilled humans research — decomposing questions, evaluating source quality, adjusting
approach on new information, and choosing between depth and breadth. It also makes a claim about
emergent behaviour that qualifies its own prescriptions: small changes to the lead agent can change
subagent behaviour unpredictably, so the team frames the best prompts as frameworks for collaboration
defining division of labour, problem-solving approaches and effort budgets rather than as instructions.

Its closing framing — that in agent systems "the last mile often becomes most of the journey", and
that the gap between prototype and production is wider than anticipated — is offered as the general
lesson. The contrast it draws with traditional software is that where a bug there breaks a feature or
degrades performance, in an agentic system one failed step can send the agent down an entirely
different trajectory.
