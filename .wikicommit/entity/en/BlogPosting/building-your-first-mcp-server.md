---
title: "Building your first MCP server: How to extend AI tools with custom capabilities"
type: "schema:BlogPosting"
lang: en
tags: [tool-use, agent-tooling]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/building-your-first-mcp-server-how-to-extend-ai-tools-with-custom-capabilities/'
    hash: sha256:79fe71c090476d29a3745d92b375a5354c83e43dff0abc079080c9c6d7048789
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub developer-relations walkthrough that teaches the Model Context Protocol by building a TypeScript MCP server for turn-based games, played against GitHub Copilot in VS Code."
  author: ["Chris Reddington"]
  datePublished: "2025-08-22"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog by a developer advocate in GitHub's Developer Relations team, accompanying
a Rubber Duck Thursdays live stream. It introduces the [[DefinedTerm/model-context-protocol]] as a
standardized way to give AI tools context and actions they lack by default — checking a GitHub issue,
running a Playwright test, calling an API — and learns it by building something visual: a web app in
which the user plays Tic-Tac-Toe and Rock Paper Scissors against [[SoftwareApplication/github-copilot]],
with the opponent's moves orchestrated by an MCP server.

The project is a single TypeScript repository holding a Next.js web app and API, an MCP server built
on the MCP TypeScript SDK, and a shared library of game types and logic, published as
`github-samples/turn-based-game-mcp`. The post uses it to explain MCP's architecture and its three
core server building blocks, then turns to the considerations that apply to real servers.

## Key Points

- The problem MCP addresses, as the post states it: AI tools cannot natively reach private data, the
  latest documentation or real-time data, and cannot take actions such as opening pull requests; before
  MCP there was no standard way to integrate them with third-party tools, so each AI tool could need its
  own plugins and integration patterns.
- MCP follows a client-server pattern: the host is the AI tool (such as Copilot in VS Code), clients
  live inside the host with a 1:1 relationship to a server, and servers provide tools, resources and
  prompts.
- Registering a server with a host is described as the step that gives the agent its capabilities; in
  VS Code this is a `.vscode/mcp.json` file listing each server and the command that starts it.
- Tools are actions the AI can take, each with a description and input schema. In the demo the model
  does not calculate game moves — calling a tool runs a handler on the server that executes the game
  logic.
- Resources give the AI context, often under a URI-based identifier; the demo defines custom
  `game://` URIs that the server translates into calls to its local API.
- Prompts are predefined, reusable guidance shipped with a server, which users reach through slash
  commands in VS Code (the demo's `/strategy`).
- The author notes that the specification has since added further capabilities, including sampling
  and elicitation, which the demo does not use.
- Production servers may need authentication and authorization; the post cites the
  [[SoftwareApplication/github-mcp-server]]'s OAuth and personal-access-token support as an example,
  while the demo has none.
- It advises checking for an existing server before building one, and doing due diligence on
  third-party MCP servers as on any supply-chain dependency — whether you recognize the publisher and
  whether the code is open to review.
- Its advice for building your own is to start simple, with focused servers that solve specific
  problems.

## Context

The post is an introductory, learning-by-building account from GitHub's developer relations, and its
examples are drawn from GitHub's own ecosystem (Copilot in VS Code, the GitHub MCP server) alongside
Playwright's MCP server. It explains MCP from a practitioner's side — configuring and building a
server — rather than analysing the protocol's design or limitations. The author chose TypeScript to
keep frontend, backend and server in one language and repository, and notes that a more robust setup
would distribute the server as a package or container image with versioning and publishing processes.
