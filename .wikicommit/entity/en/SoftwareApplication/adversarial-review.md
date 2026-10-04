---
title: "Adversarial Review"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agentic-code-review, multi-agent]
sources:
  - type: url
    url: 'https://github.com/alecnielsen/adversarial-review'
    hash: sha256:b6388c19b88afabd80a5fbec468b2934e258bedaf755ba94f82d774704eb71a7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "An experimental open-source shell tool that runs multi-agent code review with Claude and GPT Codex in an adversarial debate loop: the two agents review code independently, critique each other's findings, and Claude synthesizes the debate and implements the fixes."
  applicationCategory: "Code review tool"
---

Adversarial Review is an open-source command-line tool that reviews a codebase by having two AI coding agents, [[SoftwareApplication/claude-code]] and [[SoftwareApplication/openai-codex]], review it independently and then argue over each other's findings. It is a shell script driven against a target directory, and its README describes it as an experimental prototype, released under the MIT license.

The README states the rationale for the adversarial setup in four parts: different models catch different problems, cross-validation filters out incorrect findings, disagreements are settled through structured debate, and issues both agents agree on can be treated as high-confidence fixes. It says the approach is based on patterns from the asimov-ralph project and on research on AI debate.

## Capabilities

Each iteration runs a four-phase loop:

1. **Independent reviews** — Claude and Codex each review the code, in parallel.
2. **Cross-review** — each agent reviews the other's findings.
3. **Meta-review** — each agent responds to the other's critique of its own findings.
4. **Synthesis** — Claude reads all the debate artifacts, decides which issues are valid, and implements the fixes it rates high or medium confidence.

The loop then returns to the first phase to verify the fixes. It ends when both agents report no issues in the first phase, when the synthesis step signals completion, when the maximum number of iterations is reached (three by default), or when a circuit breaker opens. The circuit breaker is meant to stop runaway loops, and trips on three iterations with no fixes made, five or more iterations in which the agents cannot agree, or three or more iterations that keep finding the same unfixable issues.

Each agent ends its output with a structured status block giving the number of issues found broken down by severity, a confidence level, an exit signal and a one-line summary, which the script parses to drive the loop. Every phase writes its output to a per-iteration Markdown artifact, so the whole debate can be read afterwards. The review prompt for the first phase can be replaced with a custom one, and iteration count, per-agent timeout, verbose output and a dry run can be set by flag or environment variable.

## Adoption & Ecosystem

The tool requires the Claude Code and Codex CLIs, plus `jq`. The README puts the cost at up to about 21 API calls for a review that runs to the default maximum of three iterations, and lists supporting other models such as Gemini or local LLMs, weighted voting based on historical accuracy, cost tracking and a web UI as possible improvements. The arrangement it automates — a second model examining the first model's findings — is a form of [[DefinedTerm/cross-model-review]], taken here to a symmetric debate in which both models review and critique, applied within [[DefinedTerm/agentic-code-review]].
