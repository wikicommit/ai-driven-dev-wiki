---
title: "Software Engineering 3.0 (SE 3.0)"
type: "schema:DefinedTerm"
lang: en
aliases: ["SE 3.0", "SE3.0"]
tags: [ai-native-software-engineering, ai-teammates, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06107'
    hash: sha256:16a4b6cfd923d16a41de150fe7052965c2d6efabb533839e3bb60287694f1747
  - type: url
    url: 'https://arxiv.org/pdf/2507.15003'
    hash: sha256:b606da9c64693060e32a07080b2f9686773353b1bf3df05702abeea29a093a76
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A proposed era of AI-native software engineering in which development is driven by intents that human developers and AI teammates clarify through conversation, and the AI — not the human — drives the loop of turning those intents into runnable software."
---

Software Engineering 3.0 (SE 3.0) is the name
[[ScholarlyArticle/towards-ai-native-software-engineering-se-3-0]] gives to the era of software
engineering it proposes, which it calls AI-native in contrast to the AI-assisted era before it. In
SE 3.0 development is intent-centric and conversation-oriented: it is driven not by code but by
intents — desired outcomes or goals a developer wishes to achieve — which human developers and their
AI teammates clarify through back-and-forth conversation, after which the AI drives the
code-creation loop by synthesising the intents into runnable software. The same paper presents this
as a throwback to the essence of the discipline, which has always been to turn intents into
high-quality software, with code only a means to that end.

## Usage

The term belongs to a three-era periodisation the paper sets out. Software Engineering 1.0 was
code-centric, with tools supporting traditional process activities and humans driving the entire
process. Software Engineering 2.0, the present era, keeps that code-centric approach while adding AI
models to support traditional activities (AI4SE); AI coding assistants are its prime example, and the
human still drives the code-creation loop. SE 3.0 is set against both: AI is no longer an assistive
tool but a transformative element, the AI becomes a teammate rather than a task-driven copilot, and
models are expected to be knowledge-driven and efficient rather than data-driven and costly to
train.

The paper grounds the term in a technology stack of five components, each named with a `.next`
suffix as an allusion to the future: Teammate.next for adaptive, personalised AI partnership,
IDE.next for intent-centric, conversation-oriented development, Compiler.next for multi-objective
code synthesis, Runtime.next for SLA-aware execution with edge-computing support, and FM.next for
knowledge-driven models trained with [[DefinedTerm/curriculum-engineering]]. Because it is a
vision, the paper describes these by their desired attributes rather than by a concrete
implementation, and it names commercial vibe coding platforms as very early glimpses of the era
rather than as instances of it.

[[ScholarlyArticle/the-rise-of-ai-teammates-in-software-engineering-3-0]] takes up the term from that
vision and uses it for empirical work. It glosses SE 3.0 as agentic software engineering, in which
developers collaborate with autonomous AI teammates through an intent-driven, conversational process;
the agents work at the task level — reading codebases, planning changes, executing tools, running
tests and submitting pull requests — while the developer's role shifts to orchestration: setting
goals, constraints and permissions and reviewing the final changes. It names Devin, GitHub Copilot
Workspace, Google Jules, OpenAI Codex, Claude Code, Cursor DeepAgent and Genie as typical tools of
the era. The same paper adds an intermediate step, SE 1.5 or predictive coding, for token-level
assistance such as autocomplete that sits between SE 1.0 and SE 2.0, and treats autonomous coding
agents opening pull requests on GitHub as evidence that SE 3.0 is already unfolding rather than
still ahead. It argues that practices such as Agile, Scrum and DevOps were built for all-human teams
and that SE 3.0 calls for new methodologies for orchestration, review and governance.

## Related Terms

- [[DefinedTerm/ai-native-software-engineering]] — a separately proposed account of AI-native
  software engineering, organised around the unit of work, the correctness model and the
  accountability model
- [[DefinedTerm/software-3-0]] — a similarly numbered but distinct term about programming large
  language models through prompts and context
- [[DefinedTerm/curriculum-engineering]] — the training approach the SE 3.0 stack relies on for its
  models
