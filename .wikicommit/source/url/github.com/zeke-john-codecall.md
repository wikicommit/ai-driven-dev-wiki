---
source:
  type: url
  url: 'https://github.com/zeke-john/codecall'
  hash: sha256:088c8dadf1684aa880483ee2f14fc8310b9d0a31d04e019dd85036137dbae151
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 8205
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/codecall.md
failed_pages: []
---

## Summary

Codecall is an open-source TypeScript implementation of programmatic tool calling for AI agents: instead of exposing every tool definition to the model and calling tools one inference at a time, it gives the agent two tools — readFile and executeCode — plus a file tree of TypeScript SDK files generated from connected MCP servers, and lets the agent write code that orchestrates the tools inside a Deno sandbox. Tool calls from the sandbox are intercepted by a proxy and routed over IPC to the host, errors return full stack traces, a progress() function streams step-by-step updates, and agents that recover from a tool error annotate the SDK file with a learned constraint for later runs. The README reports 74.7% fewer tokens and 92.3% fewer tool calls than a traditional agent in its side-by-side demo.
