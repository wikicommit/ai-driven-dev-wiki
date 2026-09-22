---
source:
  type: url
  url: 'https://techblog.zozo.com/entry/agent-skills-for-techblog-review'
  hash: sha256:b7ab59cc842b9ca743dbf674dacebb9dfbec6ef08ca5e2e87ed8d758b0019b71
  license:

schema:
status: generated
last_generated_at: "2026-09-22"
extracted_tokens: 11912
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agent-skills-for-techblog-review.md
failed_pages: []
---

## Summary

ZOZO's Developer Engagement block describes encoding its TECH BLOG editorial review rules as a Claude Code Agent Skill, built from three years of past review comments harvested from GitHub and then curated by hand into a `rules.md` the skill reads. The skill is a project skill in the blog repository, pairing a short `SKILL.md` that fixes the output format with the rule file that carries the substance. Classifying 30 past PRs' review comments against those rules suggested roughly 75% coverage, with the remaining quarter -- compression, appropriateness of phrasing, added explanation -- judged context-dependent and left to human reviewers, and all AI findings treated as suggestions rather than applied automatically.

## Generation Notes

- "wiroha": excluded (privacy) -- the post's author, named as a member of the Developer Engagement block; entity-policy.md rules out a page about a real individual who is not a public figure. No existing page.
- "ZOZO": not extracted -- appears as the publishing employer and the operator of the blog under discussion, with no independent facts about the organization itself stated; Organization.md's granularity treats that as an incidental mention.
- "textlint": not extracted -- named once as an existing GitHub Actions check the team already runs, with no independent facts about the tool stated; SoftwareApplication.md's granularity treats that as an incidental mention.
