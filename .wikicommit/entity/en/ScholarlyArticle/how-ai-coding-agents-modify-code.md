---
title: "How AI Coding Agents Modify Code: A Large-Scale Study of GitHub Pull Requests"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, software-engineering, pull-requests]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.17581'
    hash: sha256:fab1e4e59caae8e9f728ba5dbdf4368a5508c43ea3648bf70408360c4292511c
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An empirical comparison of 24,014 merged agent-authored and 5,081 merged human-authored GitHub pull requests from the AIDev dataset, examining how the two differ in code-change structure and in how closely their descriptions match their diffs."
  author: ["Daniel Ogenrwot", "John Businge"]
  abstract: "Using the MSR 2026 Mining Challenge version of the AIDev dataset, the paper compares merged agentic and human pull requests on additions, deletions, commits and files touched, and evaluates the consistency between pull-request descriptions and their diffs using lexical and semantic similarity. Agentic pull requests differ substantially from human ones in commit count and moderately in files touched and deleted lines, and show slightly higher description-to-diff similarity across all measures."
  keywords: ["AI coding agents", "Agentic AI", "LLMs", "Pull Requests", "Code patches"]
---

This paper asks how pull requests submitted by an [[DefinedTerm/ai-coding-agent]] differ from those written by people — both in how they change code and in how accurately their descriptions reflect those changes. The authors argue that although tools such as [[SoftwareApplication/github-copilot]], [[SoftwareApplication/openai-codex]], [[SoftwareApplication/claude-code]], [[SoftwareApplication/cursor]] and [[SoftwareApplication/devin]] can now autonomously generate code and submit pull requests, large-scale analyses of agent-authored pull requests remain scarce, and without them it is hard to judge their reliability, their effect on maintainability or how clearly they communicate during review.

The study uses the version of [[Dataset/aidev]] provided for the MSR 2026 Mining Challenge, retrieved on 1 November 2025, which the paper describes as containing 932,791 agentic and 6,618 human pull requests across 116,211 repositories. Because the human pull requests in that dataset lack commit-level information, the authors reconstructed their commits, modified files and diffs through the GitHub REST API, then kept only merged pull requests with valid patches. The resulting analysis set is 24,014 agentic pull requests (440,295 commits) and 5,081 human pull requests (23,242 commits).

Structural differences were tested with the Mann–Whitney U test and sized with Cliff's delta. Description-to-diff alignment was measured lexically, with TF–IDF cosine similarity and Okapi BM25, and semantically, with cosine similarity between CodeBERT and GraphCodeBERT embeddings of the description and the cleaned diff. The authors' conclusion is that agentic pull requests are structurally distinct from human ones yet generally coherent in how they describe their edits.

## Key Points

- The largest difference between agentic and human pull requests is the number of commits (Cliff's δ = 0.5429, a large effect); files touched (0.4487) and deletions (0.4462) differ with medium effects, while additions (0.2836) and total line changes (0.3158) differ only with small effects. All differences are statistically significant (p ≤ 0.001).
- Human pull requests show the largest and most variable code changes; agentic ones tend to introduce smaller, more localized edits and to touch fewer files across fewer commits.
- Agentic pull requests are not uniform: Claude Code and OpenAI Codex show wider variability, while Devin, Cursor and especially Copilot produce consistently small, localized changes.
- The authors' takeaway is that what most distinguishes agentic pull requests is not how many lines they change but how they organize and distribute changes across commits and files.
- Lexical similarity between descriptions and diffs clusters near zero for both groups, while semantic similarity clusters between 0.9 and 1.0, suggesting both kinds of description capture the meaning of their patches even when the wording differs.
- Agentic pull requests score slightly higher on average than human ones across all four similarity measures — for example a mean CodeBERT similarity of 0.9356 against 0.9285, and a mean GraphCodeBERT similarity of 0.8254 against 0.7815 — with the clearest differences in the semantic measures.
- Okapi BM25 proved unbounded and highly variable, especially for agentic pull requests, so the authors treat it only as a coarse lexical indicator rather than a calibrated similarity measure.

## Notes

The authors suggest that review and triage could use commit count and files touched, rather than lines of code alone, as early indicators of an agentic pull request's scope, and that deletion-heavy or wide-scope agentic pull requests may warrant closer review — while noting that further work is needed to link these structural patterns to concrete risks. They also suggest that the consistently high description-to-diff alignment may support tasks such as release-note generation, changelog construction and reviewer routing, and that automated checks could flag unusually low alignment.

Their stated threats to validity are that the results depend on the completeness of AIDev and of the reconstructed human-PR commit data, which GitHub API rate limits, deleted repositories, rewritten histories and truncated diffs may affect; that the structural metrics approximate scope but not intent or correctness, and similarity measures alignment but not code quality or reviewer understanding; and that findings generalize to the open-source GitHub projects and agent versions represented in AIDev, and may differ in private or industrial settings or as agents evolve.

The paper was published at the 23rd International Conference on Mining Software Repositories (MSR '26), April 13–14, 2026, in Rio de Janeiro, under a Creative Commons Attribution 4.0 license (DOI 10.1145/3793302.3793603). The version extracted here is arXiv:2601.17581v3 [cs.SE], stamped 6 April 2026. Both authors are at the University of Nevada, Las Vegas, and a replication package with curated data and analysis scripts is published.
