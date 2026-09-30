---
source:
  type: url
  url: 'https://tech-lab.sios.jp/archives/53091'
  hash: sha256:ad600fed8b9b62a03a62c07d1ed68806968ad524260b789712fdd5d404cb3432
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 6456
generated_pages:
  - .wikicommit/entity/en/BlogPosting/splitting-one-greedy-ai-reviewer-into-three-agents-in-claude-code.md
  - .wikicommit/entity/en/DefinedTerm/review-loop-non-convergence.md
failed_pages: []
---

## Summary

A SIOS Tech Lab blog post (24 June 2026) describing how the author, after a single Claude Code review agent failed to give useful feedback on seminar slides, split slide review into three sub-agents defined under .claude/agents/, each with a different perspective, starting point and input: harsh-review (scoring from 0 to expose empty wording), logic-reviewer (scoring from 100 and flagging only five kinds of logical breakdown), and audience-reaction (role-playing a persona with only the in-scope slides). It recounts how repeatedly applying the harsh reviewer to an outline made it grow from 685 to 772 lines while its score fell from 47 to 44, and argues for splitting by perspective, inverting starting points and restricting inputs, with a human deciding which findings to adopt.

## Generation Notes

"Ryu (龍ちゃん)": privacy — the post's author, a living individual who is not a public figure; entity-policy.md rules out pages about living individuals and about private individuals.
