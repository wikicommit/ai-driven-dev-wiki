---
title: "AutoDev (unit-mesh/auto-dev)"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-tools, code-review, multi-agent, coding-agents, open-source]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/autodev-multi-agents-code-review/'
    hash: sha256:652d5c90e9f8d8fae2da5a2576fa0fcaeb7b1469a256821bab8574f5912ceaa0
  - type: url
    url: 'https://www.phodal.com/blog/autodev-remote-agent/'
    hash: sha256:5aa003cf8a64acc7d7d2469af5832b29570bcf56fcc09c3cc621d0b345d5a7b9
  - type: url
    url: 'https://www.phodal.com/blog/build-devops-inside-practise-for-ai-coding/'
    hash: sha256:e4e7bc07f479e47a0e678208bbfb58443125067f5e88b81a88b42c3f55c54f38
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source AI coding tool published in the unit-mesh/auto-dev GitHub repository, with IDE plugins including a VS Code version, a CLI and a desktop application, and a Remote Agent that runs in GitHub Actions; its agentic code review combines diff, lint, issue, test and code-structure information with a multi-agent architecture to analyse changes and generate fixes."
  applicationCategory: "AI coding tool"
  softwareVersion: "1.8 (IDE plugin, April 2024); 0.3.0 (CLI, November 2025); compose-0.3.0 (Desktop, November 2025)"
  featureList: "IDE plugin features including requirement-linked commit message generation, code-smell refactoring, AI rename suggestions and terminal command generation (1.8); AutoDev Remote Agent for issue analysis, task planning and coding in GitHub Actions or as an MCP service; agentic code review (autodev review); static information collection from Git diff, CodeGraph, linters, issues and tests; structured review findings; modification plan generation; automated fixes by a CodingAgent"
---

AutoDev is an AI coding tool whose releases are published in the `unit-mesh/auto-dev` GitHub repository. This page covers the tool in that repository; [[SoftwareApplication/autodev]] is a separate page for a
different framework that shares the name. As described
in [[BlogPosting/ai-code-review-evolved-autodev-multi-agent-architecture]], it can be installed as a CLI from the
npm package `@autodev/cli` or downloaded as AutoDev Desktop.

The problem its code-review feature addresses, as its author presents it, is that the information a reviewer
needs — lint results, tests, issues, change history — is scattered across systems, no single tool understands
complex logic, and manual review is slow and subjective.

## Capabilities

### IDE plugin

Its author presents AutoDev as a code-change assistant: rather than regenerating code for each new requirement,
it helps developers change existing code, and he argues this requires building conventions, best practices and
software knowledge engineering into the tool. Version 1.8 of the plugin, described in
[[BlogPosting/evolutionary-ai-assisted-coding-with-devops-practices]], added several features along those lines:
commit messages generated from the code change together with the user's current requirement ID, fetched through
an internal OA system; refactoring driven by the code smells the IDE's own inspections report; five AI name
suggestions offered when the user invokes the IDE's rename feature (enabled manually in the settings); and
terminal command generation that puts the date, operating system and shell into the context. The same version
added Chinese settings pages and prompts, an easier LLM server test, support for 2024.1 IDE versions and AutoSQL
improvements.

### Code review

In version 0.3.0 of the CLI, review is run with `autodev review -p .`. The review proceeds as a four-step
pipeline: it collects static information (changed hunks from the Git diff, affected classes and methods located
with tools such as CodeGraph, results from linters such as ESLint, Ktlint and Detekt, and related issues and
tests); has an LLM analyse it along a chosen review type (comprehensive, performance, security or style) to
produce structured findings; merges and prioritizes lint and AI findings into a fix plan that the user can edit;
and generates fixes as a patch that can be rolled back or iterated on.

The work is split across agents. A main CodeReviewAgent aggregates information and orchestrates; analysis
sub-agents (AnalysisAgent, ErrorRecoveryAgent, CodebaseInvestigatorAgent) handle large content, error recovery
and repository-wide investigation; and a CodingAgent makes the code changes through tool calls such as
`read_file`, `write_file`, lint and test. Sub-agents are managed by a `SubAgentManager`, and all tools are
registered in a `ToolRegistry` and executed through a `ToolOrchestrator`.

### AutoDev Remote Agent

AutoDev Remote Agent, part of AutoDev Workbench and published in the `unit-mesh/autodev-workbench` repository,
entered a trial phase in June 2025, as announced in [[BlogPosting/autodev-remote-coding-agent]]. It can run as
an MCP service on a server or inside a GitHub project's Actions, where it analyses GitHub issues, plans tasks and
writes code, writing its analysis and plans back to the issue. Its tool design follows AutoDev Sketch's, adding
GitHub tools on top of MCP-wrapped general tools, and a round limit keeps its conversations from looping
indefinitely. Its sandboxing relies on creating a complete code-running environment inside a GitHub Action and
on dynamically creating new GitHub Actions.

## Adoption & Ecosystem

Its author has said that AutoDev will not focus on building its own IDE, citing the cost to an individual of
maintaining one, and that the remote agent reflects a view that, as coding models became able to code
agentically, agents could run on the server to write, test and deploy code. The Remote Agent's first version was
designed with the help of the Augment coding assistant, building on a core refactored out of AutoDev's VS Code
version; making it bootstrap itself is a stated next goal.


For code review, its author says future versions will integrate test coverage, CI/CD and incremental analysis.
