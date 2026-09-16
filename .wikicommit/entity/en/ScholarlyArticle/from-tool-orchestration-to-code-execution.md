---
title: "From Tool Orchestration to Code Execution: A Study of MCP Design Choices"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, mcp, security]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.15945
    hash: sha256:60c6e2cb0a71555099b80957589b805892374a300cde0b5fcf920cd270f4c095
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The first empirical comparison of traditional context-coupled MCP and Code Execution MCP (CE-MCP) agent architectures across efficiency, task quality, and security, using the MAESTRO threat-modeling framework to identify sixteen CE-MCP-specific attack classes and validate four representative exploits."
  author: ["Yuval Felendler", "Parth A. Gandhi", "Idan Habler", "Yuval Elovici", "Asaf Shabtai"]
  datePublished: "2026-02-17"
---

This paper presents the first empirical comparison of traditional [[DefinedTerm/model-context-protocol]]
(MCP) and [[DefinedTerm/code-execution-mcp]] (CE-MCP) agent architectures across efficiency, task
quality, and security. Using the MCP-Bench benchmark across 10 representative MCP servers and three
GPT-4 model variants, it evaluates task behavior, tool utilization patterns, execution latency, and
protocol efficiency as the scale of connected MCP servers and available tools increases. It applies
the MAESTRO threat-modeling framework to CE-MCP, identifying sixteen attack classes across five
execution phases, and validates four representative exploits through adversarial scenarios,
proposing a layered defense architecture of pre-execution validation and semantic gating, isolated
execution, and post-execution semantic gating.

## Key Points
- Formalizes the architectural distinction between context-coupled (traditional MCP) and
  context-decoupled (CE-MCP) tool-orchestration models, and their scalability trade-offs
- Reports that CE-MCP consistently reduces token usage, execution time, and number of interaction
  turns compared to traditional MCP across all evaluated model and server configurations, while
  maintaining comparable task fulfillment in most settings
- Finds that CE-MCP is best suited to complex, multi-tool tasks with structured, data-parallel
  workflows, while traditional MCP retains an advantage on context-sensitive, heavily textual, or
  highly iterative tasks — attributing the performance difference to architectural execution
  semantics rather than to model choice
- Identifies sixteen CE-MCP-specific attack classes across five execution phases (tool discovery,
  code generation and planning, code execution, result return and validation, and runtime impact)
  using the MAESTRO framework, and empirically validates four representative attacks (context
  injection via discovery artifacts, hijacking via adversarial context, execution sink
  manipulation, and authorization state corruption), several of which achieve their effect without
  any sandbox escape
- Proposes a three-stage, defense-in-depth mitigation architecture — pre-execution static
  validation and semantic gating, isolated and monitored execution, and post-execution semantic
  gating — which blocked all demonstrated attacks in the paper's trials, though the authors note it
  was not stress-tested against adaptive adversaries aware of the defenses

## Notes
- This is an arXiv preprint rather than a peer-reviewed publication at the time of this source; the
  authors state its open-science artifacts (agent implementation, Docker configuration, attack
  scripts, and a modified MCP-Bench) are publicly available
- The authors frame CE-MCP as a distinct architectural trade-off rather than either a strict
  improvement or an inherently flawed design, and caution against treating it as categorically
  unsafe
