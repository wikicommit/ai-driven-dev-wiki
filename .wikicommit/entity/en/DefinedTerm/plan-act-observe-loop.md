---
title: "Plan-Act-Observe Loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/plan-act-observe/'
    hash: sha256:99a26fb175ac533fa131214fdd349e53534181f5243b2ad5663d9f7ffab635f4
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The core iterative cycle a coding agent follows: plan an approach, act by writing or editing code, and observe the result, then repeat based on what was observed."
---

The Plan-Act-Observe loop is the core cycle a coding agent follows while working: it plans an approach, acts on it, and observes the result, then uses that observation to plan its next step. In the planning phase the agent reads the task, examines relevant code, and decides on an approach; in the acting phase it writes code, edits files, and runs commands; in the observing phase it checks compiler output, test results, and error messages. The cycle repeats until the agent completes the task, hits a limit (token budget, time limit, or maximum iterations), or gets stuck and asks for help.

## Usage

Because the agent plans before acting, front-loading context can improve the planning phase; because it observes results, providing clearer feedback — test output, error messages, type checking — improves the observation phase. The quality of each phase affects how quickly the agent converges on a correct solution: better planning produces more coherent first attempts, and better observation (recognizing when something is genuinely fixed rather than merely suppressed) speeds convergence. A known failure mode is the agent getting stuck cycling between two fixes, each breaking what the other repaired, which guardrails on iteration count are meant to limit.

## Related Terms

[[DefinedTerm/ai-coding-agent]], [[DefinedTerm/tool-use]], [[DefinedTerm/chain-of-thought]], [[DefinedTerm/guardrails]], [[BlogPosting/self-improving-agents]]
