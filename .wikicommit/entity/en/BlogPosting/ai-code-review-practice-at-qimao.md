---
title: "AI 代码评审在七猫的实践"
type: "schema:BlogPosting"
lang: en
tags: [code-review, ai-code-review, prompt-design]
sources:
  - type: url
    url: 'https://tech.qimao.com/ai-dai-ma-ping-shen-zai-qi-mao-de-shi-jian/'
    hash: sha256:b3c89326b7176bb078a329222696a60fa6aeb732270c6818b325db21588ef5c1
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An August 2025 post on Qimao's technology blog describing an in-house AI code review service that reviews every merge request automatically and posts inline comments, built in Go on ByteDance's Eino framework, with lessons on input design and model choice."
  author: ["七猫技术 (Qimao Tech)"]
  datePublished: "2025-08-27"
  publisher: "七猫技术团队 (Qimao Technology Team)"
---

The post ("AI code review in practice at Qimao") describes how Qimao's engineering team built an AI code review service for its own merge requests. It states two goals: to assist code review with AI's ability to analyze code, offering a different perspective for finding potential problems, and to gain hands-on experience of engineering AI applications as groundwork for AIOps. Before the service existed, problem code was commented on by hand in the Yunxiao (云效) platform; the chosen design needs no extra configuration from users — opening a merge request triggers the review automatically, and results come back as inline comments through the Yunxiao API.

Much of the post is about what the author learned while tuning the service: that the review's "core logic" now consists of prompts rather than code, that giving the model less input produced better reviews, and that line numbers should not be taken from the model's output.

## Key Points

- Technology choices: full code rather than a low-code platform, for controllability, stability and extensibility in a long-maintained project; Go rather than Python, because Go is the company's main backend language and a tool for internal efficiency did not need Python's stronger AI ecosystem; and ByteDance's [[SoftwareApplication/eino]] framework rather than a hand-rolled one, because agent development follows recurring patterns — flow orchestration and cross-cutting "aspect" hooks for debugging each step — that the framework already provides.
- The review runs as a one-directional chain: pre-filtering by code group or repository; an A/B-testing stage, built in from the start because different models and prompts change the output greatly; fetching the incremental diff, commits and changed files; grouping the files by logical relationship, functional relatedness and dependencies; a first-pass review that classifies each issue as `high`, `medium` or `info`; a second-pass review that scores the first pass's findings; and an output filter that keeps the highest-scoring comments, five by default (configurable).
- The diff data is restructured before it reaches the model. After about a day and a half of prompt tuning that did not reach the expected quality, the author redesigned the input from the data structure up; the final first-pass input gives, per file, an id, the path, the full file content and the changed line ranges — described as "a lot of subtraction".
- The model lacks precise calculation: even with each diff line's number computed and supplied, its comments showed widespread "line-number drift". A line-number calculation tool the model could call was tested but consumed too many tokens, so the service stopped using line numbers from the model's output.
- More input is not better: when the diff, per-line numbering and the corresponding files were all supplied, many of the model's answers took code out of context and did not seem to understand the code itself.
- Prompt optimization is described as possibly the largest share of time in AI application development, and the post recommends Volcengine's PromptPilot tool for it.
- Models are chosen on quality, latency and cost, billed through Alibaba's Bailian (百炼) platform, for a typical input of about 100k tokens and output of about 3k: `qwen-long` for file grouping, because it supports million-token contexts for the extreme case of a new project, and `qwen-plus` for code analysis.
- The service is observed like a microservice — token consumption and API response time per call — using a Langfuse deployment provided by the operations team.
- Planned next steps: review preferences users can state in natural language (for example, only `high` issues, at most three, with particular scrutiny of concurrency in payment code), team-specific business knowledge brought in through RAG, and a feedback mechanism that combines user feedback with LLM analysis.

## Context

The post is a single team's account of an internal tool, and its tuning results come from simulating one real development iteration with more than 2,000 changed lines rather than from a measured comparison. It ends on a broader claim about AI applications: that large language models let a business mine and process semi-structured and unstructured data that traditional programming handled poorly. For the general notion of a bot that posts review feedback on pull requests, see [[DefinedTerm/code-review-agent]].
