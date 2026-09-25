---
title: "Testing out Crush, a TUI based coding agent (in neovim btw)"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, terminal-agents]
sources:
  - type: url
    url: 'https://grahamhelton.com/blog/crushing-it.html'
    hash: sha256:75cb6220438a8d614e5a070abbfec5f73355413ea8ce7b15c95c31f51b69556c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2025 personal blog post by Graham Helton recounting his first use of Charm's terminal-based coding agent Crush to build an Open Graph image generator for his static site, with his impressions of its interface and his reasons for not adopting it for regular coding on cost grounds."
  author: ["Graham Helton"]
  datePublished: "2025-08-03"
---

In this post Graham Helton tries out [[SoftwareApplication/crush]], the AI coding agent that
[[Organization/charm]] released to run in the terminal, by using it to add Open Graph image
generation to his personal static site — a tool that renders each post's frontmatter into a
press-release-styled HTML page and saves it as a PNG. He chose the task because he had done it before
with other tools, it was low-risk, and the metadata it needed was already in each post's YAML
frontmatter. He reports finishing the feature and integrating it into his site's build script with
minimal hiccups.

The post is a firsthand account from one developer's single project, and its conclusions are framed as
his own: he liked the tool's experience but would not use it for regular coding until he had
self-hosted GPUs, because of what the API usage cost him.

## Key Points

- The author found Crush to be what he expected from Charm: a TUI coding agent with Charm's look and
  feel, which would feel familiar to someone who has used [[SoftwareApplication/claude-code]].
- He ran Crush in a dedicated side pane inside neovim, which let him watch what it was doing and allow
  or deny its changes, or close it quickly while working manually; he reports some visual bugs when
  running it inside a neovim window.
- He found the diff UI jarring at first, though workable for prompts that make fairly precise edits.
- He singles out Crush's list of changed files, its display of the model in use and the associated
  cost, and its `ctrl-p` options — in particular quick switching between models and session
  summarization — as features he valued.
- In his view the most important part of Crush, besides its TUI, is that it is model-agnostic, letting
  the user choose which models to use; he wants to try it with locally hosted models, which he says is
  not possible with tools like Claude Code.
- He reports that implementing the feature cost $23.04 in API fees, mostly using Sonnet 4 for the heavy
  lifting and Gemini Flash for quick edits and documentation updates, and took about 45 minutes against
  the few hours over a couple of days he estimates it would have taken him by hand.
- He argues that tools like [[SoftwareApplication/cursor]] have two pricing advantages over paying
  API fees directly: extensive optimization of what is sent to the model, including caching, and
  economies of scale from partnering with model providers — so that for about what this one feature
  cost him in API fees, a Cursor subscription would buy a very large number of prompts on larger
  models. This is his own assessment, supported by his own usage dashboard rather than any measurement.
- He still plans to use Crush for smaller tasks that do not need expensive models, such as answering
  questions about a fairly simple codebase or making quick changes to a homelab.

## Context

The author writes that he wanted to try Crush because he dreads the experience of Cursor's
VS Code-centric UI, and that his site is for personal enjoyment rather than efficiency.
