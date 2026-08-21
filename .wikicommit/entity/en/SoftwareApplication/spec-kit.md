---
title: "Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [ai-assisted-programming, spec-driven-development]
sources:
  - type: url
    url: 'https://github.github.com/spec-kit/concepts/sdd.html'
    hash: sha256:8eb0247a43c5afbc5b75f447d9f90202cdd390cf55fa951daad26cb7eedbad2f
  - type: url
    url: 'https://github.github.com/spec-kit/'
    hash: sha256:7832ccf3affc33ff8c13ecc134677f09460cca0e97dea84295948bc90a2336ee
  - type: url
    url: 'https://github.com/github/spec-kit/blob/main/docs/reference/workflows.md'
    hash: sha256:9edc007a729f332382682e209b40662bb963919d8d88fe0d101594ce7adad161
  - type: url
    url: 'https://arxiv.org/pdf/2604.05278'
    hash: sha256:a9436d2944579fdac4ded1e91308767999c4eba452e3d149c066ac95095750ba
  - type: url
    url: 'https://arxiv.org/pdf/2606.30689'
    hash: sha256:a18183a689a7171dd459d93148005c0a497297442e4c68cb3cd91953c958f93b
review_status: reviewed
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A specification-driven development toolkit, whose documentation defines and sets out the process of [[DefinedTerm/spec-driven-development]]. Its own documentation describes it more broadly as an extensible, intent-driven harness that guides any coding agent across a software development lifecycle or another business process."
  applicationCategory: "Specification-driven development toolkit"
  operatingSystem: "Windows, macOS, Linux"
---

Spec Kit is a specification-driven development toolkit. Its documentation defines [[DefinedTerm/spec-driven-development]] — a process in which specifications become executable and directly generate working implementations — and sets out the core philosophy, development phases, and experimental goals of that approach.

Its own project site frames the tool more broadly than SDD alone, describing Spec Kit as "an extensible, intent-driven harness that pushes any coding agent beyond code, guiding it across your SDLC or any business process," and offering SDD as the process that ships ready to use rather than as the only one the tool supports. The tagline it leads with — "Spec-Driven Development or your own process — step by step or as an automated workflow" — states the same split: a default process, an automation layer, and the option to replace the process entirely.

## Overview

The core process Spec Kit ships with is **Spec → Plan → Tasks → Implement**, and its site describes each phase as producing a Markdown artifact that feeds the next, so that the coding agent receives structured context instead of ad-hoc prompts. Rich templates, quality checklists, and cross-artifact analysis are described as coming out of the box.

Spec Kit deliberately does not prescribe how teams preserve or mutate the `spec.md`, `plan.md`, and `tasks.md` files after requirements change; its documentation treats that as a separate topic, covered under spec persistence models and under workflows for evolving specs in existing projects.

The tool is installed and driven through a CLI named `specify` — its site gives `uv tool install specify-cli` followed by `specify init my-project --integration copilot` as the two-line quick start. Running `specify init` with a chosen agent sets up the corresponding command files and directory structures automatically.

## Features

The documentation frames Spec Kit's work as research and experimentation with four stated goals: technology independence, so that applications can be created using diverse technology stacks and the process is not tied to specific technologies, programming languages, or frameworks; enterprise constraints, covering mission-critical application development, organizational constraints such as cloud providers, tech stacks and engineering practices, and enterprise design systems and compliance requirements; user-centric development for different user cohorts and preferences, supporting approaches ranging from [[DefinedTerm/vibe-coding]] to AI-native development; and creative and iterative processes, including parallel implementation exploration, iterative feature development workflows, and upgrade and modernization tasks.

**Agent integrations.** The project site claims 35 integrations, naming Copilot, Gemini, Codex, Kilo Code, Zed, Claude, Forge, and Kiro among them, and states that users can switch freely between agents with a single command with no lock-in. For an agent that is not on the list, a `generic` integration is offered as an escape hatch.

**Extensibility layers.** Four named building blocks sit above the core process: presets tune it, extensions add to it, workflows orchestrate it, and bundles package the result for sharing. The site reports 138 community extensions from more than 70 authors and 25 presets, and is explicit that the process itself lives in these blocks, so a user is "never locked to SDD, or even to software." It lists six alternative processes built this way — AIDE, a seven-step AI-driven engineering lifecycle; Canon, baseline-driven workflows covering spec-first, code-first, and spec-drift; Product Forge, a product-management-oriented take on SDD; FX→.NET, an end-to-end .NET Framework migration across seven phases; MAQA, multi-agent orchestration with quality assurance gates; and Fiction Book Writing, for novels and long-form fiction from story bible to submission. Community extensions named as adding compliance gates and governance include CI Guard and Architecture Guard.

