---
title: "Software 3.0 시대, Harness를 통한 조직 생산성 저점 높이기"
type: "schema:BlogPosting"
lang: en
tags: [coding-tools, claude-code, context-engineering, platform-engineering]
sources:
  - type: url
    url: 'https://toss.tech/article/harness-for-team-productivity'
    hash: sha256:c578d09dce25f7293277154d1741cd800ad5d6afd7700ee897468e966f53f939
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An argument that the wide variation in what engineers get out of the same model is an organizational loss rather than a matter of individual skill, and that a coding agent's plugin and marketplace mechanism is the way to distribute a team's working methods as a system. The author presents it explicitly as a direction and a hypothesis rather than a result."
  author: "김용성"
  datePublished: "2026-02-26"
  publisher: "토스테크 (Toss Tech)"
---

The post opens on an observation about variance: teams have adopted large language models, but on
the author's reading each engineer is left to fend for themselves, and the same model and the same
IDE produce very different results. The illustration given is two engineers on the same repository
and the same task — one who sets up context first, feeding the repository's coding guidelines, lint
rules and existing patterns to the model before asking for anything, and gets something mergeable
in ten minutes; another who opens with "refactor this function" and spends an hour repeating that
the team does not do it that way. The author insists the difference is not coding ability but
know-how in controlling the tool, and that leaving that gap to individual sense is a loss at the
organizational level.

From there the post argues that a coding agent's plugin and marketplace mechanism is not merely an
extension mechanism but a way to distribute how an organization works. Its central claims are
[[DefinedTerm/executable-ssot]] — knowledge defined as a plugin reads as a guideline to a person
and as a system prompt to a model, so updating the plugin updates the team's agent behaviour — and
[[DefinedTerm/raising-the-floor]], improving the weakest case rather than the best one. The author
is repeatedly explicit that this is a direction rather than a demonstrated result, closing by
saying most of it is hypothesis and that how a team's workflow actually evolves on a marketplace
has to be tried to be known.

## Key Points

- The variance between engineers using the same model is presented as a gap in know-how about
  controlling the tool, not in coding ability, and as something an organization should not leave to
  individual aptitude.
- The author singles out Claude Code, naming Open Interpreter and OpenCode as fine earlier attempts
  while arguing that the sense of using a new tool still creates friction, and that leaving for a browser to paste code into a chatbot costs a context switch.
  Mixing natural language and code in the terminal where developers already spend their time is
  what the author says lets a designed workflow spread through a team without resistance — offered
  as the least-friction entry point at the current moment rather than as a settled verdict.
- Wiki and document pages are argued to be stale from the moment they are written because they are
  for people to read, whereas knowledge defined as a plugin serves both audiences at once and
  changes agent behaviour the moment it is updated.
- The author argues that generic open-source plugin collections are a good starting point but do
  not know a team's domain, and that each team has its own division between what AI does well and
  what a person must review.
- The whole arrangement is presented as a repetition of platform engineering: shared modules become
  AI workflow plugins and library publication becomes marketplace upload, with only the module's
  contents changing from code to prompts and agent logic. Quality assurance is claimed to carry
  over too — plugins should be reviewed the way shared modules are.
- A marketplace is argued to be preferable to retrieval-augmented generation on two grounds:
  predictability, since a plugin is explicit text a developer controls completely while RAG's
  hybrid search and reranking make it hard to foresee what context will be injected; and speed of
  experimentation, since a plugin can be revised locally and validated in the terminal without a
  deployment.
- Two scenarios are offered for what distribution buys. In the first a hook intercepts a commit
  attempt on the main branch and redirects the agent to create a feature branch, which the author
  contrasts with a linter that only blocks — a plugin instead corrects behaviour toward the team's
  convention. In the second a single slash command carries the best engineer's whole workflow —
  gathering context by conversation, opening an issue, creating a branch, writing a plan for human
  approval, implementing, opening a pull request — so that any engineer runs it at the same
  quality.
- Plugin knowledge is proposed to be layered into a global layer of company-wide rules, a domain
  layer of team and business knowledge, and a local layer of repository-specific detail, on the
  analogy that a new joiner is not handed every company document at once.
- A longer-range "data flywheel" is offered explicitly as a hypothesis: standardized data
  accumulating through plugins, used to fine-tune a domain-specific model, with the existing
  workflows serving as its evaluation criteria. The author lists its preconditions — a long enough
  collection period, a quality-control process, and sustained organizational investment.

## Context

The post is positioned as a follow-up to the author's earlier writing on the same blog about the
Software 3.0 era, and takes [[DefinedTerm/software-3-0]] as its frame without restating it. Its
subject, the mechanism described in [[DefinedTerm/claude-code-plugin-marketplace]], is treated here
at the level of what an organization could do with it rather than how it is built.

The caveats are the author's own and are stated more than once: this is described as closer to a
direction than to a concrete success story, as a sharing of possibilities the author sees, and in
the conclusion as mostly hypothesis. The comment thread is unimpressed on a related point, with
more than one reader calling the post abstract or vague; one of them reduces it to a single line —
that a harness and a verification loop are necessary in agent development — and remarks that an AI
asked the same question would say as much. One commenter raises a substantive objection
the post does not address: that a sufficiently controlled RAG pipeline could be as predictable as a
plugin, that tracking which of dozens of plugins are active becomes its own visibility problem, and
that the two are anyway different kinds of thing, one a knowledge-retrieval tool and the other a
definition of behavioural rules. The post also states that all its images were produced by
generative AI.
