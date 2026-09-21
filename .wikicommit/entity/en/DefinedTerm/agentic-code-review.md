---
title: "Agentic Code Review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agents]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2607.13196'
    hash: sha256:1635571abac83780f1fe27a5b0def652bdd5addba148b5a72857e7b29a0c3c98
  - type: url
    url: 'https://arxiv.org/pdf/2607.06065'
    hash: sha256:cb4fdaa0aecd873bb17c7946eae064e6fc7d82ab88b72e25a69a45f06154657d
  - type: url
    url: 'https://docs.github.com/en/copilot/concepts/agents/code-review'
    hash: sha256:5288bbf7e00b1255000a7c40ad0d7129e795426d5c72d9dc46584d8c359c2ce8
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Code review in which an AI agent acts as a reviewer. The term is used two ways across sources: as the name of an era of a project's review practice in which agent reviewers participate alongside humans, and as the name of a repository-grounded task in which a reviewer agent explores a codebase and returns a decision plus a diagnosis. Vendor documentation also attaches the adjective to the specific capabilities that let a review reach beyond the diff."
---

Agentic code review names code review in which an AI agent occupies the reviewer's role. Two sources this wiki holds use the term at different levels, and neither is a special case of the other: one names a phase of a project's review practice, the other names a task definition for a single review.

[[ScholarlyArticle/from-human-centric-to-agentic-code-review]] uses it for the most recent of three code review eras a project may pass through. That study distinguishes human-centric review, in which review is primarily a human process; LLM-assisted review; and agentic code review, in which AI agent reviewers participate in the review process alongside human reviewers and large language model reviewers. Those eras are the framework the study works in rather than categories it derives; what it identifies empirically is three adoption practices by which projects transition across them, from 1.02 million reviewed pull requests in 207 GitHub projects.

[[ScholarlyArticle/swe-review]] instead formalizes it as a repository-grounded task. A review instance supplies a repository checkout at the relevant commit, a natural-language issue, and a candidate pull request with its diff, title and body — withholding the golden patch and the hidden test results. The reviewer may browse files, search code, inspect dependencies and execute commands before submitting a report with two fields: a binary decision to approve or request changes, and, where it requests changes, a diagnosis that identifies concrete defects, cites code locations where possible, and proposes actionable fixes for a downstream revision agent.

## Usage

In the era sense, the term marks a phase of practice rather than a particular tool. Projects are characterized by which of three adoption practices they follow into that era — Gradual AI Adoption, Rapid LLM Adoption, or Rapid AI Agent Adoption — and review discussions are modelled as sequences of interactions between human, LLM and agent reviewers.

What that study reports about the era is a split: agent-involved collaboration patterns, especially reviews initiated by AI agents or involving multiple AI agents, are associated with faster review decisions under two of those adoption practices, but the authors state that the efficiency gains do not translate into better review quality.

In the task sense, the defining move is that the reviewer acts in the repository rather than reading a diff in isolation. That is also where the measured advantage lies: [[ScholarlyArticle/swe-review]] reports agentic review beating single-turn fixed-context review on both decision accuracy and resolve rate after revision, with the largest margins on tasks requiring non-local repository reasoning — which is the result one would expect if exploration is what the added capability buys. In that framing review is not a terminal commentary step but the pivot of a [[DefinedTerm/generate-review-revise-loop]].

The two usages pull in different directions on what counts as evidence. The era account is observational, drawn from what projects on GitHub actually did, and is careful that faster is not better. The task account is constructed and executable, scoring a review by whether the patch resolves the issue afterwards. A claim about agentic code review is worth checking against which of the two a source means.

## Vendor Usage

A third use of the adjective comes from the vendor side, and it is worth recording because it names something more specific than either sense above. GitHub's documentation for [[SoftwareApplication/github-copilot-code-review]] has a section headed "Agentic capabilities for Copilot code review", and what it puts under that heading is two particular abilities rather than the review as a whole: full project context gathering, which analyses the entire repository to better understand the context of a change, and the ability to pass suggestions to the Copilot cloud agent, which creates a new pull request with the suggested fixes applied. The same document also uses the adjective of a review outright, saying that certain pull requests are eligible for agentic review, so the narrower reading is the emphasis of one section rather than a definition the document holds to throughout.

Where that emphasis lands is roughly where the task sense above draws its line — what makes a review agentic is acting on the repository rather than reading a diff alone. The documentation attaches a cost to those capabilities that neither research account has reason to: they run on GitHub Actions, so by default a review that reaches beyond the diff consumes GitHub Actions minutes in addition to model usage. That default is not the only arrangement — the documentation notes that self-hosted runners consume no Actions minutes, and that an organization which has disabled GitHub-hosted runners can use self-hosted ones, with reviews falling back to a more limited form if it does not. Reviews are still produced when the capabilities are unavailable, just without what they add. This is one vendor's documentation of its own product rather than an independent characterization of the term, and it is recorded here as such.

## Related Terms
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/review-bottleneck]]
- [[DefinedTerm/code-review-as-runtime-monitoring]]
- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/generate-review-revise-loop]]
- [[DefinedTerm/closed-loop-ai-review]]
