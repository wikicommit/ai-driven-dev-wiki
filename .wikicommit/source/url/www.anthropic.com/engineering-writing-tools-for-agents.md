---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
  hash: sha256:effc06d088266ee895582c23541e543435288246b1dc4d89d3a2f4b8a1993b54

schema:
status: generated
last_generated_at: "2026-08-20"
extracted_tokens: 7649
generated_pages:
  - .wikicommit/entity/en/TechArticle/writing-effective-tools-for-agents.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
  - .wikicommit/entity/en/Organization/anthropic.md
failed_pages: []
---

## Summary

An Engineering at Anthropic post of 11 September 2025 by Ken Aizawa on designing tools for agents rather than for other software, on the premise that a tool is "a contract between deterministic systems and non-deterministic agents". It contributes two things the wiki did not have: an evaluation-driven loop in which agents are used to improve their own tools, and five concrete design principles — choosing tools that suit an agent rather than wrapping existing API endpoints, namespacing, returning only high-signal context, optimizing responses for token efficiency, and prompt-engineering tool descriptions. Because the argument throughout is about spending an agent's limited context well, it also extends the context engineering page: the tool layer, including tool descriptions and error messages, is a context-engineering surface under the same budget as everything else.

Ken Aizawa did not become a page. He is named only as the post's author, with no independent facts about him stated in the source, which is an incidental mention rather than an independent subject; the author is recorded as plain text in the article page's frontmatter instead.
