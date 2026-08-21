---
title: "Agentic AI in the Software Development Lifecycle: Architecture, Empirical Evidence, and the Reshaping of Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, ai-assisted-programming, software-development-process]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2604.26275'
    hash: sha256:0e0cd343d8397c662d30a146c709b8466c7ec253a14926f8898a8dd5d2a5a412
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A single-author arXiv survey submitted 29 April 2026, arguing that agentic systems have moved the granularity of AI-assisted development from the line or function to the repository, feature, or algorithm. It proposes a six-layer reference architecture, contrasts the traditional SDLC with an Agentic SDLC, and consolidates performance, productivity, and labor-market evidence."
  author:
    - "Happy Bhati"
  datePublished: "2026-04-29"
---

"Agentic AI in the Software Development Lifecycle" is a survey paper submitted to arXiv on 29 April 2026 by Happy Bhati, filed under Software Engineering (cs.SE) and described in its metadata as a 9-page survey with 5 figures and 2 tables. It is published under a CC BY 4.0 licence with the DOI <https://doi.org/10.48550/arXiv.2604.26275> .

Its premise is that large language models capable of multi-step reasoning, tool use, and long-horizon planning have produced a qualitative shift in software engineering. The paper draws the contrast in terms of granularity: where earlier code-completion tools such as [[SoftwareApplication/github-copilot]] operated at the level of a line or a function, the survey states that modern agentic systems — naming [[SoftwareApplication/claude-code]], OpenAI Codex CLI, Google Jules, Devin, [[SoftwareApplication/openhands]], SWE-agent, MetaGPT, ChatDev, and DeepMind's AlphaEvolve — operate at the level of a repository, a feature, or an algorithm.

The survey positions itself as a synthesis rather than as new empirical work, drawing together material the abstract attributes to [[Organization/anthropic]], [[Organization/openai]], Google DeepMind, Microsoft Research, Princeton, Stanford, and the broader academic community.

## Key Contributions

The abstract states four contributions:

- **A six-layer reference architecture** for agentic software engineering systems. The abstract names the architecture but does not enumerate its layers.
- **A contrast between the traditional Software Development Lifecycle and an emerging Agentic SDLC (A-SDLC).**
- **A consolidation of empirical evidence** along three axes: performance, reported as a rise from 1.96% to 78.4% on SWE-bench Verified between October 2023 and April 2026 (see [[Dataset/swe-bench]]); productivity, reported as 13.6%–55.8% time savings across controlled studies; and labor-market impact, reported as 49% of jobs sampled by Anthropic in 2026 having seen AI used for at least a quarter of their tasks.
- **A reframing of the field's central question.** The paper argues that the central object of inquiry has shifted from code generation to delegated execution under human supervision.

It closes by identifying five open problems the author argues will determine whether the agentic transition is net-positive for the discipline: evaluation, governance, technical debt, skill redistribution, and the economics of attention.

## Notes

The material available for this page is the arXiv abstract page rather than the paper's full text, so the layers of the proposed architecture, the studies behind the productivity range, and the argument connecting the five open problems are not recorded here.

The paper's framing — delegated execution under human supervision as the object of study, rather than code generation — converges with the practitioner vocabulary this wiki tracks under [[DefinedTerm/agentic-engineering]] and [[DefinedTerm/vibe-engineering]], both of which locate the discipline in supervision and review rather than in prompting. Its use of a single benchmark trajectory as the headline performance measure sits against the cautions recorded on [[Dataset/swe-bench]] about contamination and about test-passing as a proxy for merge-readiness.
