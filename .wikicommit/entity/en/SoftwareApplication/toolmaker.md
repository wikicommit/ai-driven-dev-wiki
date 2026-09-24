---
title: "ToolMaker"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, tool-use, agent-tooling]
sources:
  - type: url
    url: 'https://aclanthology.org/2025.acl-long.1266.pdf'
    hash: sha256:e540f7778ba7b71c57f3614b2a333278db9a340b0b059328649725e9e89f3eab
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An agentic framework that autonomously converts a scientific paper's public code repository into an LLM-compatible tool: it installs the repository and its dependencies in a Docker container and writes a Python function that performs a user-defined task, fixing it through closed-loop self-correction."
  applicationCategory: "Agentic tool-creation framework"
---

ToolMaker is an agentic framework, introduced in [[ScholarlyArticle/llm-agents-making-agent-tools]], that turns stand-alone code repositories accompanying scientific publications into tools that an LLM agent can call. Its aim is to remove the human intermediary who would otherwise have to set up, install and adapt such code before an agent could use it — a barrier its authors see as especially limiting in healthcare, biology and drug development.

A user supplies a minimal tool definition: a one-sentence description of the task, the URL of the associated GitHub repository, and the required input arguments, each with an example value. ToolMaker returns two artifacts: an environment in which the tool runs (a Docker container) and a Python function that performs the task. The framework's code, together with its evaluation benchmark [[Dataset/tm-bench]], is public in the KatherLab/ToolMaker repository on GitHub.

## Capabilities

ToolMaker is built from three kinds of component: LLM calls, which only add a message to the conversation; environment interactions, which read or change the state of the execution environment; and agents, which chain the two to complete a sub-task given as a high-level instruction. Its environment actions are running bash commands, listing directories, reading and writing files, browsing, listing a Google Drive folder, downloading a Google Drive file, and a special action that executes a candidate tool implementation. Its agents may use every action except that last one: running a candidate implementation is reserved for a separate step of the workflow itself.

Work proceeds in two stages. In environment setup, an installing agent starts from a clean python:3.12 Docker image, clones the repository, reads its documentation and downloads the libraries, models and other dependencies it judges necessary. Every write action it performs is recorded, and since each can be expressed as a bash command, their concatenation gives the environment definition as a bash script or Dockerfile. In tool implementation, a fresh agent explores the installed repository without carrying over the setup conversation, then an LLM call writes a step-by-step plan and another writes the first candidate function.

It then enters a closed self-correction loop. The environment is restored to the freshly installed snapshot, the candidate runs with the example invocation, and an LLM judges from the returned result and the output streams whether the run succeeded and the result is plausible. If not, an agent diagnoses the root cause — this time without resetting the environment, so it can inspect intermediate files the run produced — the function is re-implemented, and the attempt is summarised. Each new iteration restores the conversation to an earlier snapshot taken before the first attempt, rather than carrying every attempt's messages forward, and appends the summaries of all past attempts together with the current version of the code. The execution environment is a Docker container that ToolMaker controls through an HTTP server running inside it, which keeps it sandboxed from the host and reproducible, and state is restored with Docker's checkpointing.

As described in the paper, ToolMaker uses OpenAI's gpt-4o-2024-08-06 for its LLM calls and o1-mini-2024-09-12 for the planning and implementation steps.

## Adoption & Ecosystem

ToolMaker is evaluated on TM-Bench against [[SoftwareApplication/openhands]], which its authors adapt to produce the same two artifacts; the results are reported on the paper's own page. The authors present it as a step toward agents whose toolsets can be expanded at runtime and toward autonomous, agent-based scientific workflows, while noting that it assumes reasonably well-structured, documented repositories. It is an instance of [[DefinedTerm/tool-creation]] in the paper's sense.
