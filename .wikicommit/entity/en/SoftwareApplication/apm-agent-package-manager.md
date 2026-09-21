---
title: "APM (Agent Package Manager)"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-primitives, agent-tooling, package-management, ci-cd]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering/'
    hash: sha256:f4175892bf17116173c4ae2a309b3b81b227800f09d53afa3ad1ade536e02a2d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A package manager and runtime manager for agent primitives — the Markdown instruction, prompt and chat-mode files an agent reads — proposed as the npm-equivalent layer for distributing them. It installs and configures agent CLI runtimes, resolves MCP dependencies declared in an apm.yml file, and runs named scripts locally or in CI."
  applicationCategory: "Package manager / runtime manager for agent primitives"
  featureList: "Unified agent CLI runtime installation; MCP dependency resolution; apm.yml project configuration; named script execution; GitHub Action for CI/CD"
  author: "Daniel Meppiel"
---

APM, the Agent Package Manager, is a command-line tool for managing and distributing
[[DefinedTerm/agent-primitives]] — the Markdown files, such as `.prompt.md` and `.instructions.md`,
that carry an agent's instructions. This wiki's account of it comes from
[[BlogPosting/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering]],
written by its author, which presents it as the missing infrastructure layer for those files.

The argument it is offered in answer to is that agent primitives are genuine software written in
natural language rather than code — modular, reusable, with dependencies and versions — and that
distributing Markdown files by hand while keeping MCP dependencies consistent across environments
becomes unwieldy. The source's stated analogy is explicit and repeated: APM is meant to be for
agent primitives what npm is for JavaScript, and the post credits npm's package distribution
solution with enabling JavaScript's growth.

The tool is described as extending an existing VS Code workflow rather than replacing it. The
source states that daily development stays the same, and that the same `apm run` command works
across whichever runtime is installed.

## Capabilities

Two roles are described. As a runtime manager, APM installs and configures agent CLI runtimes,
which the source frames as a response to each vendor CLI having its own installation procedure,
configuration requirements and compatibility matrix. As a package manager, it creates distributable
packages of primitives together with their dependencies, configuration and runtime compatibility.

Project configuration lives in an `apm.yml` file the source calls the `package.json` equivalent,
defining named scripts, dependencies and input parameters. Its worked example declares scripts that
invoke different runtimes over the same prompt file — one calling `copilot` with a
`security-review.prompt.md`, another calling `codex` with the same file — and declares an MCP
dependency on `ghcr.io/github/github-mcp-server`.

The commands the source shows follow npm's shape: `apm init` to start a project, `apm compile` to
turn agent primitive files into `Agents.md` files, `apm install` to install MCP dependencies, and
`apm run <script>` with `--param` arguments to execute a workflow. The source states that
distribution is currently by sharing the `apm.yml` and primitive files — a team member clones the
repository, compiles and installs — and marks `apm publish` as future work rather than a shipped
command.

## Adoption & Ecosystem

The production half of the tool is an APM GitHub Action, which the source shows running the same
project's scripts in a CI pipeline on pull request events, with the workflow's matrix values
corresponding to the script names in `apm.yml`. In that arrangement APM installs the declared MCP
dependencies and passes input parameters through to the prompt file, so the primitives developed
in an editor run unchanged as part of the delivery process — what the source calls continuous AI.

APM occupies the third of four stages in the ecosystem progression the source predicts: primitive
files, then agent CLI runtimes, then package management, then a thriving ecosystem of shared
libraries and community packages. That placement is the author's own framing of his own tool, and
the source reports no adoption figures, no evaluation, and no version number for APM itself.
