---
title: "CodeBuddy"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, human-oversight, agent-safety, mcp]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An agentic AI coding system developed by Tencent Cloud and used by its engineers, which can autonomously plan, write, test and deploy code from natural language instructions and calibrates its default human-approval requirements to the risk of each action."
  applicationCategory: "Agentic coding tool"
  featureList: "Autonomous planning, writing, testing and deployment of code from natural language instructions; access to filesystems, terminal commands, external APIs and MCP tools; risk-calibrated default approval requirements per tool; per-project configurable permission levels; plain-language explanations of proposed shell commands; real-time monitoring for command injection"
  author: "Tencent Cloud"
---

CodeBuddy is an agentic AI coding system developed by Tencent Cloud and used by its own engineers.
It can autonomously plan, write, test and deploy code through natural language instructions, with
access to filesystems, terminal commands, external APIs and MCP tools.

[[TechArticle/model-ai-governance-framework-for-agentic-ai]] uses it as a worked example of
designing for meaningful human oversight, on the grounds that it employs a mix of preset secure
defaults and configurable permissions to allow such oversight without overly fatiguing the user.

## Capabilities

Default human-approval requirements correspond to the risk level of each action. Reading — file
contents and directory listings — requires no approval. Editing a file requires approval that is
valid only for that session, so future sessions require new approvals. Shell command execution
through Bash requires approval that is then permanent per project or per command. Network requests
through WebFetch require approval. External tool invocation over MCP is governed through allow, ask
and deny rules, with an additional first-use control in the form of trust verification for a newly
connected MCP server.

Those defaults are a starting point rather than a fixed policy: the default permission level for
each project can be set by each user or organisation, calibrated to the project's context,
potential impact and risk tolerance. The framework's illustration is that lower-risk projects such
as internal documentation sites or prototype repositories with no production credentials may
justify more permissive settings for routine file edits, while projects with access to secrets,
sensitive data, production infrastructure, deployment pipelines or external tools warrant stricter
approval requirements.

Two features are aimed at the quality of the approval rather than its existence. When a complex
shell command is proposed, a plain-language explanation helps the user understand what they are
approving, including any side effects — the framework's example is a `mysqldump` pipeline explained
as creating a compressed, dated database backup under `/backups/`, prompting for the root password,
and leaving the original database unmodified. Separately, continuous real-time monitoring for
command injection can require fresh human approval for a command that matches a previously
whitelisted pattern but is materially riskier, such as a `curl` of a documentation URL followed by
a shell redirection that writes an unexpected file.

## Adoption & Ecosystem

The framework presents CodeBuddy's permission model as one of several industry case studies
illustrating how [[DefinedTerm/human-in-the-loop]] can be kept effective against
[[DefinedTerm/approval-fatigue]] and [[DefinedTerm/automation-bias]], placing it alongside other
deployments that define significant checkpoints, help humans evaluate approval requests, and
complement both with automated monitoring.
