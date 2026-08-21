---
title: "Rethinking Code Review in the Age of AI: A Vision for Agentic Code Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, multi-agent, human-in-the-loop, pull-requests]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A vision paper proposing a five-stage, agent-orchestrated code review workflow with human-controlled quality gates, in which reviewers move from manual inspectors to supervisory operators of agents."
  author: ["Hüseyin Özgür Kamalı", "Erdem Tuna", "Vahid Haratian", "Eray Tüzün"]
  datePublished: "2026-06-08"
  abstract: "Reviews the historical evolution of code review, identifies challenges in traditional pull-request review, and proposes an AI-powered workflow spanning PR Creation, PR Augmentation, Reviewer Selection, AI-Assisted Code Review and PR Retrospective, with humans retained at key decision points."
  keywords: ["Code Review", "AI-Driven Software Engineering", "Large Language Models", "Agentic AI", "Multi-Agent Systems", "Pull Requests", "Automated Code Review", "Human-in-the-Loop"]
  citation: ""
---

This vision paper, by authors from Ankara University, Microsoft, and Bilkent University, argues that code review is the point where AI-assisted development's costs land. Its framing claim is that AI does not only help produce code — it rebounds on the review process that code must pass through. It cites coding assistants accelerating individual coding tasks by more than 50%, alongside coordination time for integration growing faster than individual output and AI-generated contributions requiring more review iterations than human-written ones. Its conclusion from this is that "code review is no longer only a productivity bottleneck. It is the primary control surface for the quality and accountability of AI-produced code."

Its diagnosis of existing AI support is fragmentation: tools address isolated tasks such as reviewer recommendation, PR description generation, or comment suggestion, and those stage-level advances do not compose on their own — a helpful review comment still depends on a PR whose rationale was written down, and reviewer matching relies on behavioural context reaching the reviewer. The paper's response is to treat review effectiveness as an outcome of the full lifecycle and to propose a framework that carries context across stage boundaries.

The paper is a vision and research-agenda contribution rather than an evaluated system: it proposes the framework, identifies open challenges, and sets out a research agenda; it does not report an implementation or empirical results for the framework itself.

## Key Contributions

**A five-era history of review practice** — Ad Hoc, Formal Inspection, Lightweight Peer Review, Integrated Code Review, and Automation-Assisted — organised around how practitioners actually conducted review rather than around tooling.

**A five-stage agentic framework**, described under [[DefinedTerm/agentic-code-review]], with explicit human-in-the-loop quality gates at each transition:

- **PR Creation** — a PR Detail Generation Agent writes title and description from the diff; an Issue Linking Agent establishes traceability links or creates an issue where none fits; an Automated Code Review Agent inspects the draft diff; a Fix Suggestion Agent proposes concrete patches with explicit statements of what they change and leave intact; the author then revises interactively in natural language before formally submitting.
- **PR Augmentation** — four agents run concurrently on the diff plus linked issue context: an Alignment Analysis Agent classifying requirement fulfilment as exact, tangling, missing, or missing-and-tangling; a Bug Proneness Analysis Agent scoring risk from historical defect density, code churn and hotspot files; a Runtime Analysis Agent executing code in a sandbox to collect logs and execution traces; and an Impact Analysis Agent evaluating cross-module dependencies. A Summary Generation Agent then synthesises their outputs into a structured summary of verifiable claims.
- **Reviewer Selection** — traditional reviewer-recommendation tooling ranks candidates on expertise, historical review experience, current workload queue and familiarity with the changes; the author picks from the list and sends invitations.
- **AI-Assisted Code Review** — a PR Review Agent acts as the central natural-language interface, delegating to an Explanation Agent, an Automated PR Review Agent, a Fix Suggestion Agent, a Toxicity Measurement Agent and a Usefulness Measurement Agent, all interacting through the [[DefinedTerm/diff-map]].
- **PR Retrospective** — review summaries capture implementation and review context as repository memory, and review metrics are computed to feed continuous process improvement.

**A catalogue of open challenges** for responsible adoption: bias and inaccuracy in LLM predictions, limited generalisation across projects, accumulated error in multi-agent pipelines, agent evaluation, transparency, accountability, privacy, automation bias, knowledge-sharing deterioration, and hidden economic costs.

## Notes

Two of the paper's self-identified risks are notable because they cut against its own design. On **accumulated error**, it works through a concrete cascade: a PR Detail Generation Agent misreading an authorisation change as routine business logic produces an inaccurate description, which leads Reviewer Selection to assign a backend rather than a security expert, so that a security defect goes unexamined. Its mitigation is the human gates themselves, which it describes as "natural firewalls against error accumulation" — the author verifying the generated description breaks the chain early.

On **automation bias**, it then argues that assuming those human gates are inherently robust is itself "a fundamental flaw." Its worked case is an author waving through an incorrect issue link, which then propagates flawed analysis downstream into reviewer assignment. It cites an observation that developers ultimately retain only 52% of AI-generated suggestions despite easy initial acceptance, and argues explicit quality indicators are needed rather than assumed reliance.

A third risk concerns what review is *for* beyond defect detection. The paper notes that knowledge transfer and team awareness are equally critical outcomes, and that routing explanation through an agent risks displacing "implicit mentoring" — citing a finding that 27.41% of pull requests in open-source projects contain embedded educational guidance. Its suggested mitigation is a mandatory "PR Critique" checkpoint requiring a human reviewer to contribute architectural insight or mentorship notes before merge is unblocked.
