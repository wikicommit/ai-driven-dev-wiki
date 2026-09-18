---
title: "From Prompt to Process: a Process Taxonomy and Comparative Assessment of Frameworks Supporting AI Software Development Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A comparative study of six frameworks that add process to AI coding agents, proposing a six-dimension taxonomy with a scoring rubric and finding a structural trade-off between process depth and portability across agents."
  author: ["Sanderson Oliveira de Macedo"]
  datePublished: "2026-06-04"
  keywords: ["AI software development", "AI agents", "specification", "software engineering", "agentic frameworks", "comparative study of frameworks"]
---

This paper argues that recent surveys map agents and large language models for software engineering
but leave out the operational frameworks that turn those capabilities into process. It takes as its
unit of analysis not the agent itself but the layer that runs over one: a structured set of artifacts,
commands, roles, templates, workflows or policies that organises whoever uses the agent. Its
hypothesis is that the value of these frameworks lies less in automating the writing of code than in
how they structure the cognitive and operational work around the agent — moving the question from
"which model writes better code?" to "which process lets humans and agents keep context, traceability
and control over changes?".

Frameworks were selected by a directed, qualitative search of primary sources rather than an
exhaustive systematic review, under a four-part functional inclusion criterion: the artifact must
support the development cycle through specification, planning, context, roles, workflows or
validation rather than only generating code; it must be aimed at someone who already operates a
development agent; it must not be the agent, IDE or closed platform itself; and it must not be a
general-purpose SDK for building agent systems. A second traction filter required at least one
thousand GitHub stars and a push within the previous six months. Six frameworks passed:
[[SoftwareApplication/github-spec-kit]], [[SoftwareApplication/openspec]],
[[SoftwareApplication/bmad]], [[SoftwareApplication/get-shit-done]],
[[SoftwareApplication/spec-kitty]] and [[SoftwareApplication/reversa]].

The paper's central contribution is the [[DefinedTerm/six-dimension-process-taxonomy]] — specification,
context, roles, execution, validation and portability — accompanied by a three-point rubric that turns
it from a descriptive vocabulary into a replicable instrument. It applies the instrument to the six
selected frameworks and, to test generality, to one deliberately excluded for low traction,
[[SoftwareApplication/spec-flow]].

## Key Points

- The six dimensions are proposed because they recur, under different names, across all six analysed
  frameworks; portability across agents is treated as a first-class comparative criterion rather than
  an installation detail, which the paper argues existing product comparisons do not do.
- Under the rubric (0 = absent or incipient, 1 = partial, 2 = strong or central), no framework scores
  strongly on all six dimensions. The paper reads this as a structural trade-off: the most portable
  frameworks sacrifice roles and validation, the one with the deepest process reduces portability and
  execution, and the one most focused on context scores zero on roles, validation and portability.
- Specification is the most saturated dimension, with almost all frameworks scoring 2, so it
  discriminates between them least. Roles and validation are the most polarised and therefore the most
  informative.
- Applying the taxonomy to an out-of-sample framework excluded for low traction produced the most
  complete profile of any case examined. The paper draws two conclusions from that contrast: the
  instrument generalises beyond its sample, and adoption and process completeness are orthogonal, so
  the traction filter selects the most adopted frameworks rather than the most complete ones.
- Across the frameworks that already adopt some process, the paper identifies convergence in
  mechanism: the isolated prompt loses centrality and persistent artifacts, work contracts,
  traceability and human review become the means of reducing ambiguity and coordinating agents.
- Five recurring patterns are named — converting the prompt into a contract, treating context as an
  engineering asset, validation beyond the final test, the tension between autonomy and governance,
  and the emergence of a supply chain of installable commands, skills and templates that carries
  supply-chain risk.
- Recurring risks the paper maps are drift between specification and code, excessive trust in
  generated artifacts, fragility of community extensions, platform dependence, and the absence of
  benchmarks for the complete process.
- The proposed research agenda calls for process-oriented benchmarks measuring intermediate artifact
  quality rather than only final solutions, context and grounding metrics, permission governance and
  security, automatic detection of specification drift, and longitudinal studies of real teams.

## Notes

The paper positions itself against two bodies of prior work. Academic reviews of agents in software
engineering are categorised by cognitive components or by life-cycle task, which the author argues
adopts a different lens from the engineering-process one used here; commercial comparisons of
spec-driven development tools already cover several of the same frameworks, but as product content —
without an explicit taxonomy, without an auditable selection criterion, and in one case published by
one of the tools being compared.

The author records several limitations directly. The directed search prioritises depth over
exhaustiveness, so low-traction or very recent frameworks may be missing. Traction measured by stars
and activity is called an imperfect and unstable indicator, and the figures are a May 2026 snapshot.
Part of the primary-source base is grey literature with possible promotional bias, which the paper
says it mitigates by confronting claims against the formal literature. The dimensional scoring was
done by a single rater with no second independent coder and no inter-rater reliability reported, which
the paper names as a threat to the rubric's objectivity and leaves as future work. A conflict of
interest is declared: one of the six included frameworks is authored by the author of the study, who
states it receives the same critical analysis and record of risks as the others. Productivity claims
from the primary sources are treated qualitatively rather than reproduced as measurements.

The paper closes by warning that without an empirical basis these frameworks risk merely
institutionalising [[DefinedTerm/vibe-coding]] with an extra layer of terminology, and that with
rigorous evaluation they could instead become a layer of software engineering made of processes
readable by humans and executable by agents. The author states that Grammarly tools were used to improve textual
agreement and a Claude model to support text structuring and translation into English, and that the
author reviewed and edited the content and takes full responsibility for it.
