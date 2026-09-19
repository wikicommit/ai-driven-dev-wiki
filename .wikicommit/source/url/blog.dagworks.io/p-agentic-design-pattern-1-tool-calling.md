---
source:
  type: url
  url: 'https://blog.dagworks.io/p/agentic-design-pattern-1-tool-calling'
  hash: sha256:f5276fdca09410e46b0e304c27f4f41294afee574a8aae025568b5534898ad22
  license:

schema:
status: partial
last_generated_at: "2026-09-19"
extracted_tokens: 6844
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agentic-design-pattern-tool-calling.md
  - .wikicommit/entity/en/SoftwareApplication/burr.md
  - .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
failed_pages: []
---

## Summary
The first post in DAGWorks's series on agentic design patterns, covering tool calling and implementing it with Burr, the company's lightweight Python library for building applications as state machines. It argues that "tool" and "function" are synonyms and distinguishes both from structured outputs, then walks through a worked agent: functions defined as tools, their signatures formatted for the OpenAI tool-calling API via Python's inspect module, a Burr action that asks the LLM which tool to call and with what arguments, one action per tool created by binding a parameter, and a final action that formats the result. It closes by arguing that Burr's graph modelling, observability UI and persistence add enough over hand-written code to be worth the dependency.

## Generation Notes
"Elijah ben Izzy" (Person): excluded, exclude_reason "privacy" - the post's named author, a living individual. entity-policy.md excludes living individuals with no public-figure exception; his authorship is recorded in the post's own page frontmatter instead. No existing page was found for him.
"DAGWorks Inc." (Organization): not extracted as an independent subject - the source names it only as the publisher of the post and the maker of Burr, stating no independent facts about the company itself, which SoftwareApplication.md and Organization.md both treat as an incidental mention.
