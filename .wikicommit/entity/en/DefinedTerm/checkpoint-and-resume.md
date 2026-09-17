---
title: "Checkpoint-and-Resume"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A design pattern for long-running AI agents that treats the agent like a long-running server process: it writes intermediate state to disk and checkpoints every N units of work, so a failure partway through a multi-hour job can recover from the last checkpoint instead of restarting from scratch."
---

Checkpoint-and-resume is one of five patterns for long-running AI agents named by Shubham Saboo and Addy Osmani as separating working long-running agents from demos: it treats the agent like a long-running server process, writing intermediate state to disk and checkpointing at regular intervals, so a failure partway through a long job recovers from the last checkpoint rather than starting over.

## Usage

It is illustrated with an agent processing 200 documents over four hours that hits an error on document 201: without a checkpoint, that failure means starting from scratch. It is presented alongside four sibling patterns from the same write-up: delegated approval (see [[DefinedTerm/human-in-the-loop]]), memory-layered context, ambient processing, and fleet orchestration, which are described as composable -- a single system might use checkpointing for document processing and fleet orchestration to coordinate specialist agents at the same time.

## When It Applies

It applies to any multi-hour or multi-day agent run where the most common failure mode is losing accumulated context to a crash or an error partway through. It assumes a persistent filesystem the agent can write to -- Google's Agent Runtime sandbox is named as one example that provides this -- but choosing the right checkpoint granularity is left as a judgment call: not on every step, and not only at the very end.

## Related Terms

[[DefinedTerm/long-running-agent]], [[DefinedTerm/human-in-the-loop]], [[SoftwareApplication/gemini-enterprise-agent-platform]]
