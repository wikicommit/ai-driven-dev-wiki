---
title: "GitHub MCP Server"
type: "schema:SoftwareApplication"
lang: en
tags: [tool-use, agent-tooling]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/building-your-first-mcp-server-how-to-extend-ai-tools-with-custom-capabilities/'
    hash: sha256:79fe71c090476d29a3745d92b375a5354c83e43dff0abc079080c9c6d7048789
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-idea-to-pr-a-guide-to-github-copilots-agentic-workflows/'
    hash: sha256:d26a28f8e99d98794a771d2e9f313c93e3141162781714ff1bfd49653195fa0b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "GitHub's own Model Context Protocol server, which gives AI tools access to GitHub data and actions — issues, pull requests, Dependabot alerts — under the access the user grants via OAuth or a personal access token."
  applicationCategory: "Model Context Protocol server"
  author: "[[Organization/github]]"
---

The GitHub MCP Server is the [[DefinedTerm/model-context-protocol]] server that
[[Organization/github]] ships for connecting AI tools to GitHub. Through it an agent can get
information from existing issues or pull requests, list Dependabot alerts, and create and manage
issues and pull requests, all within the access the user provides.

A GitHub developer advocate presents it as a real-world example of the patterns an MCP server
follows, and as a reason not to build a server of your own where one already exists: rather than
creating your own version, their suggestion is to contribute upstream to improve it for everyone.

## Capabilities

It is offered both as a remote server and for local use. Access is granted through OAuth flows in
the remote server, and through a personal access token in both the local and remote forms.

The remote server is presented as a way to reduce the overhead of running MCP servers locally,
which is commonly done through npm packages or Docker containers, and, according to GitHub's
walkthrough, lets users
authenticate with OAuth 2.0 instead of a personal access token. It gives AI tools live GitHub
context and tools such as issues, pull requests and code files; using it from VS Code means
updating the MCP configuration as the project's repository documents. That walkthrough also notes
the server is open source.

## Adoption & Ecosystem

GitHub's tutorial on building MCP servers points readers to it for use in their own workflows or
for studying a real-world implementation ([[BlogPosting/building-your-first-mcp-server]]), and a
second walkthrough uses the remote server alongside the [[SoftwareApplication/github-copilot-coding-agent]]
in an issue-to-pull-request workflow ([[BlogPosting/from-idea-to-pr]]).
