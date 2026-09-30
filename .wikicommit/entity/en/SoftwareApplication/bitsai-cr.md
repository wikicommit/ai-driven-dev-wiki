---
title: "BitsAI-CR"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, llm, data-flywheel]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2501.15134'
    hash: sha256:8cee9ceb37a21ce19689362c1d5ee9b3bbfa63f9f4f85fa4b4dcd878c06ad074
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "ByteDance's internal LLM-based automated code review system, which detects issues in a code diff against a taxonomy of review rules, verifies them with a second model, and improves continuously through a data flywheel."
  applicationCategory: "Code review"
  featureList: "context preparation of code diffs; RuleChecker issue detection over a review-rule taxonomy; ReviewFilter verification; comment aggregation; rule category blocker; data flywheel driven by annotation, user feedback and Outdated Rate"
  author: "ByteDance"
---

BitsAI-CR is an automated code review system built at ByteDance and deployed across its development
teams. Given a code diff from a merge request, it identifies potential issues and produces
structured review feedback: a review category, the specific problematic code location, and an
explanatory comment with a suggested modification. Developers enable it from a settings interface,
which also covers joining reviews and inviting it as a default reviewer. It is described in
[[ScholarlyArticle/bitsai-cr-automated-code-review-via-llm-in-practice]].

## Comment generation

Comments pass through a four-step pipeline. Context preparation partitions each diff by its hunks
to keep context length and token use in check, expands each segment to complete function definitions
within a bounded multiple of the original diff size using tree-sitter, and annotates every line with
whether it was deleted, added or unchanged and its line number. RuleChecker, a fine-tuned LLM that
combines ByteDance's internal code standards with a taxonomy of review rules, then detects issues and
proposes modifications; a rule category blocker lets rules be excluded without retraining the model.
ReviewFilter, a second fine-tuned LLM, takes each comment and returns a yes-or-no decision on whether
to keep it, to screen out hallucinations and factual errors RuleChecker produces; it is trained to
state its conclusion first and its rationale after. Finally, comment aggregation groups similar
comments by cosine similarity of their embeddings and keeps one at random from each group, so that a
merge request with many similar findings does not overwhelm the developer.

Both models are fine-tuned with LoRA from ByteDance's own Doubao-Pro-32K-0828, a choice the paper
attributes to enterprise security requirements and data-privacy considerations. The rule taxonomy
spans 219 review rules across five languages — Go, JavaScript, TypeScript, Python and Java — grouped
into categories under four dimensions: code defects, security vulnerabilities, maintainability and
readability, and performance issues. Once a developer changes the flagged code, the system
re-evaluates it, marks its earlier comments as outdated and can give an "LGTM" approval.

## Data flywheel

The system is improved continuously through a data flywheel. Review rules are mined from two
sources: internal static analysis rules with a high recommendation index and high developer
acceptance, and categories extracted from manual review comments that static analysis does not
cover, such as spelling errors, duplicate code and unclear comments. Training data was built from
120,000 review comments drawn from the internal repository's merge requests and refined with an LLM,
then quality-checked by sampling. After deployment, online performance is evaluated weekly from
three signals: user likes and dislikes, daily manual precision annotation of sampled output, and the
[[DefinedTerm/outdated-rate]] of each rule. Rules are assessed on the two metrics together, and a
rule whose precision is high but whose Outdated Rate stays consistently low is treated as one users
do not accept and may be decommissioned.
