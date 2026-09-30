---
title: "Towards AI-Native Software Engineering (SE 3.0): A Vision and a Challenge Roadmap"
type: "schema:ScholarlyArticle"
lang: en
tags: [ai-native-software-engineering, software-engineering, ai-teammates, vision-paper]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06107'
    hash: sha256:16a4b6cfd923d16a41de150fe7052965c2d6efabb533839e3bb60287694f1747
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A vision paper proposing Software Engineering 3.0 (SE 3.0), an AI-native approach in which development is driven by intents that human developers and AI teammates clarify through conversation, together with a five-component technology stack and a roadmap of open challenges."
  author: ["Ahmed E. Hassan", "Gustavo A. Oliva", "Dayi Lin", "Boyuan Chen", "Zhen Ming (Jack) Jiang"]
  keywords: ["AI-native software engineering", "Software Engineering 3.0", "Intent-driven development", "Conversational AI", "AI copilots", "Large language models (LLMs)", "Code synthesis", "Knowledge-powered models", "Human-AI collaboration", "SLA-aware runtime"]
---

This vision paper, by authors from Queen's University, the Centre for Software Excellence at Huawei
Canada and York University, argues that today's AI-assisted software engineering — which it calls
Software Engineering 2.0 — has exposed inherent limitations, and proposes a shift to
[[DefinedTerm/software-engineering-3-0]] (SE 3.0). SE 3.0 is described as AI-native rather than
AI-assisted: development is driven not by code but by intents, expressed and refined through
back-and-forth conversation between human developers and AI teammates, with the AI driving the
code-creation loop by synthesising those intents into runnable software.

The authors say the vision and its challenges were identified from surveys of academic and grey
literature, discussions with industrial and academic leaders at a series of events, meetings with
their customers and internal development teams, their own experience building FMware and the SE 3.0
stack, and interactions with industrial partners in the Open Platform for Enterprise AI (OPEA)
alliance. Because the paper is visionary, it describes the desired attributes of each component
rather than a concrete implementation, and presents itself as a starting point for discussion,
explicitly welcoming opposing views.

## Key Points

- SE 2.0 continues SE 1.0's code-centric approach while adding AI models to support traditional
  activities (AI4SE); its prime example is the AI coding assistant.
- SE 2.0 places a high cognitive overload on developers, because the human still drives the
  code-creation loop, decomposing problems, prompting assistants, evaluating suggestions and
  debugging failures.
- Frontier foundation models are trained inefficiently on massive, uncurated internet-scale data,
  which the authors link to high computational and environmental cost, limited depth of reasoning and
  an ongoing retraining burden.
- AI coding assistants show an additive bias, favouring adding code over refactoring or simplifying
  it, which the authors argue produces bloated, harder-to-maintain code.
- As assistant-generated code becomes pervasive, it risks contaminating the data used to train future
  models, creating a feedback loop that degrades model quality.
- Autonomous software engineers are acknowledged, but the authors argue their lack of focus on
  human-AI alignment of intents leaves them prone to solutions that miss the true requirements.
- The SE 3.0 technology stack has five components: Teammate.next (adaptive, personalised AI
  partners that also act as one-on-one mentors), IDE.next (an intent-centric, conversation-oriented
  IDE in which source code is hidden by default), Compiler.next (multi-objective code synthesis by
  search, trading off accuracy, latency and cost), Runtime.next (an SLA-aware runtime unifying
  FM-related activities in a single cluster, with an edge-computing extension) and FM.next
  (knowledge-driven models trained through curriculum engineering).
- In IDE.next, human-AI conversations become a key asset to version-control, because the
  code-creation loop can be re-run from them — for example when a new model is released.
- Compiler.next includes a goal-tracking mechanism that derives tests from intents rather than from
  existing code, which the authors call a well-known AI4SE pitfall.
- Five key challenges are set out, each with open questions: speeding up human-AI alignment (for
  which the authors propose giving AI teammates a theory of mind of the human), improving the
  efficiency of code synthesis, improving runtime performance, improving models' understanding of
  code and software engineering, and eliminating the need for prompt engineering; eight further open
  questions are listed without a developed vision.
- The authors see very early glimpses of SE 3.0 in commercial vibe coding platforms such as Lovable,
  Base44, Replit, Bolt.new and v0 by Vercel.

## Notes

The paper suggests researching the challenges of all five stack components in parallel, while
acknowledging that IDE.next largely depends on the others, and states that the vision can only be
validated as a whole once prototypes exist for every component. It singles out the democratisation of
AI as a challenge needing timely action, arguing for more cost-effective training and serving
approaches and for "small and mighty" models with deeper software engineering knowledge.
