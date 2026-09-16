---
title: "Are AI-assisted Development Tools Immune to Prompt Injection?"
type: "schema:ScholarlyArticle"
lang: en
tags: [mcp, security, agents]
sources:
  - type: url
    url: https://arxiv.org/pdf/2603.21642
    hash: sha256:fd0ab75587fb77f1a54e766576e9fc710b36a78afe06ff29d7801b5a329367eb
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The first empirical analysis of prompt-injection via tool-poisoning vulnerabilities across seven widely-used MCP clients (Claude Desktop, Claude Code, Cursor, Cline, Continue, Gemini CLI, Langflow), evaluating detection/mitigation mechanisms and six security-feature dimensions, and finding Claude Desktop and Cline the most secure overall and Cursor uniformly vulnerable."
  author: ["Charoes Huang", "Xin Huang", "Amin Milani Fard"]
  datePublished: "2026-03-23"
  keywords: ["Prompt injection", "Large Language Model", "Model Context Protocol", "Tool poisoning", "AI-assisted development", "Security posture"]
---

This paper presents the first empirical analysis of prompt injection delivered via tool-poisoning
vulnerabilities across seven widely used [[DefinedTerm/model-context-protocol]] (MCP) clients:
Claude Desktop, Claude Code, Cursor, Cline, Continue, Gemini CLI, and Langflow. The authors first
conduct a comparative analysis of each client's reported vulnerabilities, injection vectors, and
mitigation strategies drawn from existing security research and disclosures, assigning each a
qualitative risk level. They then empirically test all seven clients against four
[[DefinedTerm/tool-poisoning]] attacks — reading sensitive files, logging tool-invocation
activity, creating phishing links, and remote execution of scripts — delivered through a
locally-hosted malicious MCP server, and assess each client's coverage of six security features:
static validation, parameter visibility, injection detection, user warnings, execution sandboxing,
and audit logging.

The empirical results diverge somewhat from the literature-based comparative ranking. Claude
Desktop and Cline are identified as the paper's most secure clients overall, though neither is
fully immune: Claude Desktop shows a partial gap on the logging attack (the logging tool remained
available to be manually invoked, though not automatically), and Cline is unsafe against the
remote-script-execution attack, downloading and executing a script when explicitly instructed
unless the target URL matches a blocklisted domain. Cursor is found to be highly vulnerable across
all four attacks, with no tool-description validation and no parameter filtering; its execution
sandboxing status is listed as unverified rather than confirmed absent. The remaining clients
(Claude Code, Continue, Gemini CLI, Langflow) show inconsistent protection that varies by attack
type. Across all seven clients, the paper identifies common structural weaknesses — lack of static
validation of tool descriptions, insufficient parameter visibility, missing execution sandboxing,
no behavioral monitoring, and an implicit trust model that never verifies server-provided tool
metadata — and argues these stem from fundamental architectural decisions rather than
implementation bugs.

## Key Points
- Empirically tests seven MCP clients against four tool-poisoning attacks and finds Claude Desktop
  and Cline achieve the strongest overall results (three of four attacks blocked, with a partial
  gap for Claude Desktop on logging and an unsafe result for Cline on remote script execution),
  Cursor unsafe on all four attacks, and the remaining four clients (Claude Code, Continue, Gemini
  CLI, Langflow) showing mixed, attack-dependent protection
- Reports that the empirical ranking of client security differs from the ranking the same authors
  derived from a prior literature-based comparative analysis, in which Claude Desktop, Claude Code,
  and Langflow appeared as the lower-risk group
- Finds that 5 of 7 tested clients apply no static validation of tool descriptions before
  registration (2 apply partial validation), and that most clients rely on detecting attacks during
  or after execution rather than preventing them at registration or through sandboxing
- Identifies five recurring structural weaknesses across clients: lack of static validation,
  insufficient parameter visibility, missing execution sandboxing, absence of behavioral
  monitoring, and an implicit trust model with no verification of server-provided tool metadata or
  MCP server reputation
- Recommends that MCP client vendors implement static validation, parameter visibility, sandboxed
  execution, and behavioral monitoring by default, and that organizations audit MCP server
  provenance and require human-in-the-loop approval before granting write access or elevated
  privileges to an agent

## Notes
- The paper's Unsafe/Partial/Safe classifications and risk levels are qualitative judgments made by
  the authors rather than standardized metrics; the authors state the comparative literature
  analysis was conducted independently of the empirical experiments to reduce author bias, and
  report that the two approaches produced different rankings
- Execution-sandboxing coverage was assessed from documentation and architectural analysis rather
  than empirical testing, due to time and resource constraints the authors state explicitly
- Tests were conducted in November 2025 against specific client versions in isolated local
  environments with no real credentials, production systems, or real users involved
