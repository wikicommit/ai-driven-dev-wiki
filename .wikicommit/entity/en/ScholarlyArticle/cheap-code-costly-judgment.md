---
title: "Cheap Code, Costly Judgment: A Case Study on Governable Agentic Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, agentic-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01087'
    hash: sha256:8090aa5b3991512f26cd76d8d9f7894401756bc4b97c5ba42d641852854dd0bc
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A 2026 first-person case study of a 12-week agentic development effort, proposing a candidate middle-range theory of governance conversion in which agentic velocity exposes structural failure classes that human judgment converts into durable, machine-actionable governance."
  author: ["James C. Davis", "Paschal C. Amusuo", "Tanmay Singla", "Berk Çakar", "Kirsten A. Davis"]
  datePublished: "2026"
  keywords: ["Agentic Software Engineering", "Case Study"]
---

"Cheap Code, Costly Judgment" is a case study by researchers at Purdue University that asks through what process high-velocity, AI-mediated implementation can be converted into governable software engineering progress. Its design is first-person: over a 12-week period a single expert software engineer — referred to throughout as the Subject, and one of the paper's authors — used frontier AI coding agents to build a document accessibility remediation system for Office and PDF files, under a regulatory deadline. The empirical record comprises 88 contemporaneous, episode-bounded field notes together with the project repository, reported as 18,662 commits and approximately 1.6 million lines of active artifacts; the abstract characterizes the codebase as 420 KLOC of production code and 1.16 MLOC of tests, lints, supporting documentation and agent tooling.

From that record the authors induce a candidate middle-range theory they call [[DefinedTerm/governance-conversion]]: agentic velocity exposes recurring structural failure classes, human architectural-contextual judgment interprets which failures reveal missing governance, and those failures are encoded into the engineering environment so that subsequent agents inherit a narrower action space. The paper positions this as a complement to existing governance-centric accounts rather than a replacement — where prior work derives controls ex ante from obligations known before agents act, this describes an ex-post process of inducing controls from failures that only become visible during agentic work. Its headline framing, and the source of the title, is a pair of dual theses: agentic velocity is sustainable only when governance is relocated into the engineering environment rather than resting on human review, and when implementation becomes abundant the scarce human work shifts toward problem framing, abstraction discovery and architectural judgment.

## Key Points

- Proposes governance conversion — the conversion of observed agentic failure patterns into explicit, durable governance constraining subsequent agent work — as a process that existing accounts of agentic governance do not explain, and states its central claim as "failure → governance".
- Argues that under agentic velocity many necessary controls *cannot* be fully specified before work begins, so ex-ante and ex-post governance are both needed; the authors report applying this case's lessons as ex-ante governance on two subsequent projects (50 KLOC and 36 KLOC) and obtaining faster initial progress, while ex-post governance remained necessary.
- Organizes prior accounts into three process models for agentic software engineering — velocity-centric, oversight-centric and governance-centric (see [[DefinedTerm/agentic-se-process-models]]) — and argues each is insufficient on its own: process resemblance is not control, human attention becomes the throughput bottleneck, and ex-ante obligations do not anticipate every failure.
- Catalogues 41 representative governance mechanisms across ten families, split between agent governance (governance-doc controls, context and dispatch, agent observability, resource mediators, incorporation gates) and product governance (canonical seams, validation and conformance, static and dynamic analyses, provenance and attribution, repair vocabulary).
- Reports that the [[DefinedTerm/governed-engineering-environment]] grew large relative to the product: the support apparatus measured 1.16 MLOC, or 2.75× the production code, comprising static analyses (238 KLOC), dynamic analyses (405 KLOC), agent-referenced documentation (247 KLOC), agent infrastructure (110 KLOC) and tooling (162 KLOC), with 577 project-specific static analyses, over 13,000 C# test methods and roughly 1,500 Python test files.
- States that the Subject inspected almost no agent-produced code, deliberately departing from the oversight-centric model, and that the case tested whether quality could be sustained without ongoing inspection.
- Argues that weak, probabilistic forms of governance saturate at scale and must be mated to deterministic controls — typed enumerations the compiler checks, static and dynamic analyses gating commits — because "at velocity, a low-probability agent harness violation becomes a certainty"; it adds, as a counterintuitive observation, that stronger controls do not always tax velocity and can compound it.
- Proposes that the relevant productivity metric is governed throughput rather than sheer implementation volume — the paper gives "tokenmaxing" as an example of the latter — because commits landed, lines changed and agent tasks completed measure activity, not whether it becomes durable progress.
- Names authority as a moderator: governance conversion requires the person who observes a recurring failure to be able to alter the engineering environment, so in organizations with divided authority the same failure signal may yield only local patches.
- Reports the development cost as approximately $60K USD ($50K of the Subject's grant-funded salary, $6K Google Cloud, $2K inference, $2K Claude subscriptions), with estimates suggesting 9–18M tokens consumed per week.
- Offers three falsifiable propositions for future testing — velocity-exposure, soft-control saturation and governance-conversion — together with two moderators, capability-fit and authority, and is explicit that a single case cannot establish prevalence: the contribution is theory-building, not theory-testing.

## Notes

The study's own stated limitations are substantial and the authors foreground them. It examines a single Subject (N=1) using one agentic toolchain — Anthropic's Claude, accessed entirely through the "Claude for VSCode" chat interface — so the observations may reflect that subject and that toolchain rather than universal properties. The Subject was both practitioner and analyst, which the paper mitigates through contemporaneous field notes, repository evidence, a multi-author critical review, and a validity check in which a second author independently re-coded a stratified sample of 10 incidents (reported agreement: 10/10 on incident class, 6/7 on category, 5/7 on the third coding layer). The Subject's prior experience — sixteen years spanning five as a software engineer, five as a doctoral student and six as a professor, with the engineering experience stated to predate the generative-AI era — is raised as an open question for external validity: whether comparable outcomes are reachable by non-experts, domain specialists or larger teams is not answered here.

The paper also reports, under research ethics, that the sustained agentic development was harmful to the Subject: obsessive tool use degraded attention to personal relationships and prolonged work sessions caused physical strain, with the authors observing that high-velocity agentic tools make extreme work patterns practically sustainable for longer than is healthy. The paper notes that the coded corpus is dominated by engineering reflection (72 of 88 incidents), whose two largest categories — controls (35) and architecture (20) — correspond to the two ways a recurring failure was made governable: detecting it after the fact, or eliminating it by construction.
