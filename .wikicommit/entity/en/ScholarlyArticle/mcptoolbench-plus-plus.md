---
title: "MCPToolBench++: A Large Scale AI Agent Model Context Protocol MCP Tool Use Benchmark"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, tool-use, mcp]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.07575'
    hash: sha256:af67d07e38570ae6c1b05cf80e4c3fc5afec9d2c36bc7513479c90b19edba81f
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper from Ant Group introducing MCPToolBench++, a large-scale, multi-domain, multilingual benchmark for evaluating how well LLMs and AI agents call Model Context Protocol (MCP) tools, and reporting results for five models."
  author: ["Shiqing Fan", "Xichen Ding", "Liang Zhang", "Linjian Mo"]
  datePublished: "2025"
  keywords: ["[[DefinedTerm/model-context-protocol]]", "tool use", "function calling", "benchmark"]
---

A paper by Shiqing Fan, Xichen Ding, Liang Zhang and Linjian Mo of Ant Group that introduces the [[Dataset/mcptoolbench-plus-plus]] benchmark for evaluating how LLMs and AI agents use tools exposed through the [[DefinedTerm/model-context-protocol]] (MCP). The authors argue that evaluating MCP tool use is hard for four reasons: there is no comprehensive benchmark covering the highly diverse MCP tools and schemas; MCP tool calls return diverse response formats; unlike programming or math functions in existing tool-use benchmarks, real-world MCP tools do not reliably succeed and their success rate varies across servers; and a model's context window limits how many tools can be offered in a single run, because tool and parameter descriptions are long.

The benchmark is built with an automatic pipeline over MCP configurations and tool schemas collected from open MCP marketplaces — as of July 2025, a marketplace of over 4,000 MCP servers in more than 40 categories. A tool sampler draws single tools and chains of up to 10 tools, a query generator turns them into natural-language queries with ground-truth tool-call labels, and post-processing filters out queries that fail semantic or reasonableness checks. The resulting benchmark has about 1.5K question–answer pairs over six domains and includes multilingual queries.

The authors evaluate GPT-4o, Qwen2.5-max, Claude-3.7-Sonnet, Kimi-K2-Instruct and Qwen3-coder, and pair the accuracy results with a root-cause analysis of why MCP tool calls fail.

## Key Points

- The paper evaluates tool calls on two levels: an Abstract Syntax Tree (AST) score for choosing the right tool and filling its parameters, following the [[Dataset/berkeley-function-calling-leaderboard]], and Pass@K, which additionally requires the tool call to actually run and return results that match the expected ground truth. For multi-step calls it proposes an "AST DAG Accuracy" metric that compares the predicted and ground-truth execution plans as directed acyclic graphs.
- A separate Tool Call Success Rate measures, per MCP tool, the share of runs that execute without error; an LLM is used as a judge to decide whether a response that returns a success status code actually succeeded. Each tool call was run 5 times to estimate Pass@K.
- No single model led every category. On AST, Qwen3-coder led Browser and Map, Qwen2.5-max led File System and Finance, and Kimi-K2-Instruct led Search and Pay. On Pass@1, Qwen3-coder led Browser, Qwen2.5-max led File System, Claude-3.7-Sonnet led Search, GPT-4o led Map and Finance, and Kimi-K2-Instruct led Pay.
- AST and Pass@K rankings do not always agree. In Search, Claude-3.7-Sonnet scored slightly below Kimi-K2-Instruct on AST (0.728 versus 0.732) but well above it on Pass@1 (0.620 versus 0.368); the authors attribute this to the Google Custom Search tool having a higher success rate than other search providers such as Tavily and to Claude-3.7-Sonnet choosing it more often. When several tools offer similar features, a model can match the ground-truth label yet end up with a very different final result.
- The authors identify the real-world success rate of MCP tools as a key variable in the overall Pass@1 score, especially for tools that call external APIs.
- The top-ranked root causes of failed MCP tool calls were parameter errors, API errors, empty results, and session and runtime errors, with domain-specific failures such as out-of-range latitude/longitude values in map tools and screenshots saved to non-existent paths in browser tools.
- The paper analyses the token cost of offering tools to a model as growing with the number of installed servers, the average number of tools per server and the length of each tool's schema, and argues for a "Tool Dispatcher" that retrieves only the tools relevant to a query — reducing the tools passed to the model from around 100 to around 10.

## Notes

The authors state that they checked every tool used in the benchmark and verified that it offers free access or a sufficient free call quota, so that the results can be reproduced. They also note that different models take different paths to the same task — for route planning, some call a single tool with addresses while others first convert addresses to geocodes or coordinates. In the AST DAG Accuracy metric, a match is scored on the last execution nodes of each task in the predicted and ground-truth plans.
