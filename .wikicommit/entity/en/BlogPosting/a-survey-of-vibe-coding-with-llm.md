---
title: "基于大语言模型的 Vibe Coding 综述"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, ai-assisted-programming, coding-agents]
sources:
  - type: url
    url: 'https://baoyu.io/blog/a-survey-of-vibe-coding-with-llm'
    hash: sha256:55f4b02fb630800f3d09661467157048d6f52edca9864fa28067ab84f108fddc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A Chinese-language walkthrough of an academic survey of vibe coding, relaying its three-party definition, its five development models and its list of open challenges — and adding one argument of the author's own: that the recurring mistake is managing a coding agent as though it were a tool."
  author: "宝玉"
  datePublished: "2025-10-27"
---

This post is mostly a reading of someone else's work. It walks through an academic survey of vibe coding in six numbered sections, relaying the survey's definition of the practice as a three-party relationship — a human developer who has stopped being the direct author of code and become the one who states intent, sets direction and judges quality; a software project that is no longer just a codebase but a context space of code, data, documentation and domain knowledge; and a coding agent that does the writing, editing and debugging within the constraints both of them impose. It also relays the survey's five development models and its account of why the practice is harder than it looks.

The one part that is the author's own is a short argument about how practitioners get it wrong. The claim is that most people treat a coding agent as a tool — a smarter autocomplete, a better Stack Overflow — when it is in fact an agent: something you assign work to, give memory and permissions to, and then have to manage and review. Applying tool habits to what is really an employee produces two opposite failure modes, and the author argues both are common: blind acceptance, where syntactically clean output is committed on vibes and the failure is later blamed on model hallucination when the real omission was code review and automated testing; and excessive distrust, where every generated line is rewritten by hand, which costs as much in its own way. The post compares this to a poorly performing engineering manager who either abandons a report entirely or micromanages them, and prescribes the middle path: checkpoints at the decisive moments, automated verification, and delegation in between — the way a new hire is onboarded with process around them rather than given production access on day one.

## Key Points

- The post's own argument: the tool-versus-agent distinction is the thing practitioners get wrong, and the remedy is management discipline — checkpoints at key nodes and automated verification, with genuine delegation between them — rather than either blind acceptance or blanket distrust.
- It relays the survey's finding that experienced developers using advanced AI tools took 19% *longer* to complete tasks, presenting it as the paper's headline problem rather than as the author's own measurement.
- It relays the survey's explanation for that gap as three things other than raw model capability: systematic [[DefinedTerm/context-engineering]], the design of feedback loops, and infrastructure — sandboxes to execute agent code safely, interfaces for fluent interaction and project-information sharing, and platforms to test and deploy what the agent writes.
- It relays the survey's five development models by name and gloss: Unconstrained Automation (hands off entirely, fast and risky, suited to throwaway prototypes, likened to Rapid Application Development), Iterative Conversational Collaboration (pair-programming-like, quality assured but demanding of attention), Planning-Driven (specifications, rule files and implementation plans written first, likened to waterfall but more flexible), Test-Driven (tests define correctness and the agent writes code to pass them, machine verification replacing human review), and Context-Enhanced (not a standalone workflow but an augmentation, via retrieval-augmented generation and codebase indexing, combinable with the other four).
- It relays the survey's account of the developer's changing role as five activities: expressing intent and engineering prompts, managing context, debugging at the system level rather than line by line, supervising architecture while the agent handles implementation detail, and validating quality and governing the agent's permissions and code provenance. The author's own compression of this is that the value shifts from writing good code to using AI well to write good code.
- It relays the survey's four challenge areas: code reliability and security, where an agent may reproduce bugs and vulnerabilities learned from training data and manual review cannot keep pace with generated volume; supervision at scale, where existing management and audit methods are said to be outdated; the human factor, including how much trust in AI is appropriate; and an education gap, with computing curricula largely not teaching how to direct, design workflows for, or assess the risks of AI-written code.

## Context

The post is explicitly a reading of an academic survey, and it links to that paper rather than claiming its findings as original — so almost every figure and framework in it is the paper's, and only the tool-versus-agent section is presented in the author's own voice. The survey itself is held separately by this wiki as [[ScholarlyArticle/a-survey-of-vibe-coding]], which is the better source for anything the paper states; this page records what a practitioner took from it and what they added.

The author writes for a Chinese-language audience and frames the piece as notable partly for its existence — that vibe coding has become a subject one can write academic papers about is itself part of the post's point.
