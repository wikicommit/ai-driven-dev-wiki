---
title: "Assistance to Autonomy: A Systematic Literature Review of Agentic AI across the Software Development Life Cycle"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-ai, sdlc, systematic-literature-review, multi-agent-systems, industrial-adoption]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.15245'
    hash: sha256:93a6c8bfd18429d67e8c2a2a4e4865999e141411cc9f548e35302e716c6d558d
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A systematic literature review of 92 primary studies on agentic AI across the software development life cycle, identifying output verifiability as the principle connecting phase maturity, architecture and industrial mitigation strategies."
  author: ["Spyridon Alvanakis Apostolou", "Jan Bosch", "Helena Holmström Olsson"]
  datePublished: "2026"
  keywords: ["agentic AI", "autonomous systems", "LLM agents", "software development life cycle", "systematic literature review"]
---

A systematic literature review by researchers at Chalmers University of Technology, Eindhoven University of Technology and Malmö University, asking where agentic AI has actually reached maturity in software product development, which architectural patterns dominate, and what limitations industrial deployments run into. The authors frame the field as moving from assistance to autonomy: where generative AI was integrated into the lifecycle as a reactive assistant responding to explicit prompts, agentic systems plan, reason, use tools, self-refine and execute multi-step workflows with minimal human intervention, and can therefore span entire lifecycle phases rather than individual developer actions.

The review follows Kitchenham and Charters guidelines across four databases — IEEE, the ACM Digital Library, SpringerLink and Scopus — narrowing 1,609 raw records to 92 manually verified primary studies. Because the candidate volume made manual filtering impractical, the authors built and validated a domain-agnostic six-step multi-agent screening pipeline as a second contribution: role-playing Assistant and Evaluator agents classify each record independently, disagreements trigger a structured argumentative dialogue of up to three rounds, and unresolved conflicts default to inclusion so as to minimise false negatives. Different models are deliberately used for the two agents in every double-agent step, so that agreement reflects independent reasoning paths.

The synthesis's central claim is that output verifiability, rather than model capability, is what currently gates industrial agentic adoption — and that the same principle is visible in where agents are deployed, how they are architected, and how their failures are contained.

## Key Points

- Of the 92 primary studies, only 13 were developed and evaluated in an industrial context; the remaining 79 are academic proofs-of-concept evaluated on benchmarks or in controlled experimental settings.
- Agentic maturity is concentrated in post-development phases: Maintenance (20 studies), Testing & QA (18), cross-cutting work spanning multiple phases (15), Deployment & Operations (14) and Coding & Implementation (12) dominate, while Requirements Analysis (7), Project Management (3) and Design & Architecture (3) are least explored.
- The authors attribute that concentration to verifiability: post-development tasks produce outputs that can be checked through objective, executable feedback such as test results, compiler outputs, fault-localisation traces and log signals, which gives self-refinement loops a concrete state to improve against without human evaluation.
- Coding & Implementation had no industrial studies at all in the set, which the authors read not as absent research effort but as a sign that industrial adoption there requires agents to work on large legacy codebases with undocumented constraints and evolving requirements that controlled benchmarks do not capture.
- The predominant architecture across the surveyed studies is multi-agent role specialisation, most commonly [[DefinedTerm/planner-executor-reviewer]] with an Orchestrator agent managing sub-process flow; the authors report this pattern appearing across publications in all lifecycle phases.
- Structured, typed inter-agent communication — via JSON or LangGraph state graphs — frequently replaced free-text handoffs with formally typed state transitions.
- Memory and retrieval form a second structural axis, with retrieval-augmented generation as a baseline mechanism; industrial studies favour structurally grounded retrieval over flat vector search, including a hybrid vector-graph knowledge system validated in production at Apple and a Zero-Shot Dependency Mapping Knowledge Graph used as a shared memory layer across agents.
- The most commonly reported limitations are non-deterministic behaviour, information overload, hallucinations and scalability; the predominant coping mechanism across both academic and industrial studies is iterative self-correction driven by an evaluation method's results.
- Industrial mitigations across every challenge category converge on confining agent actions to verifiable, bounded spaces — predefined atomic action vocabularies, structured outputs, and stage-specific pass/fail tests that reject intermediate errors rather than propagating them.
- The authors argue that extending agentic integration into earlier lifecycle phases is first and foremost a problem of designing phase-appropriate feedback mechanisms, not of improving model capability.

## Notes

The review positions itself against several recent secondary studies by organising its findings around a cross-cutting principle rather than around agent capabilities or method categories in isolation. It contrasts its own scope with reviews covering LLM-based multi-agent systems, broader agent-centric surveys, method-category classifications, and practitioner-interview work.

The authors report validating their screening pipeline's reliability by manually re-checking 100 excluded publications, 50 from each agent-based stage. A single false negative was found, from the relevance-selection phase; extrapolating that rate across the 669 excluded records suggests roughly seven missed relevant publications in total, and the authors argue the true number is likely lower since the sole miss came from the phase operating on the smaller candidate set.

Three threats to validity are stated. Relevance decisions depend on predefined prompts and specific models, so prompt inaccuracies or future model changes may introduce systematic variability. Grey literature was deliberately excluded in favour of peer-reviewed work, which the authors acknowledge entails information loss, since industrial agentic practices frequently appear in grey literature before formal publication. Many industrial studies rely on proprietary data and organisation-specific workflows, limiting how far their architectures and mitigation strategies transfer.

The complete multi-agent pipeline, its Assistant and Evaluator prompts, and the raw datasets from all four database queries are published at <https://doi.org/10.5281/zenodo.20670298> . The study was funded by Software Center.
