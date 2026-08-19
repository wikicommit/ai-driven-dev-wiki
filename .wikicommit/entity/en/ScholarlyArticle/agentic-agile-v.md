---
title: "Agentic Agile-V: From Vibe Coding to Verified Engineering in Software and Hardware Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, software-development-process, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A paper dated 19 May 2026 arguing that the central problem in agentic AI development is engineering process control rather than prompt engineering. It synthesizes evidence from productivity trials, GitHub-scale studies, and hardware benchmarks, and proposes Agentic Agile-V, a process framework combining an Agile-V lifecycle with a task-level SCOPE-V loop."
  author:
    - "Christopher Koch"
  datePublished: "2026-05-19"
  keywords:
    - "Agentic AI"
    - "software engineering"
    - "Agile-V"
    - "AI-assisted development"
    - "coding agents"
    - "hardware development"
    - "verification"
    - "requirements engineering"
---

This paper argues that current evidence does not support the simple claim that autonomous code generation automatically improves engineering outcomes, and that the bottleneck has therefore shifted from code synthesis to specification quality, execution context, verification, traceability, and controlled iteration. Its central reframing is that the problem is no longer prompt engineering but engineering process control, expressed as a principle: conversation is useful for discovering intent; structured artifacts are required for implementation; evidence is required for acceptance.

The paper is explicitly a bounded evidence synthesis rather than a quantitative meta-analysis. The author states that the evidence base is heterogeneous — randomized trials, GitHub-scale datasets, repository-configuration studies, tool papers, issue-resolution surveys, hardware benchmarks, and process frameworks all measure different outcomes — and that pooling them into a single effect size would obscure rather than clarify the process problem.

Its proposal, [[DefinedTerm/agentic-agile-v]], has two layers: a macro layer combining Agile iteration with V-model verification and audit artifact generation, and a micro layer, the [[DefinedTerm/scope-v]] loop, used to run individual agentic tasks.

## Key Contributions

**A synthesis of mixed evidence.** The paper's reading of the productivity literature is deliberately balanced. It cites a randomized controlled trial with 96 full-time Google engineers reporting an estimated 21 percent reduction in time on a complex enterprise task with AI assistance, against a METR randomized trial with experienced open-source developers finding that AI tools increased task completion time by 19 percent in mature repositories despite developer expectations of speedup, and a 2026 meta-analysis reporting a statistically significant but moderate effect with substantial heterogeneity. Its conclusion is that AI-assisted engineering is a process-sensitive intervention whose value depends on task type, codebase complexity, developer expertise, test coverage, dependency setup, and verification cost.

The evidence on repository configuration files is presented as similarly mixed: one study associated `AGENTS.md` with lower runtime and lower output-token consumption, another found that context files can reduce task success and increase inference cost when they impose unnecessary requirements, and a factorial study found limited evidence that size, position, architecture, or local contradiction alone create reliable adherence effects. The author derives a *minimal-context principle* from this: repository instructions should be short, current, non-contradictory, and tied to executable feedback — and states the correct goal is not maximum context but decision-relevant context.

**Verification debt.** The paper names [[DefinedTerm/verification-debt]] as the condition in which output volume grows faster than verification capacity, producing weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behavior, and increased reviewer burden.

**A conversation-to-contract gate.** The paper argues that long chat histories are not reliable engineering contracts, because they contain superseded assumptions, leave constraints implicit, rarely express acceptance criteria executably, invite agents to overfit to recent turns, and make it hard for reviewers to audit which instruction governed a change. Its operational rule is stated bluntly: do not let an agent implement from a long chat; let it implement from a reviewed brief. The paper specifies when this structure becomes mandatory — when a task affects public APIs, safety, security, performance, hardware behavior, regulated workflows, customer-facing behavior, shared libraries, or persistent data.

**A minimum input artifact model and risk-adaptive acceptance gates.** The paper tabulates seven categories of minimum input an agent should receive — intent and scope, acceptance criteria, architecture context, constraints, execution context, evidence requirement, and risk class — with distinct instantiations for software and for firmware/hardware. It then defines four acceptance levels from exploratory work through routine changes and production changes to high-assurance domains, each with required evidence and a corresponding human gate. The governing rule is that agent output is not accepted because it is plausible; it is accepted because it satisfies evidence appropriate to its risk level.

**Risk-adaptive task workflows.** Separate recommended processes are given for feature development, bug fixing (framed as causal diagnosis rather than feature generation, with the agent asked for hypotheses and a failing regression test before any patch), testing and review (which must happen inside the agent loop rather than after it), and hardware, firmware, and embedded development — where the paper states that compilation is not proof and that simulation, formal checking, hardware-in-the-loop tests, timing analysis, and requirement-to-evidence traceability are essential.

## Notes

The author is explicit about threats to validity: the paper is a synthesis and process proposal rather than a new benchmark, the field is moving quickly, point estimates from 2024 to 2026 may change as models and tools evolve, productivity studies vary by task type and organizational culture, and hardware benchmarks differ in design complexity and verification rigor. The framework is proposed as something that should be validated empirically in future studies across multiple teams, repositories, tools, and hardware domains, and the paper closes with six open research questions to that end.

Its concluding position is that agentic AI is changing software and hardware development but does not make engineering process obsolete, and that the evidence rejects both extremes — agentic coding is neither a toy nor a universal productivity multiplier. The paper's final formulation is that the future of agentic engineering is not [[DefinedTerm/vibe-coding]] at scale, but verified engineering with agents inside the loop.
