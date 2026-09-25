---
title: "DeepSWE: Training a Fully Open-sourced, State-of-the-Art Coding Agent by Scaling RL"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, reinforcement-learning, open-source, benchmarking]
sources:
  - type: url
    url: 'https://www.together.ai/blog/deepswe'
    hash: sha256:607b29ec1a7476539260e91be9f97e5f5af2d90dea329b16e167e07f9a9f32f0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A research blog post from the Agentica team and Together AI introducing DeepSWE-Preview, a reasoning-enabled coding agent trained from Qwen3-32B with reinforcement learning only, and releasing its dataset, training code and evaluation logs."
  author: ["Michael Luo", "Naman Jain", "Jaskirat Singh", "Sijun Tan", "Ameen Patel", "Qingyang Wu", "Alpay Ariyak", "Colin Cai", "Tarun Venkat", "Shang Zhu", "Ben Athiwaratkun", "Manan Roongta", "Ce Zhang", "Li Erran Li", "Raluca Ada Popa", "Koushik Sen", "Ion Stoica"]
  datePublished: "2025-07-02"
  publisher: "Together AI"
---

This post, published on the Together AI research blog and presented as a joint collaboration between
the Agentica team and Together AI, introduces DeepSWE-Preview: a reasoning-enabled coding agent trained
on top of the Qwen3-32B model using only reinforcement learning (RL). Its framing is that scaling RL-based reasoning models
to long-horizon, multi-step agentic tasks is still an open problem, and it treats autonomous software
engineering — resolving GitHub issues, implementing features, debugging — as a prominent example of such
a task.

The agent was trained with [[SoftwareApplication/rllm]], Agentica's framework for post-training language
agents, and the authors state that they open-sourced the dataset, code, training and evaluation logs.
Evaluation is on [[Dataset/swe-bench-verified]].

## Key Claims

- Software-engineering tasks are cast as RL environments: an agent works in a terminal and a filesystem
  holding the codebase, using bash execution, search, a file viewer/editor and a finish tool, and receives
  a reward of 1 only when its patch passes a selected sample of the project's tests within a time limit,
  and 0 otherwise (a sparse outcome reward).
- Training used 4,500 real-world tasks from a subset of the R2E-Gym environments, filtered to exclude
  repositories that also appear in SWE-Bench-Verified to avoid contamination, and ran for six days on 64
  H100 GPUs.
- Scaling the rollouts required moving container orchestration to Kubernetes: each RL iteration spawned
  512 Docker containers in parallel, which, together with parallel experiments, overloaded the Docker
  daemon until containers were scheduled across an autoscaled node pool instead.
- The training algorithm, called GRPO++, combines several published modifications to GRPO (a higher clip
  bound and no KL loss from DAPO, no reward standard deviation and length normalization from Dr. GRPO,
  leave-one-out advantage estimation) with two of the authors' own: [[DefinedTerm/compact-filtering]] and
  dropping the entropy loss, which they report destabilized training.
- The authors report 42.2% Pass@1 (averaged over 16 runs) and 71.0% Pass@16 on SWE-Bench-Verified, and
  59% when combining an execution-based and an execution-free verifier to pick among 16 candidate
  trajectories ("hybrid" test-time scaling), which they describe as state of the art for open-weight
  coding agents at the time.
- Scaling test-time compute by output length helped little for these tasks — gains beyond a 32K-token
  context were reported as marginal (at most 2%) — whereas scaling the number of rollouts did help, with
  most of the gain reached at 8 rollouts.
- Behaviours the authors describe as emerging from pure RL with 0/1 rewards include thinking through edge
  cases and searching for and running the repository's existing regression tests before submitting, and
  spending many thinking tokens on hard steps such as localizing a bug while spending very few on simple
  steps such as scrolling through a file.
- Several approaches are reported as not working well in their experiments: starting RL from models
  fine-tuned on Claude Sonnet 3.7/4 trajectories, training on the SWE-Smith and SWE-Gym datasets instead
  of R2E-Gym, and RL on Qwen3-32B's non-thinking mode.

## Context

The post positions DeepSWE-Preview as following the same team's earlier reasoning models for math and
coding, DeepScaleR and DeepCoder, and as a first step toward showing that RL-driven reasoning can scale
long-horizon multi-step agents given high-quality execution environments. All benchmark figures above
are the authors' own reported results. Stated future directions include training a further model on top
of DeepSWE-Preview, training larger models with longer context, and extending to other agentic domains
such as web agents.
