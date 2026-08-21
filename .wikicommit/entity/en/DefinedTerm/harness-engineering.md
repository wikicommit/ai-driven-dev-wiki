---
title: "harness engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, agent-architecture, terminology, configuration]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
  - type: url
    url: 'https://github.com/ai-boost/awesome-harness-engineering'
    hash: sha256:a83ac76e225c672c3502d7424fae660eed200f06a0e01215ae550f564976915d
  - type: url
    url: 'https://arxiv.org/pdf/2607.03691'
    hash: sha256:2ca8495996618345fe8107bd0b9cf73cf84283dc0135c961a0fadc83ce891c49
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The practice of improving a coding agent's output quality and reliability by configuring the harness around the model — context files, MCP servers, skills, sub-agents, hooks, and verification mechanisms — rather than waiting for a better model. Presented as a subset of context engineering aimed specifically at managing the agent's context window."
  termCode: ""
  inDefinedTermSet: ""
---

Harness engineering is the practice of using a coding agent's configuration points to improve its output quality and reliability, on the premise that most agent failures are configuration problems rather than model problems. [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] credits the coinage to Viv (Viv Trivedy), and quotes Mitchell Hashimoto's formulation of it: the idea "that anytime you find an agent makes a mistake, you take the time to engineer a solution such that the agent never makes that mistake again."

The underlying decomposition it rests on is `coding agent = AI model(s) + harness`, where the harness is the agent's runtime or peripherals — what the model uses to interact with its environment. Skills, MCP servers, sub-agents, memory, hooks, and context files are separate concepts, but the argument is that they form a single configuration surface, and that configuring that surface is where the available leverage sits.

## Usage

**As a subset of context engineering.** HumanLayer's account places harness engineering inside [[DefinedTerm/context-engineering]] — the broader term it credits to Dex Horthy's 12-factor agents work — as specifically the part that leverages harness configuration points to manage the agent's context window. It frames the practice as answering a set of questions no prompt can: how to give the agent new capabilities, how to teach it things about a codebase absent from training data, how to add determinism beyond writing `CRITICAL: always do XYZ` in the system message, how to adapt behaviour to a specific codebase, and how to keep the context window from inflating too fast or with bad context.

**The levers.** The post points at two of Viv's posts: the first framing four customization levers — system prompt, tools and MCPs, context, and sub-agents — and the second working backwards from what models cannot do natively to derive why each harness component exists. To those four it adds two of its own: **hooks**, for automated integration and deterministic control flow, and **skills**, for progressive disclosure of knowledge (which Dex Horthy prefers to call "instruction modules"). After months of solving hard problems in complex brownfield enterprise-scale codebases, it singles out [[DefinedTerm/subagents]] as a particularly powerful lever, on the grounds that they are what maintains coherency across the many context windows such a problem takes.

**A disputed scope.** The post notes that OpenAI has written on the topic too and reads its position as treating harness engineering as configuring everything *outside* the agent's runtime, with a focus on back-pressure and verification mechanisms — while flagging its own uncertainty about that reading, since the word "harness" appears only once in that post's text and in reference to evals.

**The post-training objection, and the reply.** Because frontier coding models are post-trained on their own harnesses, one argument holds that the best configuration is the untouched one the model was trained on. The post concedes the coupling is real — its example is OpenCode having to add an `apply_patch` tool specifically for GPT/Codex models to mimic the Codex harness, while Claude and other models continue to use ordinary edit and write tools — but argues the coupling cuts both ways: models can be *over-fitted* to their harness. Its cited evidence is Viv's observation about Terminal Bench 2.0, where Opus 4.6 in Claude Code places 33rd but reaches 5th in a harness not seen during post-training, with an error band of roughly four positions either way.

**Practice, not perfectionism.** The post's stated approach is to bias towards shipping and configure only in response to real failures rather than anticipated ones. Its list of what did not work is as specific as its recommendations: designing the ideal configuration upfront before hitting real failures; installing dozens of skills and MCP servers just in case; running a five-minute test suite at the end of every session; and micro-optimising which sub-agents could access which tools, which it reports produced tool thrash and worse results. What did work, on its account: starting simple and adding configuration only after an actual failure, iterating and discarding what did not help (the author reports throwing away many more hooks than are in use), distributing battle-tested configurations to the team through repository-level config, optimising for iteration speed rather than one-shot success, and giving the agent a broad capability first and then paring back what is exposed once the needs are known.

