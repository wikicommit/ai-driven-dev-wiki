---
title: "Agentic Search"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-tooling, retrieval]
sources:
  - type: url
    url: 'https://claude.com/blog/building-agents-with-the-claude-agent-sdk'
    hash: sha256:895d1a97d551333d37c154b093d44ddda469401d6c2596c7a363373e974754a4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Having an agent find the context it needs by searching a file system itself — deciding what to load with tools such as grep and tail — rather than relying on a pre-built embedding index. Anthropic recommends it as the starting point over semantic search."
---

Agentic search is an approach to retrieval in which an agent gathers its own context by searching a
file system with ordinary tools, deciding for itself what to pull into its context window. In
Anthropic's description, the file system represents information that *could* be pulled into the
model's context: when Claude encounters large files such as logs or user-uploaded files, it decides how
to load them by using bash tools like `grep` and `tail`. On that account the folder and file structure
an agent works in becomes a form of [[DefinedTerm/context-engineering]] in its own right.

## Usage

Anthropic uses the term in [[BlogPosting/building-agents-with-the-claude-agent-sdk]] as one of the ways
an agent built on the [[SoftwareApplication/claude-agent-sdk]] gathers context, the first stage of the
gather-context, take-action, verify-work loop the post describes. Its worked example is an email agent
that stores previous conversations in a folder named `Conversations`, so that it can search them when
asked about earlier exchanges.

The term is defined there by contrast with semantic search, which chunks the relevant context, embeds
the chunks as vectors and searches for concepts by querying those vectors. The post characterises
semantic search as usually faster than agentic search but less accurate, more difficult to maintain
and less transparent.

## When It Applies

Anthropic's recommendation is to start with agentic search and to add semantic search only if faster
results or more variations are needed. The approach assumes an agent that has a file system and
shell tools to search it with, and it trades speed for the accuracy, maintainability and transparency
the post attributes to it. How well-established it is: the comparison with semantic search is stated
as Anthropic's own guidance, drawn from its teams' experience building agents on the SDK, and the
post gives no measurements for it.

## Related Terms

- [[DefinedTerm/just-in-time-context-retrieval]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/sub-agent-architecture]]
