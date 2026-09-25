---
title: "AutoDev: Automated AI-Driven Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, test-generation, code-generation, sandboxing]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.08299'
    hash: sha256:53380bcd0a97fbbfa9084db3f8d4ee7bfb7bcf2ea5d181f445128a68e48c1257
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Microsoft preprint introducing AutoDev, a framework in which autonomous AI agents achieve user-defined software engineering objectives by editing files, retrieving code, building, executing, testing and running git operations inside a Docker-confined environment under user-configured permissions. With a single GPT-4 agent it reports 91.5% Pass@1 for code generation and 87.8% Pass@1 for test generation on HumanEval."
  author: ["Michele Tufano", "Anisha Agarwal", "Jinu Jang", "Roshanak Zilouchian Moghaddam", "Neel Sundaresan"]
  keywords: ["AI agents", "autonomous software engineering", "test generation", "code generation", "Docker", "guardrails"]
---

The paper argues that AI coding assistants integrated into IDEs, exemplified by GitHub Copilot, mostly suggest code snippets and manipulate files in a chat interface, without using IDE capabilities such as building, testing, executing code or running git operations — so developers still have to run the tests, paste failure logs back into the chat and repeat validation themselves. To fill this gap the authors, all affiliated with Microsoft, present [[SoftwareApplication/autodev]], a fully automated AI-driven development framework in which users define complex software engineering objectives that autonomous AI agents carry out directly within the repository.

AutoDev is organized into four groups of capabilities: a Conversation Manager that tracks the conversation between the user and the agents and parses and permission-checks every command an agent proposes; a Tools Library of commands for file editing, retrieval, build and execution, testing and validation, git and communication; an Agent Scheduler that orchestrates one or more agents; and an Evaluation Environment that executes the commands inside a Docker container. Users configure the permitted commands, the number of agents and their responsibilities through YAML files. The authors describe it as extending [[SoftwareApplication/autogen]] beyond conversation management so that agents interact with the code repository directly, and as building on Auto-GPT with code- and IDE-specific capabilities. The evaluation uses HumanEval for code generation and a modified version of it for test generation.

## Key Points

- With one GPT-4 agent (gpt-4-1106-preview), AutoDev reaches 91.5% Pass@1 on HumanEval code generation, raising GPT-4 from its 67% zero-shot baseline (a 30% relative improvement); the authors place this second on the HumanEval leaderboard at the time, behind Language Agent Tree Search (94.4%), and best among approaches that need no extra training data.
- On test generation — HumanEval modified so that AutoDev writes tests for the human-written solution — it reaches 87.8% Pass@1, a 17% relative improvement over zero-shot GPT-4, and its passing tests reach 99.3% coverage against 99.4% for the human-written tests; counting failing tests as uncovered, overall coverage is 88.8%.
- An average code generation task used 5.5 commands and an average test generation task 6.5; test generation involved more retrieval and more incorrect commands, most of which came from the agent mixing natural language with code or commands.
- Average conversations used 1,656 tokens for code generation and 1,863 for test generation, against an estimated 200 and 373 for zero-shot GPT-4; the authors argue that much of the extra is spent on testing, validation and explanation that a developer would otherwise have to do, and name the Docker-based environment as the main execution cost.
- All agent actions run inside Docker containers, and users can enable or disable individual commands — for example allowing agents only local commits rather than pushes — which the authors present as guardrails for privacy and file security.
- The results rest on HumanEval alone, with multi-agent collaboration disabled in the evaluation; the authors report only preliminary, anecdotal observations that an AI Developer and AI Reviewer pair helped on a complex bug.

## Notes

The evaluation deliberately disabled the `ask` command, so the agent ran without human feedback beyond the initial objective. The `talk` and `ask` commands were described as helpful for developers following the agent's intentions, and `ask` was added at a developer's request during a pilot study in which AutoDev was used as a CLI command with the conversation observable in VS Code. The authors plan to evaluate on more challenging, real-world datasets, integrate AutoDev into IDEs as a chatbot experience, and bring it into CI/CD pipelines and PR review platforms. They frame the result as a change in the developer's role from manually validating AI suggestions to supervising multi-agent collaboration.
