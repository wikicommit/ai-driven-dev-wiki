---
source:
  type: url
  url: 'https://jonghoonpark.com/2026/03/29/agentic-engineering'
  hash: sha256:92fea29c2779ce511435e3c79aeb42f9b33855c8f3a1f24849a1c6993534b024
  license:

schema:
status: generated
extracted_tokens: 1770
last_generated_at: "2026-09-21"
generated_pages:
  - .wikicommit/entity/en/BlogPosting/lessons-from-releasing-a-product-with-ai-agents.md
  - .wikicommit/entity/en/DefinedTerm/agentic-engineering.md
  - .wikicommit/entity/en/DefinedTerm/agent-skills.md
failed_pages: []
---

## Summary

A Korean write-up of a conference talk in which a self-described conservative developer recounts rebuilding and releasing the K-DEVCON community site with Claude Code. It traces the move from vibe coding to agentic engineering, argues against economizing on tokens on the grounds that a developer's cognitive flow is the more expensive resource and that debugging should be handed back to the agent rather than taken over by the developer, and presents test code as the mechanism that makes AI-written code trustworthy — covering architecture rules, coverage thresholds and static analysis in the test pipeline, not only logic. It reports concrete uses including two-track routing that serves crawlers pre-generated static OG HTML so SEO works without SSR, a weekly loop running a third-party SEO skill and feeding its findings back to the agent, Lighthouse output handed to the agent as JSON, and templating repeated prompts as Skills. It closes on the last 20% AI does not fill: AI supplies answers but only a developer with direct experience chooses the direction, and AI carries no responsibility.

## Generation Notes

- "박종훈" (the post's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment: he is the firsthand subject of this account. No page exists for this entity.
- "Andrej Karpathy": excluded, privacy — a living individual, ruled out by the same switch. No page exists for this entity.
- "K-DEVCON": not extracted — the community whose site the account is about, named as the setting with no independent facts about the organization itself stated.
- "Claude Code": not extracted as an update — the account uses it throughout but states nothing about the tool itself beyond the Skills feature, which is recorded on the Agent Skills page instead.
- "Two-track routing": not extracted — the post links to its own earlier article for the technique, and this source describes it only in outline (secondary-citation discipline).
