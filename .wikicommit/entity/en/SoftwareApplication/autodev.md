---
title: "AutoDev"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agent-tooling, sandboxing, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.08299'
    hash: sha256:53380bcd0a97fbbfa9084db3f8d4ee7bfb7bcf2ea5d181f445128a68e48c1257
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Microsoft framework for autonomous AI-driven software development in which AI agents achieve user-defined objectives by editing files, retrieving code, building, executing, testing and running git operations inside a Docker container, restricted to the commands the user permits."
  applicationCategory: "Autonomous AI agent framework for software engineering"
  featureList: "Conversation Manager with command parser and output organizer; Tools Library (file editing, retrieval, build and execution, testing and validation, git, communication); Agent Scheduler with round-robin, token-based and priority-based collaboration; Docker-based Evaluation Environment; YAML-configured rules, actions and permissions"
  author: "[[Organization/microsoft]]"
---

AutoDev is a fully automated, AI-driven software development framework from Microsoft, designed for the autonomous planning and execution of software engineering tasks. A user defines an objective — for example, testing a specific method — and AutoDev's AI agents pursue it by performing actions in the repository: writing a test file, running it, reading the failure log, retrieving more context, fixing the file and re-running the tests until they pass, with no developer intervention beyond setting the objective.

The paper introducing it, [[ScholarlyArticle/autodev-automated-ai-driven-development]], positions it against AI coding assistants integrated into IDEs such as [[SoftwareApplication/github-copilot]], which it describes as mostly suggesting code in a chat interface while leaving developers to run tests and validate the output themselves. It describes AutoDev as extending [[SoftwareApplication/autogen]] beyond conversation management so that agents act on the repository, and as LLM-agnostic, allowing models of different sizes and architectures to collaborate on a task.

## Capabilities

Users first configure rules and actions in YAML files, enabling or disabling specific commands and defining the number of agents, their responsibilities and their available actions — for example a "Developer" agent and a "Reviewer" agent. The Conversation Manager initializes and maintains the conversation, parses each agent response into a command and arguments, checks it against the user's permissions, and adds a structured summary of each result to the conversation; it ends the conversation when an agent issues `stop`, a user-defined iteration or token limit is reached, or a problem is detected. The Agent Scheduler decides which agent acts next using round-robin, token-based or priority-based collaboration.

The Tools Library abstracts low-level commands behind simple ones: file editing (`write`, `edit`, `insert`, `delete`, down to a range of lines), retrieval from `grep`, `find` and `ls` up to embedding-based retrieval of similar snippets, build and execution (`build`, `run`), testing and validation (`test`, `syntax`, linters and bug-finding tools), git operations with fine-grained permissions such as allowing only local commits, and communication commands `talk`, `ask` and `stop`. Every command runs inside the Docker-based Evaluation Environment, which returns standard output and errors to the conversation.

## Adoption & Ecosystem

In a pilot study developers used AutoDev as a CLI command while watching the conversation in VS Code; the `ask` command, which lets agents request user feedback, was added at a developer's request during that study. The authors plan to integrate AutoDev into IDEs as a chatbot experience and into CI/CD pipelines and PR review platforms, so that developers can assign tasks and issues to it and review the results in a PR system.
