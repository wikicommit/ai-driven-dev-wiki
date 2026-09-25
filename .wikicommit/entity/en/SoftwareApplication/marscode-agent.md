---
title: "MarsCode Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, program-repair, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2409.00899'
    hash: sha256:2014b1e14f5cc4a5abb1174a2723cac2db5dc19b8d6647801539698c9f80a0ef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An LLM-based agent framework from ByteDance for automated bug fixing, in which several role-specific agents retrieve code, plan, reproduce, edit and test to produce a patch for an issue."
  applicationCategory: "Automated bug-fixing agent framework"
  featureList: "Multi-agent collaboration (Searcher, Planner, Reproducer, Programmer, Tester, Editor); dynamic debugging and static repair workflows; code knowledge graph retrieval; language server protocol retrieval with fuzzy positioning; file and grep search; AutoDiff code editing; LSP static code diagnostics; Docker-based runtime sandbox"
---

MarsCode Agent is a framework from ByteDance that uses LLMs to automatically identify and repair
bugs in software code. It is introduced in
[[ScholarlyArticle/marscode-agent-ai-native-automated-bug-fixing]], which describes it as building
an agent framework and providing agents with interactive interfaces and tools for code retrieval,
debugging and editing, so that agents can take over some software engineering tasks.

## Capabilities

Work is divided among six roles. The Searcher collects code snippets related to the issue using the
code knowledge graph and the language server protocol; the Planner analyzes them and classifies the
issue into a dynamic debugging or a static repair workflow; the Reproducer writes a reproduction
script and confirms the issue reproduces in a sandbox; the Programmer edits the code; the Tester
checks each version against the reproduction script; and the Editor proposes multiple repair
solutions for static repair. Only the Programmer and the Editor can edit code, only the Programmer
can reset the repository, and only the Reproducer and the Tester can run reproduction scripts. In
dynamic debugging the Programmer and the Tester iterate until the issue is resolved, in a runtime
sandbox set up in a Docker container. In static repair, drawing on an approach similar to
[[DefinedTerm/agentless]], several candidate fixes are generated in a single LLM request,
normalized with an AST, merged and voted on.

For retrieval, MarsCode Agent builds a code knowledge graph whose nodes are code entities such as
variables, functions, classes and files, and whose edges record file structure, function calls and
symbol references; an agent's query goes through entity recognition, embedding similarity and
keyword search against the graph, and the merged candidates are re-ranked. The language server
protocol complements the graph for definitions and references outside the target project, with
fuzzy positioning that works out an LSP request from a file name, line number or identifier the
agent supplies. General file search and grep are also available.

Code edits are written in AutoDiff, a format inspired by Aider that resembles git conflict markers:
the agent gives the file path, the original code and the replacement code, and the tool matches the
original snippet to the most similar segment of the file, replaces it, adjusts indentation and
produces a unified diff. Each edit is then checked with LSP static diagnostics before and after the
change, and if new errors at the Fatal or Error level appear, the diagnostics are returned to the
agent for further changes.

## Adoption & Ecosystem

The report evaluates MarsCode Agent on SWE-bench Lite, part of [[Dataset/swe-bench]], and compares
its code retrieval with other publicly traceable solutions, including CodeR, Moatless and Agentless.
Its authors list reducing LLM call costs, improving user-agent collaboration and supporting dynamic
debugging within real user workspaces among their plans for the framework.
