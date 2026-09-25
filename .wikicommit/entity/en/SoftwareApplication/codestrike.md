---
title: "codestrike"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, coding-tools, open-source]
sources:
  - type: url
    url: 'https://github.com/CrowdStrike/codestrike'
    hash: sha256:a6e1e972e6ab62486a1b31f8e2651c1a50c1c36eaabcae1511455d402f492e59
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source, AI-driven pull request review tool written in Go and published by CrowdStrike. Given a pull request, it runs an LLM-powered review over the diff and posts the results back as a single comment."
  applicationCategory: "AI pull request review tool"
  author: "CrowdStrike"
---

codestrike is an open-source, AI-driven pull request review tool written in Go and published by CrowdStrike under the MIT license. Given a pull request, it runs an LLM-powered review over the diff and posts the results back to the pull request as a single comment.

The project describes itself as being in public preview and under active development ahead of a stable 1.0 release, with features that may still change, and asks users to explore and test it but to avoid production deployments for now.

## Capabilities

codestrike talks to GitHub with a personal access token and to a model through an OpenAI-compatible API, whose base URL is configurable, so the model provider is not fixed. A review is started from the command line by pointing `codestrike review` at a pull request URL. Flags let it fetch full file content rather than only the diff, for richer but slower reviews that use more tokens; select a review persona such as security or performance, which maps to a prompt file; and run a dry run that prints the review instead of posting it as a comment. It can also run as a persistent HTTP service with a review endpoint, so that external systems such as CI pipelines, webhooks or chatbots can trigger reviews through an API.

Review behaviour is set in a YAML configuration file: the system prompt, a tone, guardrails such as a maximum patch size and paths to ignore (vendored dependencies, lock files, minified assets), and a token budget expressed as the fraction of each model's context window that may be used for input, with tokens reserved for the response. Project files such as CLAUDE.md can be loaded as additional context for the reviewer, and an option extends this to [[DefinedTerm/agents-md]] files and to Cursor rules in the reviewed repository. The model is asked to reason step by step about each file's changes before producing review comments, and that reasoning block is stripped from the final output; the README calls this [[DefinedTerm/chain-of-thought]] prompting.

## Adoption & Ecosystem

codestrike ships as a plugin for [[SoftwareApplication/cursor]], with a pull-request review skill that lets Cursor's agent review a pull request directly from chat. The skill shells out to the codestrike command-line tool, which must therefore be built and on the user's path; an MCP server is described as planned follow-up work.
