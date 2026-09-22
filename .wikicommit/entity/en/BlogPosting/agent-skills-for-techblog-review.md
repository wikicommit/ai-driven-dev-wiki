---
title: "Claude Code Agent Skillsを活用したTECH BLOGレビュー ── AIで推進するレビュー自動化"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, coding-tools, technical-writing, review-automation]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/agent-skills-for-techblog-review'
    hash: sha256:b7ab59cc842b9ca743dbf674dacebb9dfbec6ef08ca5e2e87ed8d758b0019b71
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "ZOZO's Developer Engagement team describes encoding its tech-blog editorial review rules as a Claude Code skill, built by mining three years of past review comments and curating them by hand into a rule file the skill reads."
  author: "wiroha"
  datePublished: "2026-02-17"
  publisher: "ZOZO"
---

This post is an account of turning an editorial review process into an agent skill. The subject under review is prose rather than code, which makes it an unusual neighbour to this wiki's accounts of [[DefinedTerm/agentic-code-review]]: an agent is put in the reviewer's role here too, but what it is given to apply is the team's own editorial knowledge, written down as an explicit rule file.

The stated problem is concentration rather than volume in the abstract — two people review roughly a hundred articles a year, which makes the work dependent on particular individuals, slow, and prone to missed points that turn into repeated correction rounds. A textlint check in GitHub Actions already covered mechanical proofreading, so the gap the team set out to close was the set of review perspectives that rule-based linting cannot express.

## Key Points

- The skill is deliberately split in two: a short `SKILL.md` that fixes the procedure and the output format, and a `rules.md` that carries the review rules themselves. The author identifies the rule file as the substantive part.
- The rules were not written from scratch. Claude Code was pointed at three years of past review comments in the repository, collected through the GitHub CLI, and asked to draft rules from them; the drafts were then refined by hand. The author presents the accumulated review history as an asset that could be mined.
- `SKILL.md` restricts the skill's tools to reading files and fetching URLs, the latter so the skill can check the article's links for breakage as part of the review.
- The skill is placed in the blog-writing repository, where the author reports it becoming enabled automatically as a project skill. Reviewers can also point it at an article they do not have locally by giving a URL, which it retrieves through the GitHub CLI.
- The output format is pinned in the skill definition — a line number, the perspective, a summary of the fix, and a diff block showing before and after — and the skill is told to report only actual problems, omitting "no issues" entries.
- The author reports the skill catching a stray leading space at the start of a line as an example of a perspective the rules do not cover, and singles out its detection of a wrong filename as the surprising case, on the grounds that it went beyond widely known service names.
- Coverage was estimated rather than measured directly: classifying the review comments on thirty past pull requests against the rule file suggested roughly 75% could be covered. The remaining quarter is characterized as judgments needing context — compressing or restructuring text, whether phrasing is appropriate, where explanation should be added.
- Findings are treated as suggestions and are not applied automatically. The author gives a worked reason: the skill correctly identified a wrong URL but proposed the English-language documentation in place of the Japanese, which a person had to correct.
- The rules are applied with human judgment rather than uniformly. The post gives the example of colloquial phrasing, which the rules discourage but which the team keeps in event-report articles where it conveys the writer's feeling better.
- Humans also remain responsible for checking that confidential or inferable information has not made it into an article — a category the author does not attempt to delegate.
- The author notes that the example sentences in the rule file were altered by hand from the generated drafts so that no specific article could be identified from them.

## Context

The post's argument for choosing a skill over the alternatives is about the operating model rather than capability: browser-based assistants require copying the article text back and forth, the same mechanism can be used by writers for self-review as well as by the review team, the rules can live in GitHub where anyone can propose a change by pull request, and starting from optional use allows precision to be improved before anything becomes automatic. The team explicitly preferred this to having Claude Code GitHub Actions or Devin post automated comments on pull requests, wanting to start from optional use and raise accuracy gradually.

The author's claims about effect are stated carefully and are mostly about the reviewer's attention rather than throughput: time spent devising corrections is reduced, review perspectives became less dependent on an individual's experience and skill, and delegating detail frees attention for structure and readability. The coverage figure is presented as an estimate derived from classifying past comments, not as a measurement of the skill in use, and adoption by writers is described as recent with self-review not yet required.

Stated intentions include feeding review results back into the rules, possibly supporting tools other than Claude Code — the author notes that having the rules in a separate file makes them transferable — and, if there is interest, open-sourcing the skill. None of these are reported as done. For the underlying mechanism this post applies, see [[DefinedTerm/agent-skills]] and [[SoftwareApplication/claude-code]].
