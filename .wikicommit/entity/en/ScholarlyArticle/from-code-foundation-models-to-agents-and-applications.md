---
title: "From Code Foundation Models to Agents and Applications: A Comprehensive Survey and Practical Guide to Code Intelligence"
type: "schema:ScholarlyArticle"
lang: en
tags: [survey, code-llms, coding-agents, benchmarks, reinforcement-learning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2511.18538'
    hash: sha256:5de6418c3ebb599f746fb892165c9eec893f778014fe7927fc64a352d1304d90
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A large multi-institution survey and practical guide that follows code LLMs across their lifecycle — from foundation models and pre-training data through benchmarks, alignment and reinforcement learning, to software engineering agents, safety and deployed applications — and adds the authors' own experiments on pre-training scaling, fine-tuning and reinforcement learning for code."
---

This survey, by a large collaboration whose first and corresponding authors are at Beihang University
and whose contributors come from many universities and companies, sets out to
synthesize research on large language models for code across the whole model lifecycle and to act as a
practical guide. Its abstract frames the motivation as the commercial adoption of tools such as
[[SoftwareApplication/github-copilot]], [[SoftwareApplication/cursor]], [[SoftwareApplication/trae]]
and [[SoftwareApplication/claude-code]], and the rise from single-digit to over 95% success rates on
benchmarks like HumanEval. The authors argue that existing surveys are either panoramic or focused on
earlier model generations, and that the research–practice gap — code correctness, security, awareness
of large codebases and integration with development workflows — deserves systematic treatment.

The survey is organized in nine parts: code foundation models (general and code-specialized LLMs, their
architectures, pre-training tasks and open pre-training datasets); code tasks, benchmarks and evaluation
metrics at statement, function, class and repository level and for agentic systems; alignment through
supervised fine-tuning, reasoning data construction, multilingual and multimodal code, and
reinforcement learning including reinforcement learning with verifiable rewards; software engineering
agents organized by lifecycle phase (requirements, development, testing, maintenance and end-to-end);
code for generalist agents (code as interaction protocol, as agentic capability and as environment
interface); the safety of code LLMs; training recipes; and applications. It opens with a six-stage
account of how programming has evolved, from manual and tool-assisted coding through framework-based and
AI-assisted development to AI-driven and, as a possible future, AI-autonomous coding.

## Key Points

- The survey organizes software engineering agents by the phases of a waterfall-style lifecycle —
  requirements engineering, software development, testing, and maintenance — and describes a layered
  architecture for issue-resolving agents that runs from an agent–computer interface layer (as in
  [[SoftwareApplication/swe-agent]] and [[SoftwareApplication/openhands]]) through architecture,
  knowledge and semantic layers to a self-evolving intelligence layer.
- It treats code as the medium for generalist agents along three dimensions: interaction protocols
  (tool use, the [[DefinedTerm/model-context-protocol]] and agent-to-agent coordination), agentic
  capabilities (thinking, acting and memory in code, as in [[DefinedTerm/codeact]]), and environment
  interfaces (simulation gyms and computer-use agents).
- On evaluation, it traces a shift from string-matching metrics such as CodeBLEU to execution-based
  metrics such as [[DefinedTerm/pass-at-k]] and on to [[DefinedTerm/llm-as-a-judge]] approaches, and
  catalogs repository-level and agentic benchmarks including [[Dataset/swe-bench]] and its variants and
  [[Dataset/terminal-bench]].
- In the authors' pre-training experiments across seven programming languages, interpreted languages
  such as Python show larger scaling exponents than compiled languages such as Rust and Go, and
  multilingual pre-training mostly helps — syntactically similar pairs such as Java and C# reinforce
  each other — with Python as a target language as the main exception.
- In their supervised fine-tuning experiments, global batch size is the dominant sensitivity factor
  (accuracy degrades once it exceeds roughly 256), the dense Qwen2.5-Coder-14B is more robust to
  hyperparameter changes than the mixture-of-experts Qwen3-30B-A3B, and datasets with executable or
  test-based supervision transfer best under a fixed data budget.
- In their reinforcement-learning experiments on code with a verifiable reward, the best choices depend
  on the target metric: RLOO gave the best pass@1 and pass@5 among advantage estimators while
  REINFORCE++ with a baseline converged faster and was adopted as the default; 16K-token responses gave
  the best pass@1 and 2K tokens the best pass@5; and 16 rollouts per prompt is recommended as a default.
- On safety, the authors describe code LLMs as insecure by default because they learn from public code
  in which flawed patterns are common, and organize mitigation into safety pre-training, safety
  post-training, red-teaming, and a defense-in-depth approach for coding agents built on secure
  execution environments, pre-execution validation and runtime oversight.

## Notes

The authors' reinforcement-learning experiments were run with the VERL framework on the
codecontest_plus dataset and evaluated on the lcb-v6 benchmark; the authors state that they plan to
compare results across further training frameworks, because infrastructure differences may change
stability and outcomes.
