---
title: "DeepSeek Harness"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, agent-architecture, open-source]
sources:
  - type: url
    url: 'https://github.com/deepseek-ai/deepseek-harness'
    hash: sha256:73b3f3e39f8b81a409e0d59b1885722d53cc505cf0ee89cfe1ec6d34ae864145
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source agent harness from DeepSeek AI, invoked as `dsh`, built on an everything-is-a-plugin architecture powered by the Cordis framework and run through a local web UI; released as a developer preview."
  applicationCategory: "Agent harness"
  author: "DeepSeek AI"
---

DeepSeek Harness, invoked as `dsh`, is an open-source [[DefinedTerm/agent-harness]] developed by
DeepSeek AI and released under the MIT license. Its tagline, "Everything is a Plugin", names its
architecture: the harness is built on an everything-is-a-plugin design powered by the Cordis framework.

## Capabilities

The harness is launched with `npx @deepseek-ai/dsh web`, which starts a web UI on the local machine
(by default at `127.0.0.1:3080`) and opens it in the browser; over SSH it prints the host address
instead, since the SSH client or editor owns the forwarded local address. It can also be built and run
from a checkout of the repository, and the project's development tooling covers both a web and a
desktop application. The project is explicitly a developer preview that is iterating rapidly, and its
README warns in capitals that there will be compatibility-breaking changes and asks users to read a
safety notice before running it.

## Adoption & Ecosystem

Because extension happens through plugins, the project asks plugin authors to tag their repositories
with the `dsh-plugin` GitHub topic so that plugins can be discovered. The README also directs coding
agents working on the repository to follow its `AGENTS.md` ([[DefinedTerm/agents-md]]).
