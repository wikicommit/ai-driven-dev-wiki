---
title: "MCPToolBench++"
type: "schema:Dataset"
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
  description: "A benchmark of about 1.5K queries with ground-truth tool-call labels for evaluating how well LLMs and AI agents use Model Context Protocol (MCP) tools, covering single-step and multi-step calls across six domains, with multilingual queries."
  creator: ["Shiqing Fan", "Xichen Ding", "Liang Zhang", "Linjian Mo"]
  url: "https://github.com/mcp-tool-bench/MCPToolBenchPP"
---

MCPToolBench++ is a benchmark for evaluating how large language models and AI agents call tools exposed through the [[DefinedTerm/model-context-protocol]] (MCP). It pairs natural-language queries with ground-truth tool-call labels, mixing single-step queries with multi-step ones that need a chain of tool calls, and includes multilingual queries such as route finding with maps worldwide and questions about global financial markets. It was introduced in [[ScholarlyArticle/mcptoolbench-plus-plus]] by researchers at Ant Group.

## Contents

Each record is a query together with the tool calls expected to fulfil it, in JSON form; multi-step records specify the order of the calls and which calls depend on the results of earlier ones, and some chains use up to 10 tools for a single request. The paper reports 1,509 instances spread over six categories — Browser, File System, Search, Map, Finance and Pay — drawing on 87 MCP tools, with Map the largest category (500 instances) and Finance the smallest (90). The tool schemas average about 288 tokens per tool, and the paper describes the benchmark as built on a marketplace of over 4,000 MCP servers from more than 40 categories as of July 2025.

## Provenance

MCP servers were gathered from open MCP marketplaces, including smithery.ai, deepnlp.org, pulsemcp.com and modelscope.cn, and their configuration files, server metadata and tool schemas were collected and indexed locally. A tool sampler then drew single tools (with replacement) and multi-step chains of 2 to 10 tools (without replacement), within one category or across LLM-generated combinations of categories such as finance and plotting. An LLM-driven query generator produced query templates, generated parameter values — using code dictionaries for inputs such as stock ticker symbols and geocodes — filled the templates, and rewrote the results into natural queries. Post-processing removed queries that failed a semantic check (for example, coordinates the rewrite could not turn into a place name) or a reasonableness check (for example, travelling from New York to Tokyo by train).

The authors state that every tool used was tested and offers free access or a sufficient free call quota from its provider, so that results can be reproduced. The benchmark is published on GitHub and as a Hugging Face dataset.

## Use

In [[ScholarlyArticle/mcptoolbench-plus-plus]] the authors evaluate GPT-4o, Qwen2.5-max, Claude-3.7-Sonnet, Kimi-K2-Instruct and Qwen3-coder on the benchmark, reporting that no single model led every category and that tool-selection accuracy and actual execution success do not always rank models the same way.
