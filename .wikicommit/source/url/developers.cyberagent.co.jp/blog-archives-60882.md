---
source:
  type: url
  url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
  hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
  license:

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 7463
generated_pages:
  - .wikicommit/entity/en/BlogPosting/redesigning-code-review-for-the-ai-era.md
  - .wikicommit/entity/en/SoftwareApplication/greptile.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code-action.md
  - .wikicommit/entity/en/DefinedTerm/testing-skyscraper.md
  - .wikicommit/entity/en/DefinedTerm/ai-final-gatekeeper.md
  - .wikicommit/entity/en/DefinedTerm/review-bottleneck.md
failed_pages: []
---

## Summary

A CyberAgent Developers Blog post, written for the 2025 Advent Calendar, describing how one team redesigned its code review flow after adopting Cursor, Claude Code and Codex roughly doubled the team's commit count and correspondingly raised review load. The measures described are unified monorepo guidelines written to hold only team-specific rules, a shift-left testing strategy the team calls the "testing skyscraper" that raised its test-to-code line ratio from 78.6% to 112.6%, standardized Claude skills and commands for PR creation and CI fixing, and a three-tool AI review setup using GitHub Copilot, Greptile and Claude Code Action. It also describes making AI rather than a human the final gatekeeper, running a post-approval check that returns a merge-OK, merge-with-concerns or merge-not-recommended verdict.
