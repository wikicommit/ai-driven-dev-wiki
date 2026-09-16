---
title: "Red-Teaming Coding Agents from a Tool-Invocation Perspective: An Empirical Security Assessment"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.05755'
    hash: sha256:8e50b266c6e2a6123f82bdf0c720da2858a0661af4273550d96402af17f54c6c
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The first systematic security red-teaming of six popular real-world coding agents (Cursor, Claude Code, Copilot, Windsurf, Cline, Trae) from a tool-invocation perspective, introducing a prompt-exfiltration technique (ToolLeak) and a two-channel prompt-injection technique that achieved remote code execution on every tested agent."
  author: ["Yuchong Xie", "Mingyu Luo", "Zesen Liu", "Zhixiang Zhang", "Kaikai Zhang", "Yu Liu", "Zongjie Li", "Ping Chen", "Shuai Wang", "Dongdong She"]
  datePublished: "2026-06-28"
  keywords: ["Red-Teaming", "Coding Agents", "Tool Invocation"]
---

This paper presents what it describes as the first systematic, tool-invocation-focused security red-teaming of six widely-used real-world coding agents (Cursor, Claude Code, GitHub Copilot, Windsurf, Cline, Trae) across their officially supported backend LLMs. The red-teaming proceeds in two phases: prompt exfiltration (recovering an agent's hidden system prompt and tool metadata), and tool-invocation hijacking (using the recovered information to trigger unauthorized command execution).

Its central technical contributions are [[DefinedTerm/toolleak]], a technique exploiting a gap between how models handle ordinary chat replies versus schema-driven tool-argument generation to exfiltrate hidden prompts, and a [[DefinedTerm/two-channel-prompt-injection]] technique that combines a malicious tool's description and its return value to hijack an agent's command-execution behavior.

## Key Points

- ToolLeak achieved the best prompt-exfiltration performance across all six agents in an emulated setting, and the best "pseudo-recall" score (a proxy metric, since ground-truth system prompts for commercial products are unavailable) on 18 of 25 tested agent-LLM combinations in the real-world setting, reaching near-perfect scores (e.g. 1.00) on Cursor and Claude Code with several backend models.
- The two-channel prompt-injection technique achieved remote code execution on every one of the six tested coding agents in at least one configuration, and consistently outperformed four single-channel baselines (adapted from AgentDojo, InjecAgent, and MCPTox, plus a single-channel version of the paper's own attack) in a head-to-head comparison.
- Testing across older and newer agent/model releases found a clear hardening trend: newer versions of Cursor and Claude Code that adopt "progressive disclosure" (surfacing only tool names to the model rather than full tool descriptions) blocked the description-channel lure that the attack depends on, and newer backend models (e.g. Claude Sonnet 4.6, Opus 4.7) showed stronger refusal behavior even when the return channel remained open — reducing the two-channel attack's success rate to 0.0 on Claude Code and at most 0.3 on Cursor across new-generation backends.
- Agents without comparable architectural redesigns remained exposed regardless of backend: the paper reports the two-channel attack still achieved a 1.0 success rate on Cline, Windsurf, and Trae with certain newer backend models (e.g. Gemini 3.1-pro).
- Of the defenses evaluated, perplexity-based anomaly detectors failed to flag the malicious tool descriptions used in testing, a prompt-injection-specific classifier (Llama-Prompt-Guard-2-86M) detected the majority of malicious cases, and tool-level runtime scanners (Agent-Scan, MCP Safety Scanner) that inspect invocation traces rather than individual tokens flagged the payloads on all six evaluated agents.
- The paper attributes the root cause of tool-invocation hijacking to an architectural issue rather than a model-alignment gap alone: current agent designs treat model-generated tool calls and their returned outputs as homogeneous text streams, with no clean separation between instructions and data, and it points to prior instruction-data-separation architectures (SecAlign, MetaSecAlign, StruQ) as a more durable direction than reactive detection.
- The paper frames its threat model as requiring the attacker to get a victim to connect to an attacker-controlled external tool (e.g. via an under-vetted MCP registry) but not requiring root/admin privileges, control of the backend LLM, or the ability to directly invoke privileged built-in tools.

## Notes

The paper is a preprint; its case studies target specific named products and versions as of the time of testing, and the paper's own results already show several of the tested vendors (Cursor, Claude Code) had shipped architectural mitigations (progressive disclosure) by later releases, so the reported attack success rates are version- and configuration-specific rather than a permanent characterization of any product. The paper's own code/artifact repository link is hosted on an anonymized-hosting domain.
