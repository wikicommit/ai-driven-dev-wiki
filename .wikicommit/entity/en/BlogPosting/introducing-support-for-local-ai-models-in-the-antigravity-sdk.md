---
title: "Introducing Support for Local AI Models in the Antigravity SDK"
type: "schema:BlogPosting"
lang: en
tags: [agents, local-models, multi-agent]
sources:
  - type: url
    url: 'https://developers.googleblog.com/introducing-support-for-local-ai-models-in-the-antigravity-sdk/'
    hash: sha256:29af3552e39410efe70d79dcfd4f566d9ee66624acce774cc7db217bcbc4ca24
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Google's announcement that the Antigravity SDK can run agents on local models, starting with Gemma 4 26B A4B on LiteRT, with a demonstration of a hybrid workflow in which a cloud model plans and local models do the work on-device."
  author: ["Sachin Kotwani", "Taylor Mullen"]
  datePublished: "2026-09-23"
  publisher: "[[Organization/google]]"
---

This post announces that the [[SoftwareApplication/antigravity-sdk]] — which it describes as letting developers build with the same agentic capabilities that power [[SoftwareApplication/google-antigravity]] — supports local workflows across a range of local models and execution options. Initial support is for Gemma 4 26B A4B running on Google AI Edge's LiteRT. The post says the new support lets agentic assistance run on local models completely offline, and separately that the workflow was optimized for LiteRT and Gemma 4 26B to use the local GPU and RAM efficiently, to get more out of what the local machine can deliver.

Most of the post is demonstration. After a short setup — installing the SDK and LiteRT-LM, importing the model, and running an agent configured with `LiteRTAgentConfig` — it shows two examples: a hybrid pipeline in which a cloud model plans and a swarm of local models carries out a security-patching task, and a local agent building a terminal resource-monitoring utility from a single prompt.

## Key Points

- Four reasons are given for running agents locally: no API costs or rate limits; privacy, with code and requests kept on the local machine, which the post singles out for compliance-restricted corporate environments; offline resiliency where connectivity is unreliable; and hybrid workflows that mix token-efficient local processes with larger cloud models when needed.
- The recommended hardware is a machine with more than 24GB of VRAM or unified memory.
- The post describes an Architect-Builder pattern as a good way of combining cloud model scale with the advantages of local models. In its demo, Gemini 3.8 Flash in the cloud acts as planner and conductor while local Gemma 4 26B instances do the heavy lifting.
- In that demo the cloud model decomposes an audit-and-patch task over three vulnerable modules using only filenames and task descriptions, so no source code leaves the machine; the local models then run what the post calls an adversarial audit loop — reproducing the vulnerabilities, writing candidate fixes, critiquing the patches and validating them against regression test suites.
- For that recorded run the post reports that the cloud model spent 95 tokens and that 97.2% of all tokens (3,322) ran locally, producing verified patches that passed their tests. These are figures from one run of Google's own demo.
- In the second example, the agent writes a Python terminal dashboard using the psutil and rich libraries, generates its `requirements.txt` and tests the result, entirely on the local machine.
- Besides LiteRT, the SDK supports any OpenAI-compatible server — Ollama, LM Studio and vLLM are named — through `LocalOpenAIAgentConfig`, which the post says lets developers swap local inference backends without changing agent orchestration, tools or workflows.

## Context

This is the vendor's own announcement, and its performance statements come from its own demonstrations rather than from an evaluation. The hybrid demo is a concrete instance of splitting planning and execution between models of different sizes and locations — the planner sees task descriptions and filenames, the executors see the code — a division the post argues serves privacy and cost at once.