**Workflows.** The workflow engine is the automation layer for the same process. Spec Kit's reference documentation describes workflows as automating multi-step Spec-Driven Development processes by chaining commands, prompts, shell steps, and human checkpoints into repeatable sequences, with support for conditional logic, loops, fan-out/fan-in, and the ability to pause and resume from the exact point of interruption. Eleven step types are documented: `command` (invoke a Spec Kit command), `prompt` (send an arbitrary prompt to the coding agent), `shell`, `init`, `gate` (pause for human approval), `if`, `switch`, `while`, `do-while`, `fan-out`, and `fan-in`. A run persists its state under `.specify/workflows/runs/<run_id>/` as `state.json`, `inputs.json`, and `log.jsonl`, which is what makes `specify workflow resume` able to continue from the exact step where a run paused or failed; documented run states are `created`, `running`, `completed`, `paused`, `failed`, and `aborted`.

The built-in workflow that ships with the tool, `speckit` ("Full SDD Cycle"), makes the human checkpoints explicit: it runs `specify`, pauses at a `review-spec` gate, runs `plan`, pauses at a `review-plan` gate, then runs `tasks` and `implement`, with either gate's rejection aborting the run.

**Overlays.** Rather than editing an installed workflow, a project can layer an overlay onto it — a YAML file declaring edit operations (`insert_after`, `insert_before`, `replace`, `remove`) against the base workflow's step list, resolved by priority with lower numbers winning. The documented purpose is keeping local customisations safe across updates, since overlays live outside the installed workflow directory and survive reinstalling it. The documentation also states the limits plainly: overlays operate on the step list only, cannot change workflow metadata or the input schema, cannot target steps added by other overlays, and cannot use fan-out templates as anchors.

**Catalogs and distribution.** Workflows are discovered through catalogs resolved in a fixed order — the `SPECKIT_WORKFLOW_CATALOG_URL` environment variable overriding everything, then project config, then user config, then the built-in official and community catalogs — and organisations can host their own catalogs to curate what their developers discover. The site states the tool works offline, behind firewalls, and on Windows, macOS, and Linux.

**Stated security posture.** The workflows reference is unusually direct about what the engine does *not* guarantee, and the caveats are worth recording alongside the capabilities. A `shell` step runs a local command with the user's own privileges and there is no capability sandbox; the `requires` block is an advisory pre-condition, not a runtime gate, and a `requires.permissions` capability gate is rejected by validation precisely because it would imply a sandbox that does not exist. Expressions are resolved by plain string substitution with no quoting or escaping added, so an interpolated value reaching a `run` field is interpreted as shell syntax — a risk the documentation flags as sharpest for workflow inputs supplied by whoever runs the workflow and for a prior `prompt` step's output, which it says should be treated as untrusted because it is text produced by the AI agent and can in turn be influenced by files, tickets, or web content the agent read. Its recommended controls are to constrain values at the source with an `enum` allowlist, to keep unconstrained values out of `run` fields entirely, and not to treat quoting as a security boundary; it also warns that a `gate` step does not display or sanitise the command that follows it and prints its `message` verbatim, so untrusted material should be surfaced through `show_file`, whose contents are control- and ANSI-stripped, instead. On the same theme, its FAQ states that most workflows are independently created and maintained by their respective authors and that the Spec Kit maintainers do not review, audit, endorse, or support workflow code.

## Research use

Spec Kit's staged workflow has been used as the baseline that academic work builds on and measures against. [[ScholarlyArticle/spec-kit-agents]] takes the Specify → Plan → Tasks → Implement sequence as its starting point and argues that the structure alone does not prevent [[DefinedTerm/context-blindness]] — intermediate artifacts that are internally coherent yet incompatible with the target repository. Its proposed addition is a context-grounding layer wrapped around the existing stages: read-only discovery hooks that probe the repository before each phase, and validation hooks that check the resulting artifact afterwards, both kept outside the agent's main prompt. In that paper's own evaluation the addition raised a 1–5 composite judged-quality score from 3.51 to 3.66 across 128 runs, at the cost of roughly 13 minutes of extra runtime per run in its longer workflow family — figures reported by the paper's authors about their own system.

A second study, [[ScholarlyArticle/citation-discipline-in-spec-driven-development]], measures Spec Kit against two rival traceability disciplines and reaches a less favourable conclusion. It characterises Spec Kit as enforcing artifact-level consistency through its spec-plan-tasks chain, with the citation chain ending once implementation begins, and contrasts this with per-line requirement citations on one side and post-hoc external trace maps on the other. On its two measured dimensions Spec Kit came last: lower output determinism than either comparator (mean lexical similarity 0.460 against OpenSpec's 0.487 on Claude Sonnet 4.6, and 0.434 against 0.480 on GLM-5-turbo), and no automated hallucination detection at all, since detection in that study depended on requirement identifiers being present in the code itself. The paper states this makes Spec Kit "the weakest choice on the measured dimensions", while explicitly allowing that "its developer experience and natural workflow may compensate in practice".

## History

The project presents itself as community-built. Its site reports more than 240 contributors, over 121,000 GitHub stars, 35 integrations, 138 extensions, 25 presets, and 6 "friends" projects, and states that anyone can create and publish an extension, preset, or workflow. The site records its own last update as 16 July 2026.
