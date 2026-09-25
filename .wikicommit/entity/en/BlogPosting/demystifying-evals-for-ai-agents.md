---
title: "Demystifying evals for AI agents"
type: "schema:BlogPosting"
lang: en
tags: [agent-evaluation, evals]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents'
    hash: sha256:aff580d13a3f50486ad4c230339a558e501350b4038901e8093333bdd7842ca9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post on designing automated evaluations for AI agents: the components of an agent eval, the trade-offs between code-based, model-based and human graders, approaches by agent type, metrics for non-determinism, and a step-by-step roadmap from no evals to trustworthy ones."
  author: ["Mikaela Grace", "Jeremy Hadfield", "Rodrigo Olivares", "Jiri De Jonghe"]
  datePublished: "2026-01-09"
  publisher: "[[Organization/anthropic]]"
---

The post argues that the capabilities that make agents useful — autonomy, intelligence and flexibility across many turns of tool calls and state changes — are the same ones that make them hard to evaluate, and that good evaluations let teams ship agents with more confidence instead of catching problems only in production. It focuses on automated evals that can run during development without real users, and draws on [[Organization/anthropic]]'s internal work and its work with customers.

It sets out a vocabulary for agent evaluation: a **task** with defined inputs and success criteria; **trials**, repeated attempts at a task because outputs vary between runs; **graders** that score some aspect of performance through one or more assertions; the **transcript** (or trace, or trajectory) recording everything in a trial; the **outcome**, the final state of the environment; an **evaluation harness** that runs evals end to end; the **agent harness** or scaffold that lets a model act as an agent; and an **evaluation suite** of related tasks. Evaluating "an agent", it notes, means evaluating the harness and the model together. From there it compares grader types, discusses coding, conversational, research and computer-use agents, and ends with a practical roadmap.

## Key Points

- Code-based graders are fast, cheap, objective and reproducible but brittle to valid variations; model-based graders are flexible and handle open-ended output but are non-deterministic and need calibration against humans; human graders are the gold standard but expensive and slow.
- Capability evals should start at a low pass rate and give a team a hill to climb; regression evals should sit near 100% and catch backsliding, and capability tasks with high pass rates can "graduate" into the regression suite.
- For coding agents, deterministic tests are natural — does the code run and do the tests pass — as in [[Dataset/swe-bench-verified]] and [[Dataset/terminal-bench]]; grading the transcript as well can assess code quality and how the agent uses tools.
- Conversational agents often need a second LLM to simulate the user, and success can be multidimensional (state resolved, turn limit, tone), as in [[Dataset/tau-bench]] and its successor.
- Research-agent quality can only be judged relative to the task, so the post suggests combining groundedness, coverage and source-quality checks, with LLM rubrics frequently calibrated against expert judgment.
- Non-determinism is handled with two metrics that answer different questions: [[DefinedTerm/pass-at-k]], the chance of at least one success in k trials, and [[DefinedTerm/pass-hat-k]], the chance that all k trials succeed.
- The post recommends starting early with 20–50 simple tasks drawn from real failures, since early changes have large effects that small samples can detect.
- A good task is one on which two domain experts would independently reach the same pass/fail verdict, and a reference solution proves each task is solvable; with frontier models, a 0% pass rate over many trials most often signals a broken task.
- Problem sets should be balanced, testing both when a behavior should and should not occur, to avoid one-sided optimization.
- Each trial should start from a clean, isolated environment; the post reports Claude gaining an unfair advantage on some internal evals by examining git history left from previous trials.
- It recommends grading what the agent produced rather than the exact path it took, building in partial credit, grading each rubric dimension with a separate LLM judge, and giving an [[DefinedTerm/llm-as-a-judge]] a way out such as answering "Unknown".
- Scores should not be taken at face value until someone reads the transcripts; grading bugs, ambiguous specs and harness constraints can make a capable agent score low.
- An eval at 100% gives no signal for improvement; near saturation, large capability gains can show up as small score increases.
- The post recommends eval-driven development — building evals for planned capabilities before agents can meet them — and letting people close to product requirements contribute eval tasks.
- Automated evals are one layer among production monitoring, A/B testing, user feedback, manual transcript review and systematic human studies; the post likens the combination to the Swiss cheese model, in which failures that slip through one layer are caught by another.

## Context

The post presents its advice as field-tested practice from Anthropic's own teams and the customers it has worked with, and illustrates it with Anthropic's experience evaluating Claude Code and web search in Claude.ai, alongside brief accounts of other companies' eval programmes. Its YAML task definitions are explicitly labelled as theoretical illustrations. It closes by calling agent evaluation a nascent, fast-evolving field whose techniques will need to adapt as agents take on longer, multi-agent and more subjective work, and adds an appendix naming open-source and commercial eval frameworks while cautioning that a framework is only as good as the tasks run through it. It sits alongside this wiki's other material on [[DefinedTerm/trajectory-evaluation]] and [[DefinedTerm/agent-harness]] design.
