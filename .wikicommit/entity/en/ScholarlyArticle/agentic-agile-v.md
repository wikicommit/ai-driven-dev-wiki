---
title: "Agentic Agile-V: From Vibe Coding to Verified Engineering in Software and Hardware Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, verification, software-process, hardware]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An evidence synthesis and process proposal arguing that the bottleneck in agentic engineering has moved from prompting to process control, and setting out Agentic Agile-V — an Agile-V lifecycle backbone paired with a task-level SCOPE-V loop, risk-adaptive acceptance gates and evidence bundles for accepting agent-generated work."
  author: ["Christopher Koch"]
  datePublished: "2026"
  keywords: ["agentic AI", "software process", "Agile-V", "verification", "hardware development", "requirements engineering"]
---

This paper starts from a deliberately balanced reading of the evidence on agentic coding: the author holds that current findings support neither the claim that autonomous code generation automatically improves engineering outcomes nor the view that it fails. Drawing on productivity trials, GitHub-scale adoption studies, repository-configuration research, issue-resolution benchmarks and hardware verification benchmarks, he argues that results diverge sharply by context — acceleration in some enterprise settings, slowdown in mature open-source work, a moderate but heterogeneous average effect — and that persistent failures cluster in repository setup, dependency handling, permission gating and hardware verification.

From that reading the author draws a single diagnosis: the central problem is no longer prompt engineering but engineering process control. Agentic AI can generate plausible engineering artifacts faster than humans can inspect them, so the bottleneck shifts from code synthesis to specification quality, execution context, verification, traceability and controlled iteration. He names the resulting failure mode [[DefinedTerm/verification-debt]] — the gap that accumulates when output volume grows faster than the capacity to verify it — and states that it can become operational or physical risk in hardware and embedded work.

The proposal, [[DefinedTerm/agentic-agile-v]], is a two-layer process framework: an Agile-V lifecycle backbone in which each increment stays traceable from requirements through verification and audit evidence, and a task-level SCOPE-V loop — Specify, Constrain, Orchestrate, Prove, Evolve, Verify — for running individual agentic tasks. Around these sit a conversation-to-contract gate separating exploratory dialogue from implementation, a taxonomy of minimum input artifacts, risk-adaptive acceptance gates, and an evidence-bundle model. The organising principle the author states is that conversation is useful for discovering intent, structured artifacts are required for implementation, and evidence is required for acceptance.

## Key Points

- The paper's stated method is a bounded evidence synthesis rather than a quantitative meta-analysis, on the reasoning that pooling randomized trials, GitHub-scale datasets, configuration studies, benchmarks and process frameworks into one effect size would obscure the process problem rather than clarify it.
- It relays contrasting productivity results — a randomized trial of full-time engineers reporting roughly a 21% reduction in time on a complex enterprise task, a separate trial of experienced open-source developers reporting a 19% increase in completion time in mature repositories despite expectations of speedup, and a meta-analysis reporting a statistically significant but moderate effect with substantial heterogeneity.
- Long chat histories are argued to be unreliable engineering contracts: they carry superseded assumptions, leave constraints implicit, rarely state executable acceptance criteria, invite the agent to overfit to recent turns, and leave reviewers unable to audit which instruction governed a change.
- The operational rule the author derives is to not let an agent implement from a long chat, but from a reviewed brief — with structure made mandatory when a task touches public APIs, safety, security, performance, hardware behaviour, regulated workflows, customer-facing behaviour, shared libraries or persistent data.
- Evidence on repository instruction files is presented as genuinely mixed: one study associates them with lower runtime and lower output-token consumption, another finds context files can reduce task success and increase cost when they impose unnecessary or mismatched requirements, and a factorial study finds limited evidence that file size, position or structure alone produce reliable adherence effects. The author's conclusion is a minimal-context principle — instructions should be short, current, non-contradictory and tied to executable feedback.
- Code context alone is held to be insufficient; agents are argued to need execution context: build commands, dependency setup, test commands, environment variables, toolchain information, simulator access and clear acceptance criteria.
- Four risk levels are defined with escalating evidence requirements, from exploratory throwaway work needing a smoke test or manual run, no production credentials, and optional review, through routine and production tiers, to high-assurance work requiring traceable requirements, independent tests, simulation, formal or hardware-in-the-loop evidence as applicable, and explicit sign-off. The stated acceptance rule is that agent output is accepted not because it is plausible but because it satisfies evidence appropriate to its risk level.
- For production and high-assurance tasks the paper specifies a minimum evidence bundle: the task brief and requirement identifiers, the agent's plan and affected files, executed commands and test results, a diff summary with residual risks, a trace from acceptance criteria to tests, the reviewer's decision, and a rollback path.
- Hardware and firmware are argued to raise the bar because compilation is not proof: incorrect pin mappings, register values, timing assumptions, bus behaviour, reset handling or memory layout can fail in ways that are costly or unsafe, so simulation, formal checking, hardware-in-the-loop tests and requirement-to-evidence traceability are treated as essential.
- The author relays hardware benchmark results as especially cautionary, including a benchmark reporting low pass rates on real-world Verilog generation and zero percent pass@1 on system-level tasks for the models evaluated.
- Permission gating is placed inside the testing problem rather than beside it: the paper relays a stress-test finding that permission-gate assumptions may fail under ambiguous state-changing scenarios, particularly where an equivalent effect can be achieved through file edits instead of shell commands.
- Its advice to tool builders is to optimise for evidence generation as well as code generation — structured brief editors, dependency setup capture, test discovery, traceability, risk classification, permission gates, sandboxed execution, review summaries and exportable evidence bundles.

## Notes

The author is explicit that the paper is a synthesis and process proposal rather than a new benchmark, that the field is moving quickly enough that point estimates may not hold, and that productivity studies vary by task type, developer experience, codebase maturity, tool generation and organisational culture. He states the framework itself should be validated empirically in future work across multiple teams, repositories, tools and hardware domains, and sets out a research agenda that includes whether structured execution briefs actually improve agent success over conversational prompts, what the minimum useful content of repository instructions is, and which task classes the framework helps rather than slows through overhead.

Agile-V, the lifecycle half of the framework, is described as a compliance-ready approach combining Agile iteration with V-model verification and audit-artifact generation, which the paper cites as having been proposed to address a lack of built-in task-level verification and regulatory traceability in machine-speed AI-assisted engineering, with a case study demonstrating feasibility in a hardware-in-the-loop setting; this paper generalises it to agentic software, firmware and hardware development by specifying inputs, task workflows and acceptance gates. The closing position is that agentic AI does not eliminate engineering discipline but increases the value of requirements, constraints, traceability, independent verification and human approval — summarised as a future that is not [[DefinedTerm/vibe-coding]] at scale but verified engineering with agents inside the loop.
