---
title: "Agentic AI in the Software Development Lifecycle: Architecture, Empirical Evidence, and the Reshaping of Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, software-engineering, software-process, surveys, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.26275'
    hash: sha256:aa482f682e7c0b75e0722b3f300a2b51efed9d71f5422587078df55ec3fd8595
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A single-author preprint synthesizing industrial and academic work on agentic coding systems, proposing a six-layer reference architecture and an Agentic SDLC, compiling evidence on benchmark performance, productivity and labor-market effects, and naming five open problems for the field."
  author: ["Happy Bhati"]
  abstract: "The paper argues that LLMs capable of multi-step reasoning, tool use and long-horizon planning have produced a qualitative shift in software engineering: where code-completion tools operated at the granularity of a line or function, agentic systems operate at the granularity of a repository, a feature or an algorithm. It proposes a six-layer reference architecture, contrasts the traditional SDLC with an Agentic SDLC (A-SDLC), consolidates evidence on performance, productivity and labor-market impact, argues that the central object of inquiry has shifted from code generation to delegated execution under human supervision, and identifies five open problems."
  keywords: ["agentic AI", "software development lifecycle", "reference architecture", "developer productivity", "human–AI collaboration"]
---

This preprint, written by an author at Northeastern University and marked as under review, is a
synthesis rather than an original study. It contrasts the in-editor completion tools that followed
the 2021 release of GitHub Copilot — where, in the paper's framing, the human remained the engineer
and the model was an autocomplete with judgment — with agentic systems such as
[[SoftwareApplication/claude-code]], OpenAI's Codex CLI, [[SoftwareApplication/google-jules]],
[[SoftwareApplication/devin]], [[SoftwareApplication/openhands]] and
[[SoftwareApplication/swe-agent]], which read a repository, plan changes across files, run commands
and tests, observe failures and deliver a committed change. Drawing on published material from
industrial labs and academic groups, it offers four contributions: a synthesis of the main lines of
work, a six-layer reference architecture, a contrast between the traditional software development
lifecycle and an Agentic SDLC, and a consolidation of empirical evidence together with an agenda of
open problems.

The paper's central argument is that code generation is the wrong frame for the transition. The
right frame, it proposes, is delegated execution under human supervision, and it expects the
long-run winners to be those who invest earliest in the process, governance and skills that
delegation requires. It describes its overall reading as cautiously optimistic.

## Key Points

- The proposed reference architecture has six layers, with dependency running upward and feedback
  flowing downward: L0 the foundation model; L1 reasoning, memory and self-reflection; L2 the
  [[DefinedTerm/agent-computer-interface]]; L3 tools and environment; L4 orchestration, where
  single-agent loops and role-specialized multi-agent systems coexist; and L5 governance and safety.
  The author argues that L5 is currently the least mature layer and is becoming the bottleneck on
  enterprise deployment.
- Following industry frameworks, the paper distinguishes an Agentic SDLC, in which an orchestrator
  coordinates specialized sub-agents while a human supervises at intent, review and approval gates,
  from an SDLC merely accelerated by AI assistants. It emphasizes three structural differences: the
  unit of work shrinks to tasks an agent completes in minutes to hours; the developer's role shifts
  from producing to orchestrating, reviewing and directing; and behavioral metrics such as agent
  acceptance rate, escalation quality and supervision burden displace, without entirely replacing,
  cycle time and defect rate.
- It argues that agentic systems break the classical SDLC's assumption that behavior is fully
  specified at build time, because both the systems and the development process become stochastic:
  the same task may take a different path on different runs.
- Its compiled [[Dataset/swe-bench-verified]] timeline, drawn from vendor reports and papers, rises
  from 1.96% in October 2023 to 78.4% in April 2026, while non-agentic retrieval-based systems
  plateau near 20%; the author reads this as the gain being dominated by scaffolding rather than raw
  model capability.
- On productivity it groups evidence into controlled experiments, which report the largest effects,
  field experiments and longitudinal team studies, and cautions that gains are unevenly distributed
  and that AI-assisted code may increase long-term technical debt.
- It observes convergence across the major programs: all expose a CLI- or IDE-resident agent with
  shell, file and test access, human approval at high-impact actions, some form of long-term memory,
  parallel or multi-agent execution for non-trivial tasks, and a story about safety and audit.
- The five open problems it names are evaluation beyond SWE-bench (long-horizon delegation,
  collaboration with reviewers, faithfulness to intent, absence of reward hacking); governance, safety
  and audit, including making human–agent responsibility mapping verifiable by auditors; the
  technical-debt hypothesis, since agents are biased toward producing more code and local fixes; skill
  redistribution, with experienced engineers capturing compounding gains while newcomers underperform;
  and the economics of attention, since if agents produce many plausible patches per hour, human
  review becomes the rate-limiting resource.

## Notes

The paper's quantitative claims are compilations of other work — vendor announcements, model cards,
Anthropic Economic Index reports, and productivity studies on GitHub Copilot — rather than new
measurements, and several of its figures (including its table of approximate SWE-bench Verified
scores per program) are marked by the author as approximate. It also places major systems on a
capability–autonomy plane and contrasts the strategic posture of the major industrial programs. The
version extracted here is arXiv:2604.26275v1.
