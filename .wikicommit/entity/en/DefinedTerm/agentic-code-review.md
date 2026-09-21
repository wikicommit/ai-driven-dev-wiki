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
  - type: url
    url: 'https://github.com/AsyncFuncAI/AsyncReview'
    hash: sha256:fe75d41284e3b16f547100098c199269e82a0d07655fa5e6c55e1989662c322e
  - type: url
    url: 'https://github.com/alibaba/open-code-review'
    hash: sha256:b9e25b582bd7eea6db72fdab8f395f2c2a3a3d52275e5bb2239736035a7c6c88
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Code review in which an AI agent acts as a reviewer. The term is used two ways across sources: as the name of an era of a project's review practice in which agent reviewers participate alongside humans, and as the name of a repository-grounded task in which a reviewer agent explores a codebase and returns a decision plus a diagnosis. Vendor documentation attaches the adjective to the specific capabilities that let a review reach beyond the diff, and two open-source tools build for the repository-grounded task while disagreeing over how much of the resulting loop the agent should run."
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

## Tool Usage

Two open-source projects in this wiki's sources build for the repository-grounded task the second
sense above defines, and they disagree about how much of the resulting loop the agent should be
trusted to run. Only one of the two adopts the label: AsyncReview calls itself agentic code review
outright, while Open Code Review never uses the adjective, describing itself as an AI-powered code
review CLI with a hybrid architecture. It is recorded here because its argument is about this
capability, not because it claims the term.

[[SoftwareApplication/asyncreview]] takes the maximal reading. Its README describes going beyond
simple diff analysis by autonomously exploring the repository, fetching context and verifying
findings in a sandbox before answering, in a recursive loop of reasoning, generating Python code,
executing it, and observing the result. Its stated contrast with other review tools is a list of
four pairings: limited context against reading any file in the repository, static analysis that
guesses how code works against executing search queries and verification scripts, inventing library
methods against citing existing file paths and lines, and one-shot generation against iterating
before answering. The third of those names hallucination as the failure the approach is meant to
remove, which is the same claim the task sense makes about grounding.

[[SoftwareApplication/open-code-review]] accepts the same premise — its agent reads full file
contents, searches the codebase and inspects other changed files — and argues against a different
thing: not repository access, but leaving the review process to the model. It argues it from the
record of general-purpose agents doing this job. Its README states three
problems it attributes to using one for code review: on larger changesets the agent cuts corners,
reviewing only some files and missing others; reported issues drift off the actual code location;
and quality fluctuates with minor prompt variations. Its stated diagnosis is that a purely
language-driven architecture lacks hard constraints on the review process, and its response is to
take four steps away from the model — which files to review, how to bundle related files into
isolated sub-agent units, which rules match which file, and a pair of external modules for comment
positioning and reflection — leaving the agent only dynamic decisions and dynamic context
retrieval. Against a general-purpose agent on the same model it reports higher precision and F1 at
roughly a ninth of the tokens, with lower recall as a deliberate trade-off, in a comparison it ran
itself on [[Dataset/aacr-bench]].

Both accounts are their own projects' self-descriptions, and the second's figures are its own
reported results from a comparison it ran. What they establish jointly is not a settled answer but that the
term's task sense has become contested territory: the shared premise is that review needs
repository access, and the live question is how much of the resulting loop should be the model's to
run.

## Related Terms

- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/review-bottleneck]]
- [[DefinedTerm/code-review-as-runtime-monitoring]]
- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/generate-review-revise-loop]]
- [[DefinedTerm/closed-loop-ai-review]]
