---
source:
  type: url
  url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
  hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 2377
generated_pages:
  - .wikicommit/entity/en/BlogPosting/dotagents-standard-agent-skill.md
  - .wikicommit/entity/en/DefinedTerm/dotagents.md
  - .wikicommit/entity/en/SoftwareApplication/dotagents-standard-skill.md
  - .wikicommit/entity/en/DefinedTerm/agents-md.md
  - .wikicommit/entity/en/DefinedTerm/progressive-disclosure.md
failed_pages: []
---

## Summary

A practitioner's write-up of dotagents-standard, an Agent Skill packaging the dotagents convention credited to Brandon Greenwell: split a project's agent context into a slim always-read AGENTS.md router and a hidden .agents/ library organised by kind — rules, context, memory, personas, skills, specs, logs. Its stated contribution beyond the convention is the classification taxonomy, since the standard says context should be split by kind but not which kind a given paragraph is; it singles out rule-versus-memory and context-versus-specs as the confusions that matter. Routing rules must name a trigger and carry an action verb, or an unconditional router simply recreates the monolith one directory deeper. The skill applies progressive disclosure to its own material and is MIT-licensed.
