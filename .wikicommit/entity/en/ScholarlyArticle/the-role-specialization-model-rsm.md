---
title: "The Role Specialization Model (RSM): Coordinating LLM-Based Tools in Agentic Software Development - An Exploratory Case Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-software-engineering, multi-agent, case-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.12311'
    hash: sha256:da0a1a9ed5fdc70d6195410af825c7ebac9ea2f2a4d43ef18fce2f1b5afd1363
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An exploratory single-case study that proposes the Role Specialization Model (RSM), which gives each of several LLM-based development tools a distinct role under a human orchestrator, and reports how the plan held up while building a small Python desktop application."
  author: ["Carlos Alberto Fernández-y-Fernández", "Jorge R. Aguilar Cisneros"]
  abstract: "The paper presents an exploratory case study in which three LLM-based tools — Antigravity, Gemini CLI and Qwen Code run locally via Ollama — are coordinated according to the Role Specialization Model proposed in the work, while incrementally developing a Python desktop application for climate-data visualization. It asks how such tools can be coordinated, what deviations from the planned role distribution emerge and why, and how the product compares against the ISO/IEC 25010 quality model, and concludes that explicit role coordination can support development but requires deliberate coordination strategies, context management and human verification of agent output."
  keywords: ["agentic software engineering", "SE 3.0", "role specialization", "multi-agent orchestration", "prompt engineering", "vibe coding"]
---

This paper, by authors at the Universidad Tecnológica de la Mixteca and UPAEP in Mexico, proposes the
Role Specialization Model (RSM): a way of coordinating several LLM-based development tools in one
workflow by giving each a distinct domain of responsibility based on its capabilities, so that their
contributions complement one another and overlap is minimised. The authors describe it as the
separation-of-concerns principle applied to assistive tools rather than to code. In the instance
studied, [[SoftwareApplication/google-antigravity]] takes the Architect role (multi-file generation
and iterative refinement), [[SoftwareApplication/gemini-cli]] the Analyst role (bulk processing,
documentation and architectural audit), and Qwen Code, run locally through Ollama for data privacy,
the Specialist role (data validation and unit testing), with a human orchestrator reviewing and
approving outputs and acting as the single integration point.

The study is an exploratory single case, designed and analysed by the developer who carried it out:
one developer built a Python desktop application, Climate Data Visualizer, which loads CSV files of
temperature and humidity records and draws them as interactive line charts, in five phases spread
across the three tools. The paper frames the work within the SE 3.0 view of agentic software
engineering, in which the human acts as architect, mentor and evaluator of agents, drawing on
[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]].

## Key Points

- The Antigravity agent's first, zero-shot design was functional but monolithic, with one class
  handling interface, data loading, validation and chart rendering; a later architectural audit
  through Gemini CLI introduced a separate data-model class, type hints and narrower exception
  handling.
- The main deviation from the plan was that Gemini CLI carried out the refactoring assigned to Qwen
  Code while doing its architectural analysis. The authors attribute this to three factors: no
  explicit scope boundary between the phases, functional overlap between the two tools, and workflow
  inertia, since switching tools would have meant re-establishing the whole project context.
- Generating a test dataset through Gemini CLI took three prompting attempts: the agent first tried
  to invoke tools unavailable in the terminal, and only a prompt with explicit negative constraints
  ("DO NOT run commands. Do NOT use tools.") produced clean output. The paper calls this prompt
  hardening and treats it as a critical technique in this study, while noting that more cases are
  needed to confirm it generalises.
- The Antigravity agent initially ignored a date format given in the prompt; the authors explain this
  after the fact as reasoning on the broader design task displacing a specific formatting
  constraint, which they present as real-world evidence of an effect reported in earlier research.
- A qualitative ISO/IEC 25010 assessment by the first author rated functional suitability,
  maintainability, interaction capability and flexibility high and reliability moderate, the latter
  because of a virtual environment that became corrupted during development.
- The authors conclude that role specialization is a valid design principle for multi-tool LLM
  coordination but needs explicit scope boundaries, and that human verification of agent output
  remains indispensable: most of the developer's productive time went to orchestrating, correcting
  deviations and validating output rather than writing code.

## Notes

The authors support the model through theoretical triangulation — consistency with separation of
concerns, with multi-agent role-specialization frameworks such as [[SoftwareApplication/metagpt]] and
[[SoftwareApplication/chatdev]], and with the SE 3.0 framework — while stating that this cannot
replace empirical replication. Unlike those fully automated multi-agent systems, the RSM coordinates
existing commercial and open-source tools through a human developer.

Stated threats to validity include observer bias from a single researcher-developer, a single
project and toolset, a qualitative rather than measured quality assessment, and a single
unreplicated run of probabilistic agents. Two of the three tools share the same underlying Gemini
model, which the authors say may partly explain the role overlap; they propose testing a
heterogeneous toolset and adding a fourth, evaluator agent following the
[[DefinedTerm/llm-as-a-judge]] paradigm to take over part of the human's audit role.
