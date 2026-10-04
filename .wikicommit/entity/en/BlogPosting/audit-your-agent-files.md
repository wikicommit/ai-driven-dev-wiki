---
title: "Audit your Agent files"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agent-skills, coding-agents]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/audit-your-agent-files/'
    hash: sha256:bf6cc075edd2de267c6190a1d95d339738e4119f4228c256549765493314d40a
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Addy Osmani's argument that a coding agent's configuration — context files, skills, plugins, MCP servers, hooks and memory — has a half-life as models, harnesses and codebases change, so it should be audited on a cadence and each instruction asked to earn its place again rather than accumulated indefinitely."
  author: "Addy Osmani"
  datePublished: "2026-08-27"
---

This post argues that "your coding agent's configuration has a half-life." Models improve, harnesses add capabilities and codebases change, while instructions written for an older setup stay behind. The author treats everything that accumulates between a developer and the model as one environment to audit — [[DefinedTerm/claude-md]] and [[DefinedTerm/agents-md]] context files, [[DefinedTerm/agent-skills]], plugins, [[DefinedTerm/model-context-protocol]] servers, [[DefinedTerm/agent-hooks]], memory, commands and subagents, and permissions and settings — and singles out permissions and settings as "the only rules here that actually bind the agent."

He writes as a self-described fan of skills who maintains a skill pack of his own, and presents the post as taking the critiques of skills and context files seriously rather than dismissing them. Its recommendation is periodic hygiene: run an audit every few weeks, review memory separately, archive before deleting, and test whether a task still goes well without the local configuration.

## Key Points

- Agent configuration rots through a ratchet: the agent gets something wrong, a rule is added, the file grows and dilutes what matters, adherence drops, and the cycle repeats — until a short decision guide has turned into a knowledge base.
- The failure modes the author reports finding in his own files are overly long examples, content already carried by READMEs, package manifests or skill files, a rule added every time the agent errs, and rules so specific they still miss the intended outcome.
- He cites a study of 100 popular repositories as finding lint-related leakage in 62%, context bloat in 42% and skill leakage in 35% of their agent files.
- He cites a paper that turned developers' interaction history into personal skills as finding that personalization did not help much: a skill from one developer's history performed about as well as one borrowed from someone else, and a generic skill built from many developers was more useful overall. He notes the experiments used an LLM-based developer simulator, and takes away to start from a strong generic skill and add personal rules gradually.
- He cites a paper finding that, across 288 runs on 17 real tasks, context files did not make a clear difference to the correctness of Claude Code and Codex — but did change how the agents worked, for instance running targeted tests after a guide warned that the full suite was slow.
- From that he concludes context files should hold what the model cannot easily infer from the code — how to run the right checks, which operations are expensive, what must remain untouched, where unusual conventions live — rather than generic advice on clean code or summaries of existing code; he cites a related study in which prose summaries answered 4 of 45 behavioural questions about code against 27 of 45 for the source itself.
- He reports Anthropic's statement that it removed more than 80% of Claude Code's system prompt for its Claude 5 generation models with no measurable loss on internal coding evaluations, and cautions that the result is not a target, since those evaluations are not public and cover specific models in a specific harness. His lesson is that instruction value can expire, and that a rule which must always hold belongs in a test, hook or permission rather than in prose.
- In [[SoftwareApplication/claude-code]], the author distinguishes `/doctor` inside a session, a configuration audit that surfaces unused skills, MCP servers and plugins relative to their context cost, slow hooks and duplicated CLAUDE.md guidance, from `claude doctor` in a shell, which only prints installation diagnostics. He also reviews memory separately with `/memory`, because auto-memory can hold stale preferences after the project files are tidy.
- He corrects a common claim about skill cost: an installed skill does not load its whole body into every prompt, since only names and descriptions load for discovery within a listing budget that defaults to 1% of the context window, and the body loads on invocation. The case for pruning, on his account, is discoverability, accidental triggering, maintenance and the developer's own clarity rather than token cost.
- His recommended cadence is every couple of weeks or once a month: archive the setup first, run `/doctor` and `/memory`, remove what is flagged or no longer remembered, run a real task with no local skills, then keep the deletion or restore it. He frames the no-skills run as a smoke test rather than proof, since agent outcomes vary between runs.
- "Installing a useful skill and keeping it forever are separate decisions."

## Context

The post starts from developer discussion about how hard it is to keep skills and context files current and under the 200-line guidance for CLAUDE.md, and from official advice to periodically delete a CLAUDE.md, skills and hooks and rebuild only what matters — advice the author thinks is sound in principle but harder to act on than it sounds, because people fear quality will drop and lack an easy way to restore. His own audit surfaced writing and design skills he had forgotten installing. He reports that companies he has spoken with see shared team or organization skills, capturing engineering culture, compliance rules and internal tooling quirks, as compounding in value.

It lists three other posts by the same author as related reading: [[BlogPosting/brownfield-agentic-engineering]], [[BlogPosting/agentic-skill-decay]] and [[BlogPosting/human-judgment-doesnt-leave-the-software-factory]].
