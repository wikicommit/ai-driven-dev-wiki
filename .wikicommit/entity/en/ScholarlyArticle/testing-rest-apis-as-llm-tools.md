---
title: "A Framework for Testing and Adapting REST APIs as LLM Tools"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2504.15546'
    hash: sha256:39549788a2452ec0fb8ea5da808b3e0e1e78cd4676d00b50ff2c06f8b85de2cd
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A framework from IBM Research that adapts established API testing techniques to evaluate whether enterprise REST APIs are usable as tools by LLM-based agents, generating data-aware test cases, translating them into natural-language utterances, and comparing direct tool execution against agent-driven execution to build a taxonomy of tool-use errors."
  author: ["Jayachandu Bandlamudi", "Ritwik Chaudhuri", "Neelamadhav Gantayat", "Sambit Ghosh", "Kushal Mukherjee", "Prerna Agarwal", "Renuka Sindhgatta", "Sameep Mehta"]
  keywords: ["REST APIs", "LLM tools", "agentic testing", "tool robustness", "enterprise APIs"]
---

The paper argues that REST APIs exposing enterprise software functionality are typically not designed with LLM agents in mind, and that existing tool-use benchmarks such as the Berkeley Function Calling Leaderboard, τ-bench, and ToolACE evaluate tool selection and argument correctness but not whether a given API is actually usable — "agent-ready" — as a tool in the first place. The authors present a framework that wraps an API's OpenAPI specification as a Python (LangChain) tool, generates test cases with an LLM, converts them into natural-language utterances of the kind an agent would receive, and executes those utterances inside a [[DefinedTerm/react-prompting]] agent to check whether the agent can invoke the tool correctly and interpret its response.

The method combines several stages: Tool Creation from an OpenAPI specification; LLM-based test-case generation across mandatory-only, all-parameters, and mandatory-plus-optional-subset scenarios; [[DefinedTerm/data-aware-testing]], which grounds generated inputs in real inter-tool data dependencies; natural-language utterance generation, tried both with a prompted LLM and with a LoRA-fine-tuned small model; and test execution, which compares direct Python tool calls (treated as ground truth) against the same test cases driven through an agent via their natural-language utterances.

The framework is deployed as part of the alpha release of [[SoftwareApplication/watsonx-orchestrate-agent-development-kit]], IBM's tool-builder-focused product. By the time of writing, tool builders using it had wrapped more than 600 APIs as tools spanning IT, human resources, finance, procurement, and sales, and the paper reports that this automation, combined with the framework's actionable recommendations, reduced tool build effort by about 30% (roughly two days per tool) relative to the prior manual process, for a reported total of over 1,200 person-days saved to date.

## Key Points

- The framework generated over 2,400 natural-language test cases across 189 enterprise tools spanning six applications (DnB, Salesloft, ServiceNow, Jira, Kubernetes, Salesforce), retained 2,411 of them as accurate and high-naturalness, and executed them with two agent LLMs (Granite-3.3-8B-Instruct and Llama-3.3-70B-Instruct) via a ReAct agent built on LangGraph.
- The paper's error taxonomy groups tool-use failures into four categories: Input Specification Errors (parameter mismatch, parameter type mismatch, parameter value mismatch), Output Processing Errors (output mismatch, empty output, malformed output, tool output exceeding the LLM's token limit), Tool Invocation Errors (tool not identified, incorrect tool selection, repeated tool invocation), and Tool Execution Errors (access errors, server errors).
- Across the two agent LLMs, roughly 26-30% of test cases executed with no error; parameter type and value mismatches were the most common failure, and the paper attributes 13-19% of test cases' errors specifically to issues generating correct input payloads (parameter types and values).
- Restricting to 705 test cases for which a tool dependency graph was approved by a human tool builder, using data-aware test inputs instead of LLM-invented ones reduced empty-output and output-mismatch error rates by around 10 percentage points each and increased the fraction of test cases executing without any error, compared with the same test cases generated without data-aware inputs.
- An LLM-as-a-judge evaluation of the generated natural-language utterances — validated against human judgment on 15% of the test set, at 89% agreement for accuracy and 93% for naturalness — found 96.4% of utterances accurate (only 1.7% inaccurate) and 87.4% both accurate and scoring above 3 out of 5 on naturalness.
- Analysis of per-tool test-case pass rates found 34% of tools in the 0-25% pass-rate range needing substantial iteration, 30% in the 25-75% range needing moderate iteration, and 36% already at a 75-100% pass rate.

## Notes

The framework builds on prior stand-alone REST API testing tools (RESTler, EvoMaster, RESTest, RestTestGen) and prior LLM tool-use benchmarks and evaluation frameworks (the paper cites the Berkeley Function Calling Leaderboard, τ-bench, ToolACE, T-Eval, EasyTool, Gorilla, and ToolQA), positioning its own contribution as evaluating an API's "agent-readiness" specifically — whether an agent can actually invoke it and use its response — rather than tool-selection accuracy alone. The paper states plans to extend the work to multi-turn utterances that simulate a conversation leading to tool invocation, and to explore an error taxonomy for sequential, multi-step tool calls.
