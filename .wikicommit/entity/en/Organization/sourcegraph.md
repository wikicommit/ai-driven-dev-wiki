---
title: "Sourcegraph"
type: "schema:Organization"
lang: en
tags: [developer-tooling, context-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://sourcegraph.com/blog/agentic-coding'
    hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c
  - type: url
    url: 'https://sourcegraph.com/blog/context-engineering'
    hash: sha256:004e8195be79c691c84abc9a3ab6d698b8815f7ee396e367c8aca94f56715dc3
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A company describing itself as the code understanding platform for enterprise, whose code search and code intelligence products are positioned as a retrieval layer sitting underneath AI coding agents rather than competing with them. It publishes [[Dataset/codescalebench]] and announced SCIP, the code intelligence protocol its index is built with."
  url: "https://sourcegraph.com/"
---

Sourcegraph is a company whose products index source code across an organisation's repositories to make it searchable and navigable, and which since 2026 has positioned that index as context infrastructure for AI coding agents as well as for people. Its own tagline on the material recorded here is "the code understanding platform for enterprise."

Its stated strategic position is deliberately underneath rather than alongside the agents themselves. [[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]] states that its offering "none of this competes with Claude Code, Codex, Gemini CLI, or any other agent. It sits underneath them," and the companion post frames a February 2026 Sourcegraph 7.0 release around the claim that the code intelligence platform is "the shared intelligence layer for both developers and AI agents." The underlying argument the company makes for that position is that coding agents optimise for the code being written while enterprises need visibility into all the existing code.

Everything on this page comes from the company's own blog and is therefore its account of itself.

## History

The material here dates only two moments. Its code search product is described as having been "trusted by enterprise teams for over a decade," and the Sourcegraph 7.0 release is dated February 2026. The company also announced SCIP, an open Protobuf-based code intelligence protocol that it states replaced LSIF and produces compiler-accurate cross-repository navigation.

## Activities & Products

The company indexes repositories across code hosts — GitHub, GitLab, Bitbucket, Gerrit, Perforce, and Azure DevOps are the ones named — into a single search corpus available both through a UI and to agents. The agent-facing surface it emphasises is an MCP server exposing SCIP-backed code intelligence to any MCP-compatible client, reported as offering 13 tools covering keyword and semantic search across repositories, symbol resolution and dependency tracing, cross-repository navigation, commit and diff history, and file reads. The sources also name Amp as an example of a coding agent already wired to Sourcegraph for context, so that teams adopting it get the code graph by default. The individual products are not covered on separate pages here, being vendor product material rather than development methodology.

Its research output is more directly relevant to this wiki's subject. [[Dataset/codescalebench]] is the benchmark it publishes for measuring coding agents on large-codebase and multi-repository tasks, and the two 2026 guides recorded here — [[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]] and [[BlogPosting/context-engineering-a-practical-guide-for-ai-agents]] — set out its framing of [[DefinedTerm/eighty-percent-problem]] and of [[DefinedTerm/context-engineering]] as a four-pillar discipline. It also publishes usage claims drawn from its own customer base, such as the report that 84% of large enterprise accounts saw a steady increase in lines of code after AI rollout.
