---
title: "AI IDE Rules"
type: "schema:DefinedTerm"
lang: en
aliases: ["Rules", "Steering"]
tags: [agents, coding-tools, context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Textual instructions kept in files inside a project that an AI IDE automatically injects into the model's context, so that project-specific constraints, conventions and architectural guidelines persist across interactions instead of being retyped each time."
---

Rules, in the context of an [[DefinedTerm/ai-ide]], are textual instructions or directives written by
developers to constrain and guide the behaviour of the LLM-driven assistant. They are kept in rule
files at the project's root or in a configuration directory, and the IDE retrieves the relevant content
and injects it into the model's context window when the developer interacts with the assistant. The
mechanism amounts to persistent prompt engineering: what would otherwise be retyped every session is
stated once and applied automatically.

Their purpose is to align the IDE's output with a specific project — architectural constraints, coding
styles, library preferences, development workflow. A rule file is typically written in natural language,
usually Markdown. The location differs by tool: `.cursor/rules/` for [[SoftwareApplication/cursor]],
`.windsurf/rules/` for [[SoftwareApplication/windsurf]], `.trae/rules/` for
[[SoftwareApplication/trae]], `.qoder/rules/` for [[SoftwareApplication/qoder]], and
`.kiro/steering/` for [[SoftwareApplication/kiro]], which calls its version of the mechanism Steering
and generates three files there by default. Cursor and Windsurf both began with single-file formats
(`.cursorrules`, `.windsurfrules`) that were later superseded by directory-based management.

## Usage

[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] mined 7,310 rules from 83 open-source
projects and grouped them into five primary categories: **Architecture & Design** (technology stack
selections, design principles and patterns, system architecture, design references and constraints);
**Code Implementation** (framework usage, code style conventions, performance optimization, language
features, error and exception handling, business logic); **Development Workflow & Project Management**
(workflow conventions, project documentation, directory structure, environment configuration, version
control, dependency management); **Quality Assurance** (testing strategy, security practices, code
quality standards, logging standards, code review); and **AI Collaboration Specifications** (AI
behavior and decision strategies, AI output content guidelines, AI context management, AI tool usage).
That last category acts as meta-control over the model's own behaviour, interaction style and tool use,
as distinct from rules about the code.

What that study found in practice is a gap between what developers say matters and what their rule
files contain. Architectural and context-management rules are rated most important — System
Architecture at 4.25 out of 5, AI Context Management at 4.17 — while accounting for only 2.67% and
1.76% of mined rules. Workflow Conventions, the largest category in the
repositories at 9.29%, falls in the lowest importance quartile; Testing Strategy, the second largest at
8.76%, rates mid-pack. The study's explanation is a consequence of
how rules get written: 71.72% of surveyed developers generate rules with AI and then refine them, and
48.48% add rules only when the AI makes a mistake, so the files accumulate around whatever causes
visible friction during generation rather than around what a developer would nominate as important.

Most projects keep this centralised: 43.4% have exactly one rule file and 26.5% have two, while
projects with more than twenty are rare. Rule counts cluster in the dozens to low hundreds.

Rules are not static. In that study, 55 of 83 projects had rule files that changed, and adding is the
dominant operation — typically 50–80% of changes in a category. Six drivers were identified from commit
evidence: **Expansion** (extending the agent's scope to new modules or adopting new IDE features),
**Context Enrichment** (supplying implicit project background to bridge the model's context gap),
**Synchronization** (keeping rules consistent with a changing codebase), **Refinement** (tightening
phrasing without changing intent), **Correction** (adding negative constraints after observing
hallucinations or bad output), and **Pruning** (deleting obsolete rules). Mining evidence and developer
self-report disagree sharply on their relative weight: the commits are dominated by Expansion and
Context Enrichment, while 77.78% of surveyed developers name Correction as a primary trigger — a gap
the study reads as negativity bias. Even when correcting, developers mostly add: 68.75% of corrections
were performed as additions rather than edits to the existing text.

## When It Applies

Rules apply where a project has conventions an assistant would otherwise have to be told each session,
and where those conventions can be stated in natural language a model will follow. The study's
compliance measurement bears directly on where that second condition holds: updating a
rule raised average artifact compliance by 22.99%, but the effect concentrated in concrete, statically
checkable constraints — Dependency Management gained 64.82% and Testing Strategy 52.73%, while Project
Documentation gained 6.25% and System Architecture 3.33%.

Two failure modes follow from that asymmetry. The first is spending limited context window on
formatting and syntax, which conventional linters enforce more reliably; the study recommends
delegating those and reserving the window for domain-specific business logic and architectural
patterns. The second is stating non-functional requirements abstractly. Rules about performance
optimization and security practices change rarely, and when they do change they are usually deleted —
65.22% and 61.90% of their changes respectively — which the study explains by these being inherently
abstract requirements that are hard to state precisely in a prompt, where vague-but-strict constraints
can trigger over-defensive model behaviour or hallucinated false positives. Its advice is to convert
them into concrete code patterns, or to rely on static analysis instead.

A third failure mode is accumulation. Because corrections arrive as additions, rule files grow long and
can come to contain contradictions; the study recommends periodically consolidating and pruning.
Compliance also decays: it peaks at the commit that introduces a rule and falls back toward 65% over
the following commits, which the study attributes to rule staleness and to the context window growing
more complex as business code and conversation accumulate.

The evidence base is one mixed-methods study, and two of its own caveats matter here. Under external
validity it notes that its projects are predominantly TypeScript web development, built — per its own
dataset overview — by solo developers or teams of one to three. Separately, under internal validity, it
records that the compliance figures rest on 160 rules filtered to those an automated script could
check, which leaves them dominated by statically verifiable categories.

## Related Terms

- [[DefinedTerm/ai-ide]] — the class of tool this mechanism belongs to
- [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] — the study behind the taxonomy,
  evolution drivers and compliance figures above
- [[DefinedTerm/agents-md]] — a comparable context-file convention, not tied to one IDE
- [[DefinedTerm/context-engineering]] — the broader practice this mechanism is one instrument of
- [[DefinedTerm/prompt-engineering]] — what rules amount to a persistent form of
