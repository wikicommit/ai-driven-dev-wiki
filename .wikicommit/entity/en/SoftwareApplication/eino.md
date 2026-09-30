---
title: "Eino"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-framework, go, llm-application-development]
sources:
  - type: url
    url: 'https://tech.qimao.com/ai-dai-ma-ping-shen-zai-qi-mao-de-shi-jian/'
    hash: sha256:b3c89326b7176bb078a329222696a60fa6aeb732270c6818b325db21588ef5c1
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "ByteDance's Go framework for building LLM-centred applications and AI agents, which provides flow orchestration — composing typed processing steps into a chain that is compiled and checked before it runs — and aspect hooks for debugging each step."
  applicationCategory: "LLM application and AI agent development framework"
  featureList: "Flow orchestration of typed steps into a chain; compile-time checking of step inputs and outputs; per-run local state; aspect (cross-cutting) capabilities for debugging individual steps"
  author: "ByteDance"
---

Eino is a framework from ByteDance for developing LLM-centred applications and AI agents in Go, published in the `cloudwego/eino` repository on GitHub. Qimao's engineering team chose it over hand-rolling its own plumbing when building an AI code review service ([[BlogPosting/ai-code-review-practice-at-qimao]]), reasoning that AI agent development has settled into recurring patterns the framework already covers.

## Capabilities

The two capabilities that team singles out are flow orchestration and "aspect" capabilities. Orchestration is described as indispensable for an application whose core is an LLM, where development consists of continually adjusting the inputs and outputs of each step; aspect capabilities address the need to debug each stage of the business logic.

In orchestration, each step is wrapped with a defined input and output data structure and the steps are then combined. In the team's code, a chain is created with its input and output types and a generator for per-run local state, steps are appended to it in order as lambdas, and the chain is compiled — a step that validates the inputs and outputs — into a runnable. The team reports that this keeps the logic clearer and easier to maintain: as requirements change, fixed steps are supplied and only the orchestration is rearranged.

## Adoption & Ecosystem

In the Qimao service, Eino runs a one-directional chain of four steps — fetching merge-request data, grouping changed files, a first-pass review and a second-pass review — inside a Go service that reviews merge requests automatically.
