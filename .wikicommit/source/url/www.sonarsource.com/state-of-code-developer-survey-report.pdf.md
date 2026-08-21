---
source:
  type: url
  url: 'https://www.sonarsource.com/state-of-code-developer-survey-report.pdf'
  hash: sha256:3d43f704cf1e52ecf4045d4342479248b68f557da49a051f79fb79b036967a0d

schema:
status: partial
last_generated_at: "2026-08-21"
extracted_tokens: 18647
generated_pages:
  - .wikicommit/entity/en/Report/state-of-code-developer-survey-2026.md
  - .wikicommit/entity/en/DefinedTerm/verification-bottleneck.md
  - .wikicommit/entity/en/Organization/sonar.md
  - .wikicommit/entity/en/DefinedTerm/indirect-prompt-injection.md
failed_pages: []
---

## Summary

Sonar's survey of 1,149 professional developers, fielded throughout October 2025, whose central claim is that the explosion in AI-generated code has not yet produced the expected productivity gains and has instead created a verification bottleneck downstream of generation — now a page in its own right. Its most useful figures for this wiki are the gap between distrust and practice (96% do not fully trust AI code is functionally correct, but only 48% always check before committing), the reason for the review cost (61% agree AI "often produces code that looks correct but isn't reliable"), and the finding that toil did not shrink but changed composition, holding at 23–25% of the work week regardless of AI use frequency. Every figure is the vendor's own and framed as such on the generated pages.

Excluded as unrelated to the configured theme:
- "SonarQube" (theme_mismatch): the publisher's own product, presented in the report's closing chapter as the verification layer for AI code. This is vendor product marketing, which the configured theme excludes explicitly; the report's SonarQube-users comparison is recorded on the Sonar organisation page as a first-party claim instead of becoming a product page.

Re-checked on 2026-08-21 (content unchanged, cache hit) as a dedicated coverage comparison. Eight uncovered findings were added. To the report page: the adoption-versus-effectiveness gaps that lead the report to call AI a better "explainer" and "prototyper" than "maintainer" or "refactorer"; the spread of AI use by criticality of the work up to 58% on mission-critical services; the benefit-side baseline (35% average productivity boost, 54% higher job satisfaction, 82% coding faster); the company-size divide in which SMBs report both larger gains and up to 11 points higher negative impacts; the rarity of distinct process for AI-generated code (18% of enterprises, 12% of SMBs, 10% of mid-market); the inversion of concerns by experience, where developers with over twenty years report fewer concerns than juniors; the company-size split in agent effectiveness, with SMBs rating agents markedly more effective for vibe coding; and the report's first-party causal claim, from its own LLM personality research, that models inherently tend toward verbosity and unnecessary technical debt. Two further findings went to term pages: the projected rise in the perceived value of deterministic rules-based review from 60% to 68% over two years, and the enterprise-versus-SMB split in concern about direct and indirect prompt injection. The status stays `partial` because of the theme exclusion above.
