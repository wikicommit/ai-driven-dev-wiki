---
title: "τ-bench"
type: "schema:Dataset"
lang: en
aliases: ["tau-bench"]
tags: [agent-evaluation, benchmarks, tool-use]
sources:
  - type: url
    url: 'https://github.com/sierra-research/tau-bench'
    hash: sha256:3821f8efe04242eb2fa276ba2645bcc2430d7efa92ab2f006b6a3da1ff37aed3
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A benchmark for tool-agent-user interaction that emulates dynamic conversations between a language-model-simulated user and a language agent equipped with domain-specific API tools and policy guidelines, originally in airline and retail domains."
  creator: ["Shunyu Yao", "Noah Shinn", "Pedram Razavi", "Karthik Narasimhan"]
  url: "https://github.com/sierra-research/tau-bench"
---

τ-bench ("tau-bench") is a benchmark for tool-agent-user interaction in real-world domains. It emulates
dynamic conversations between a user, simulated by a language model, and a language agent that is
given domain-specific API tools and policy guidelines. Its
repository, under the sierra-research GitHub organization and MIT-licensed, holds the code and data for the
benchmark introduced in a 2024 paper (arXiv 2406.12045).

## Contents

The original repository contains two environments, airline and retail, each with its own tasks, and a
leaderboard that scores agent strategies — function-calling ("tool-calling"), Act and ReAct — with a
pass^k metric reported for k from 1 to 4. The repository now carries a warning that these airline and
retail tasks are outdated versions: its successor, τ²-bench, has been updated to τ³-bench, which fixes
the airline and retail tasks and adds a banking domain and a voice evaluation modality, and users are
directed there for the latest version.

## Provenance

The benchmark is run from source against model providers' APIs. The simulated user defaults to
GPT-4o with an `llm` strategy, and alternative user-simulator strategies are provided: `react`, which
has the simulated user write a thought before its response; `verify`, which adds an LLM verification
step and regenerates an unsatisfactory user response; and `reflection`, which has the simulator
reflect on an unsatisfactory response before generating a new one. Because runs can be expensive, the
repository also ships historical trajectories for both environments and invites contributions of more.

## Use

For analysing failed runs, the repository provides an LLM-based auto error identification tool that
assigns fault for a failure to the user, the agent or the environment, and classifies the fault as a
partially completed goal, a wrong tool, a wrong tool argument, or an unintended action; both labels
come with a description. The repository cautions that because this tool relies on an LLM, its identifications may
be inaccurate.
