---
title: "Crush"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, terminal-agents]
sources:
  - type: url
    url: 'https://charm.land/blog/crush-comes-home/'
    hash: sha256:38219ec2c85fe0ee2206231fc8b703100ea96a34b9746879df882c0e8ddc0f01
  - type: url
    url: 'https://grahamhelton.com/blog/crushing-it.html'
    hash: sha256:75cb6220438a8d614e5a070abbfec5f73355413ea8ce7b15c95c31f51b69556c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A terminal-based AI coding agent written in Go on Charm's terminal UI libraries, originally built by Kujtim Hoxha and now developed at Charm."
  applicationCategory: "AI coding agent"
  author: "[[Organization/charm]]"
---

Crush is a terminal-based AI coding agent. It was built by Kujtim Hoxha, who, according to
[[Organization/charm]], set out a few months before July 2025 to build something that would get
people's attention. It was written in Go on the core of Charm's stack — the Bubble Tea, Bubbles, Lip
Gloss and Glamour libraries. Charm announced in [[BlogPosting/crush-welcome-home]] that the project had
"come home" to the company, where it continues with its original creator and the full support of the
Charm team.

## Capabilities

Charm describes Crush as able to access directly the same command-line tools a developer can — git,
docker, npm, ghc, sed, nix and others — and to use them with extensive knowledge of the tools. As an
illustration of what it can do, Charm's founder says he used Crush to build a GLSL shader generating
layered Gaussian noise for the company website's background in a few minutes.

A user's account of the tool, [[BlogPosting/testing-out-crush-tui-coding-agent]], describes it from the
outside as a TUI coding agent that asks before making an edit, so the user can allow or deny each
change, keeps a list of the files it has changed, and shows the model in use together with the
associated cost. Its `ctrl-p` options include quick switching between models and a summary of the
session. That author ran it in a side pane inside neovim and reports some visual bugs there.

## Adoption & Ecosystem

Charm's case for Crush is a case for the terminal as the interface for AI-assisted development:
developers already live there, and it is fast, scriptable and integrates with existing workflows. The
project, which Charm says is "now called Crush", continues with its original creator alongside the Charm
team.

The same user account treats Crush's model-agnostic design — the user picks which models it uses — as
its most important feature besides the TUI, and reports building a small feature for a personal site
with it, mostly on Sonnet 4 with Gemini Flash for quick edits. Its author concluded that, for him, the
API cost of such use outweighed the experience for regular coding, and planned to keep using Crush for
smaller tasks that do not need expensive models.