### A literature, and how it is being carved up

That the term now has a body of literature rather than a handful of posts is itself observable. `ai-boost/awesome-harness-engineering`, a CC0-licensed curated list on GitHub carrying 3.7k stars and 440 forks at the time it was read, describes itself as "curated resources, patterns, and templates for building reliable AI agent harnesses" and organises the field into seven top-level sections: Foundations, Design Primitives, Reference Implementations, Security/Sandbox & Permissions, Evals & Verification, Templates, and Production Infrastructure & Operations, plus a pointer to adjacent awesome lists.

Its **Design Primitives** section is the most substantive part for definitional purposes, because it decomposes the harness explicitly "by the problem they solve, not by vendor" — into twelve areas: agent loop; planning and task decomposition; context delivery and compaction; tool design; skills and MCP; permissions and authorization; memory and state; task runners and orchestration; verification and CI integration; observability and tracing; debugging and developer experience; and human-in-the-loop. That decomposition is broader than the six levers above, adding operational concerns — observability, debugging, task running — that the practitioner accounts treat as background rather than as harness components.

Its **Foundations** section, described as "canonical essays that define what harness engineering is and why it matters," shows the term being used in parallel by several parties rather than belonging to one: it lists essays under this name from [[Organization/anthropic]], [[Organization/openai]], Google, Microsoft, Red Hat, LangChain, deepset, IBM, and Meta, alongside academic work, and includes pieces by [[Person/martin-fowler]] and [[Person/birgitta-bockeler]]. The list also links a separate academic survey and reading list on agent harness engineering maintained by another group.

This is a curated index rather than an argument, and each entry carries the list maintainer's own one-line characterisation of a document; none of those linked documents has been ingested here, so no claim from them is recorded on this page. What the list supports directly is the shape of the field: that harness engineering is being written about across vendors, academia, and practice, and that the components being catalogued under it extend past configuration into operations.

### Evidence for the premise, and a warning attached to it

The practice rests on a premise — that the harness rather than the model determines much of an agent's behaviour — which the practitioner accounts above assert from experience. [[ScholarlyArticle/dont-blame-the-large-language-model]] supplies a controlled test of it, and the result cuts both ways.

It supports the premise by construction: holding the language model fixed and varying only the harness across 35 sequential releases of one CLI produces measurable quality variation, which is only possible if the harness is doing real work. But the direction of that variation is the warning. Across those releases there is no statistically significant improvement in resolve rate on the benchmark tasks used, early versions sometimes beat later ones, and token consumption and tool calls roughly double without corresponding gains. Feature-heavy releases buy resolve rate at the cost of efficiency; fix-heavy releases raise cost without buying resolve rate.

The practice this suggests is missing is the one the paper names **agentic quality assurance** — regression testing that measures the agent's non-functional quality, token consumption and tool-call overhead included, rather than only whether a generated patch is correct. Its evidence that this gap is real is that every concrete quality degradation it documents passed all the projects' existing automated checks. Read alongside the "engineer a solution so the agent never makes that mistake again" formulation above, this is the same discipline pointed at the harness developer rather than the harness user: without measurement across versions, harness changes are as capable of degrading an agent as improving it, and the degradation is invisible to conventional tests.

## Related Terms

Harness engineering is the practice; the [[DefinedTerm/agent-harness]] is the thing being engineered, and [[DefinedTerm/agent-scaffolding]] the construction-time half of that pair. Its named levers each have their own entries: [[DefinedTerm/context-files]], [[DefinedTerm/model-context-protocol]], [[DefinedTerm/agent-skills]] and their [[DefinedTerm/progressive-disclosure]] loading, [[DefinedTerm/subagents]], [[DefinedTerm/agent-hooks]], and [[DefinedTerm/backpressure]]. The problem the whole practice is organised against is [[DefinedTerm/context-rot]].
