---
title: "MCP-Bench"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, tool-use, mcp]
sources:
  - type: url
    url: 'https://github.com/Accenture/mcp-bench'
    hash: sha256:9edf96577002e279a51e4ba8dcce90b35e383f11bb327aeccb2c75917fb53716
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "A benchmark and evaluation framework for tool-using LLM agents that runs real-world tasks against 28 live Model Context Protocol (MCP) servers, in single-server and multi-server settings, and scores how well models discover, select and use the tools."
  creator: ["Zhenting Wang", "Qi Chang", "Hemani Patel", "Shashank Biju", "Cheng-En Wu", "Quan Liu", "Aolin Ding", "Alireza Rezazadeh", "Ankit Shah", "Yujia Bao", "Eugene Siow"]
  url: "https://github.com/Accenture/mcp-bench"
---

MCP-Bench is a benchmark for assessing how large language models perform in tool-use scenarios through the [[DefinedTerm/model-context-protocol]] (MCP). It provides an end-to-end pipeline for evaluating how effectively different LLMs can discover, select and use tools to solve real-world tasks, by connecting the agent under test to a fixed set of real MCP servers. It is published in a repository under the Accenture GitHub organization, is described in an accompanying arXiv preprint, and was accepted to the NeurIPS 2025 Workshop on Scaling Environments for Agents.

## Contents

The benchmark consists of task files and the MCP servers those tasks run against. Tasks are split into three sets: tasks that use a single server, tasks that combine two servers, and tasks that combine three, with the server combinations for the multi-server sets defined in separate split files.

The 28 MCP servers are existing open-source servers covering a wide spread of domains — biomedical research and clinical trials, medical calculators, cryptocurrency and decentralized-exchange data, maps and geocoding, academic paper search and calls for papers, NASA and US National Parks data, museum collections, Hugging Face models and datasets, NixOS packages, OpenAPI specification exploration, OSINT, Reddit, Wikipedia, weather, time zones, unit conversion, mathematics and scientific computing, among others.

## Provenance

Tasks are produced by the repository's own synthesis module, which generates tasks for single servers and for the two- and three-server combinations and applies what the repository calls fuzzy conversion during task generation. The servers themselves are third-party projects bundled with an installation script; several need API keys from outside providers (for example NASA, the National Park Service, Google Maps, Hugging Face and the National Cancer Institute), which the repository describes as free to obtain.

The code and tasks are released under the Apache 2.0 license on GitHub, and a leaderboard is hosted as a Hugging Face Space.

## Use

The repository ships the harness used to run the benchmark: a multi-round task executor with retry logic, a server manager that connects to and orchestrates the MCP servers, and an evaluator that uses [[DefinedTerm/llm-as-a-judge]] metrics. A model's overall score averages rule-based checks of schema understanding with LLM-judged task completion, tool usage and planning effectiveness, and is averaged across the single-server and multi-server settings; o4-mini is the judge model, and the repository states that it must be used to reproduce the published results. Models are reached through OpenRouter or Azure OpenAI, and further OpenRouter models can be added to the model factory.

The repository's leaderboard reports 20 models scored this way, with gpt-5 at the top (0.749 overall), followed by o3 and gpt-oss-120b, and llama-3-1-8b-instruct lowest (0.428).
