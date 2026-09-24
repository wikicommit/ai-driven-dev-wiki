---
title: "Why Are Agentic Pull Requests Merged or Rejected? An Empirical Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, code-review, evaluation, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.22534'
    hash: sha256:86242f871d4dd502cdfdf9c5a6346361f31b07c300cce562052319a0eb42cb18
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An MSR '26 empirical study of closed pull requests submitted by AI coding agents, which manually inspects 717 cases to recover why they were merged or rejected and argues that merge and rejection outcomes alone misrepresent agent capability."
  author: ["Sien Reeve O. Peralta", "Fumika Hoshi", "Hironori Washizaki", "Naoyasu Ubayashi", "Inase Kondo", "Yoshiki Higo", "Hiroki Mukai", "Norihiro Yoshida", "Kazuki Kusama", "Hidetake Tanaka", "Youmei Fan"]
  datePublished: "2026"
  abstract: "The study tests the hypothesis that merge and rejection labels do not reliably reflect coding-agent capability without considering review interactions. From 11,048 closed agentic pull requests, refined to 9,799 human-reviewed ones, it manually inspects 717 and finds that only 35.7% of rejected PRs reflect clear agentic failures, while 31.2% were driven by workflow constraints and 33.1% lacked observable decision rationale; among merged PRs, 15.4% required explicit reviewer involvement and 5.5% showed no visible interaction trace."
  keywords: ["AI-assisted development", "agentic pull requests", "human–AI collaboration", "software engineering", "code review"]
  citation: "23rd International Conference on Mining Software Repositories (MSR '26), April 13–14, 2026, Rio de Janeiro, Brazil. https://doi.org/10.1145/3793302.3793575"
---

This short paper, presented at the 23rd International Conference on Mining Software Repositories
(MSR '26) by researchers from Japanese universities including Waseda University, The University of
Osaka and Kyushu University, asks why pull requests submitted by AI coding agents —
[[DefinedTerm/agentic-pull-request]]s — end up merged or rejected. Its starting point is that
agent performance is commonly assessed from merge and rejection outcomes alone, such as merge rates
or approval frequencies, and it hypothesises that those labels do not reliably reflect agent
capability unless review interactions are taken into account.

The authors build on the [[Dataset/aidev]] dataset, restricting it to closed agentic PRs with an
explicit merge or rejection decision in repositories with at least 500 stars (11,048 PRs), then
removing bot-only reviewed submissions to leave 9,799 human-reviewed PRs across five agents —
[[SoftwareApplication/openai-codex]], [[SoftwareApplication/devin]],
[[SoftwareApplication/github-copilot]], [[SoftwareApplication/cursor]] and
[[SoftwareApplication/claude-code]]. From these they draw a stratified sample of 717 PRs (353
rejected, 364 merged) and code each one manually from its interaction artifacts — reviewer
comments, CI outcomes, commit history and workflow actions — with two annotators per PR. Rejected
PRs are coded as agentic failure, non-agentic failure or unknown; merged PRs as a feedback loop
(reviewer feedback followed by agent-only revisions), human intervention (reviewer commits applied
before merge), no feedback loop, or unknown.

## Key Points

- Rejection mostly did not reflect agent failure: of 353 rejected PRs, 126 (35.7%) showed
  observable agentic failure signals such as failing checks or tests, 110 (31.2%) were closed for
  workflow or process reasons such as duplicates, superseded changes, inactivity, test PRs or
  incorrect submission context, and 117 (33.1%) lacked enough evidence to classify — often silent
  closures without comments. Inter-rater agreement was Cohen's κ ≈ 0.90.
- Merged PRs did not uniformly represent autonomous completion: 56 of 364 (15.4%) involved explicit
  reviewer participation, split evenly between feedback loops (28) and reviewer-applied commits
  (28); 288 (79.1%) merged with no observed feedback loop and 20 (5.5%) had ambiguous or
  insufficient interaction evidence. Inter-rater agreement for this coding was Cohen's κ = 1.0.
- Reviewer interventions on merged PRs commonly addressed missing tests, CI configuration issues or
  repository-specific conventions rather than core functionality.
- Interaction patterns differed systematically across agents: Copilot and Devin accounted for 54 of
  the 56 merged PRs with feedback loops or human intervention in the sample, and the authors describe
  them as accounting for most workflow-driven rejections too, whereas OpenAI Codex and Cursor PRs
  were typically merged with minimal interaction. The authors attribute these differences partly to repository practices such as
  stricter CI gating and iterative review norms, so observed outcomes reflect the deployment context
  as much as the agent.
- The authors argue that outcome-based metrics conflate agent capability with repository workflows,
  and that evaluation should incorporate interaction-level evidence and represent uncertainty
  explicitly when that evidence is absent, rather than infer agent performance from outcome labels.

## Notes

The authors note several threats to validity: the operational definitions of agentic failure and
feedback loop leave ambiguity when reviewer intent is implicit; silent closures mean some decision
rationale is unobservable; no effort metrics such as review duration were collected, so the cost of
the 15.4% of human-involved merges is unquantified; and the focus on high-star open-source
repositories and five agents may not generalise to smaller projects, proprietary settings or future
agent systems. As future work they propose using the manually curated labels to automate detection
of workflow-driven closures, reviewer intervention and feedback loops at scale, and building
interaction-aware benchmarks.
