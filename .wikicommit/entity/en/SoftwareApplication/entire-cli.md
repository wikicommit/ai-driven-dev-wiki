---
title: "Entire CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, cli, open-source, agent-tooling]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.20779'
    hash: sha256:2da8cc42c5f1fad936e428f3013e1a312598cbf5a01c8c1112ea9578963593b4
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source command-line tool from Entire.io that automatically logs coding-agent sessions in a repository and links them to code commits with line-level attribution of which lines a human and which an agent wrote."
  applicationCategory: "Developer tool"
  featureList: "Coding-agent session transcript logging; checkpoints linked to commits; line-level human-versus-agent code attribution"
---

The Entire CLI is an open-source tool from Entire.io that, once a developer enables it in a
repository, automatically records coding-agent session transcripts and links them to the resulting
code commits with line-level attribution of human-written versus agent-written lines. According to
the SWE-chat authors, it addresses a growing difficulty in reviewing, understanding and validating
AI-generated contributions by letting developers track how a codebase evolved not only commit by
commit but prompt by prompt, creating a searchable record of every AI-assisted change. The tool was
publicly launched on February 10, 2026.

## Capabilities

The CLI installs git hooks in the repository and records session transcripts for several coding
agents — [[SoftwareApplication/claude-code]], OpenCode, [[SoftwareApplication/gemini-cli]],
[[SoftwareApplication/cursor]] and Factory AI Droid — with Claude Code the first one it supported.
The logs capture user prompts, agent responses, tool calls such as file edits, shell commands and code
searches, and token usage. Transcripts, together with checkpoint and session metadata, are stored on a
dedicated branch of the repository (`entire/checkpoints/v1`), and each checkpoint is linked to a
commit. Attribution is computed at commit time using temporary checkpoints on shadow branches, which
yields the split of committed lines between human and agent.

## Adoption & Ecosystem

Developers who push this checkpoint branch to a public GitHub repository make their sessions publicly
readable, and that is the basis of [[Dataset/swe-chat]]: its collection pipeline finds such
repositories through GitHub code search, downloads the checkpoint directories and parses the raw
transcripts. In the accompanying study,
[[ScholarlyArticle/swe-chat-coding-agent-interactions-from-real-users-in-the-wild]], the tool's own
repository contributed less than 20% of sessions at the time of writing, a share the authors report
declining as adoption spread after launch.
