---
title: "Chrome DevTools MCP"
type: "schema:SoftwareApplication"
lang: en
tags: [mcp, coding-tools]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/ai-coding-workflow/'
    hash: sha256:bb23e1f299d66f8dc6e402e687b71bed11c3c380f0544deff076220a9c992780
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An MCP integration that gives an AI coding agent direct access to a live browser — the DOM, performance traces, console logs and network traces — so that bugs can be diagnosed from runtime data rather than from static code alone."
---

Chrome DevTools MCP is a [[DefinedTerm/model-context-protocol]] integration that lets AI tools see what the browser can see. It grants an agent direct access to inspect the DOM and to obtain rich performance traces, console logs and network traces — described in [[BlogPosting/my-llm-coding-workflow-going-into-2026]] as giving an agent "eyes". Its source code is on GitHub at <https://github.com/chromeDevTools/chrome-devtools-mcp>.

## Capabilities

Its purpose is to bridge the gap between static code analysis and live browser execution. By exposing runtime data from the browser to the agent, it removes the friction of manually switching context to relay that information, and allows UI testing to be automated directly through the LLM, so that bugs can be diagnosed and fixed based on actual runtime data.

## Adoption & Ecosystem

Addy Osmani, whose earlier team built it, describes using it as part of his debugging and quality loop when coding with AI agents.
