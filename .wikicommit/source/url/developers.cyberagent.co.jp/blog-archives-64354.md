---
source:
  type: url
  url: 'https://developers.cyberagent.co.jp/blog/archives/64354/'
  hash: sha256:7ac3321a16784860220e265d36626c789264513a777c2bb4d5e8056552855f2d
  license:

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 6541
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/agent-as-a-judge.md
  - .wikicommit/entity/en/BlogPosting/agent-as-a-judge-in-the-feedback-loop.md
failed_pages: []
---
## Summary

A CyberAgent engineer describes implementing Agent as a Judge — an evaluation agent that inspects a coding agent's execution transcript rather than its diff — and wiring it into the development feedback loop through a Claude Code Stop hook. The judge first collects the session's commands, file reads and token cost, then actively verifies each completion claim against evidence such as CI status or execution logs, scoring six axes and taking the weakest as the overall verdict. Its output is a human-readable Markdown report including a work timeline, plus a JSON verdict carrying a suggested next action per axis.
