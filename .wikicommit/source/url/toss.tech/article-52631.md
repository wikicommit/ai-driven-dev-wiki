---
source:
  type: url
  url: 'https://toss.tech/article/52631'
  hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
  license:

schema:
status: partial
last_generated_at: '2026-09-22'
extracted_tokens: 4463
generated_pages:
  - .wikicommit/entity/en/BlogPosting/making-ai-follow-team-rules.md
  - .wikicommit/entity/en/DefinedTerm/lost-in-the-middle.md
  - .wikicommit/entity/en/SoftwareApplication/pfmls-stylepack.md
  - .wikicommit/entity/en/DefinedTerm/agent-hooks.md
failed_pages: []
---

## Summary

A Toss Bank ML engineer describes why team coding conventions stop being followed as a coding-agent session lengthens -- the rules, loaded once at the start, drift into the middle of the context, which is the position the model attends to least -- and why writing them into a project-root instruction file does not fix it. The team's answer is a plugin, pfmls-stylepack, that injects the relevant conventions through hooks at two points inside the agent loop: immediately after each file is written, and again as the agent tries to finish, when it reviews the whole change as a diff. The post also describes instrumenting the plugin against itself, using logs of which rules fired to tighten a trigger that misfired across 21 sessions without changing any code, and to move defects that only appear at runtime out of triggered rules and into always-loaded context.

## Generation Notes

- "김경윤": excluded, privacy -- the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment: he is central to this source's subject. No page exists for this entity.
