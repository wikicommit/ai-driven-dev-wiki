---
title: "agentic software engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, software-development-process, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/html/2510.19692v2'
    hash: sha256:92e93ca4d7008eac6b0b901390613b8e86cb8c8f7b1bcd4f2bc30e5cf30fa0f5
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An emerging research area and practice concerned with applying agentic AI across software engineering. As of early 2026 its scope is actively contested: several competing framings have been proposed, most focused on coding activities, while others argue for extending it across the whole software engineering lifecycle."
---

Agentic software engineering (agentic SE) is an emerging research area and practice concerned with the application of agentic AI to software engineering — and, reciprocally, with software engineering for agentic AI. It is nascent enough that its scope, values, and vocabulary are all still being argued over rather than settled: [[ScholarlyArticle/toward-agentic-software-engineering-beyond-code]] notes that as of January 2026 most of the framings proposed for it were still under review.

## Usage

Several distinct visions were proposed in parallel. Hoda's paper surveys them and characterises them as sharing one feature: they are primarily focused on and around a single SE activity, coding. Among the proposals it discusses are a new role of *agentic AI Software Engineer*, described by Roychoudhury and colleagues as an autonomous LLM-based coding agent that combines coding, testing, and debugging into a coherent, explainable workflow, and predicting a shift in interest from programming in the large to programming with trust; a *unified software engineering agent* (USEagent) from Applis and colleagues, with capabilities spanning multiple programming tasks and framed as a first draft of a future AI Software Engineer able to be a team member in mixed AI-and-human teams; and *structured agentic software engineering* (SASE) from Hassan and colleagues, a conceptual framework covering two symbiotic modalities — SE for Humans and SE for Agents — organized as a hierarchy of increasing autonomy from manual coding at level 0 through goal-agentic (dubbed Agentic SE, or SE 3.0) up to general domain autonomy at level 5 (SE 5.0), and envisioning dedicated agent command and agent execution environments replacing traditional IDEs.

Against these, Hoda argues for scoping agentic SE as a 'whole of process' discipline covering ethical alignment, requirements engineering, design, development, and operations, rather than as coding acceleration. Her stated reason is historical: every previous SE process model, from Waterfall through Agile, was defined by a whole-of-process approach, and she suggests this may be part of why Scrum, which covered the full lifecycle and project management concerns, considerably outperformed extreme programming.

She also notes an argument from empirical evidence: early studies characterise AI's role as a "personal accelerator" for coding, writing, and documentation tasks while showing limitations in teamwork, coordination, accountability, and culture — the socio-technical concerns a code-centric framing does not reach.

## The SE 3.0 framing

The [[DefinedTerm/structured-agentic-software-engineering]] proposal is set out in full in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], which uses "Agentic Software Engineering" both for the broader era it addresses and as the name of a specific level in its autonomy hierarchy. In that hierarchy, Level 3 — *goal-agentic*, dubbed SE 3.0 — is the stage at which a system maps a technical goal such as "add a caching layer" to a detailed plan of code changes, sitting between Level 2 task-agentic AI-augmented SE (SE 2.0), where a planned code change is mapped to a generated block of code, and Level 4 specialized domain autonomy (SE 4.0), where a broad technical mandate for a specific domain is mapped to a list of concrete technical goals.

The distinction that organizes the hierarchy is between *agency*, defined as the capacity of a system to act and execute plans to achieve a given goal, and *autonomy*, the capacity to self-govern and independently formulate those goals. Hassan and colleagues argue the immediate, industry-defining challenge lies in mastering the SE 3.0 era rather than pursuing full autonomy, since the transition from Level 2 to Level 3 fundamentally shifts the human-computer relationship and introduces complexity in workflow orchestration, trust, and verification.

That paper also draws a line the field's vocabulary often blurs: *agentic coding* describes the one-to-one interaction between a developer and an AI assistant, an augmentation of a solo activity aimed at boosting individual productivity, whereas *agentic software engineering* must support N-to-N collaboration in which many humans and many agents work as a coordinated team. Its stated premise is that software engineering has always been a team sport, so the collective challenges — managing complexity, coordinating across roles, reconciling competing stakeholder needs, and sustaining shared artifacts — demand the acceleration of structured collaboration rather than only individual acceleration.

## Related Terms

Vocabulary for the area is itself contested. Hoda's paper observes that syntactic drift is already visible — agentic AI software engineer versus AI software engineer versus agentic software engineer — and that some discrepancies reflect deeper semantic and philosophical issues. It offers a coverage test as one example of the stakes: a software engineer is more than a coder, so an autonomous coding agent needs to be able to do more than coding before the title "AI software engineer" fits.
