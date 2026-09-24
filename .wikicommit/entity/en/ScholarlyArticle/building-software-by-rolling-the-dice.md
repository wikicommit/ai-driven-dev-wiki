---
title: "Building Software by Rolling the Dice: A Qualitative Study of Vibe Coding"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, ai-assisted-programming, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.22418'
    hash: sha256:f10a74dba745c31d031399f5009f9e4afada40b2a3620baed32d7616596a8ba6
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An FSE '26 grounded-theory study of 20 vibe coding videos — seven live-streamed sessions and 13 opinion videos — describing how vibe coders define and practise vibe coding and how they cope with the stochastic nature of AI generation."
  author: ["Yi-Hung Chou", "Boyuan Jiang", "Yi Wen Chen", "Mingyue Weng", "Victoria Jackson", "Thomas Zimmermann", "James A. Jones"]
  keywords: ["[[DefinedTerm/vibe-coding]]", "[[DefinedTerm/rolling-the-dice]]", "grounded theory", "mental models", "design fixation"]
---

A paper by Yi-Hung Chou, Boyuan Jiang, Yi Wen Chen, Mingyue Weng, Victoria Jackson, Thomas Zimmermann and James A. Jones, for the ACM International Conference on the Foundations of Software Engineering (FSE '26). It asks how practitioners actually define and engage in [[DefinedTerm/vibe-coding]] — building software primarily through prompts rather than writing code — given that the term has become an umbrella for practices ranging from fully delegating to autonomous agents to agent-supported engineering that still involves manual editing and inspection. The authors call the people they study "vibe coders", a group that includes both professional programmers and "vernacular" programmers who are not formally trained but create software for their own needs.

The authors used Straussian grounded theory on publicly shared YouTube videos: seven live-streamed or minimally edited coding sessions (about 16 hours, 254 prompts) and 13 opinion videos in which practitioners reflected on vibe coding (about 5 hours). Videos were selected by keyword search and then purposive sampling for maximum variation in background, problem domain and tools, including a second search targeting coders with no experience. The coding team combined a developer, a software-engineering researcher, a product designer and a product manager. The qualitative analysis was supplemented by annotating 2,439 activities in the live streams to measure time allocation and by coding every prompt by intent to measure how often coders repeated a request without new information.

The resulting framework describes five entities — vibe coders, prompts and contexts, wrappers and tools, foundation models, and artifacts — and three recurring activities: requirements and design, implementation and debugging, and evaluation. Its central image is that, across approaches, vibe coders must contend with the stochastic nature of generation, so that debugging and refinement come to feel like "rolling the dice".

## Key Points

- Behaviour spanned a spectrum from coders who relied almost entirely on AI and never inspected code — one never opened a file across nearly five hours — to coders who read diffs and adapted the generated code. Some practitioners argued for a strict definition of vibe coding while others rejected the boundary between vibe coding and traditional software engineering.
- Trust in AI took three forms: purposive (accepting output without scrutiny as a performance for the audience), unwilling (deferring to the AI despite frustration), and, most often, selective (calibrating when to rely on AI and when to intervene).
- Vibe coders built opportunistic workflows, mapping specific wrappers and models to tasks and combining them; opaque tool behaviour, such as context passed to the model without being visible to the user and hidden token costs, hindered accurate mental models.
- Coders' mental models of the artifacts, shaped by their expertise and reliance on AI, influenced their prompting, evaluation and trust: those who knew or had read the code wrote more prescriptive prompts with specific context.
- Tasks expected to be deterministic, such as debugging or refining a feature, felt stochastic. The authors call reissuing a prompt with the same intent and no new information [[DefinedTerm/rolling-the-dice]]; the two high-reliance live-streamers devoted nearly 40% of their prompts to it, while coders who inspected code or had relevant backgrounds typically stayed under 20%. One coder sent 31 consecutive prompts consisting only of error messages over an hour.
- To rein in stochastic changes, coders used undo, version control, small incremental changes, automated tests and linters.
- Many coders formulated new requirements in response to outputs, in a way the authors compare to exploratory programming, yet they typically accepted or refined the first generated output rather than seeking alternatives, which the authors read as design fixation.
- Waiting for generation took over 20% of total session time across all live streams, and more than half of one session; coders coped by multitasking or sending prompts in parallel. Time spent checking external resources was under 5%.
- Keeping track of what had already been shared with the model was a recurring challenge; some coders externalized it in a progress file, instruction files or an external memory graph.

## Notes

The authors present the study as a snapshot rather than a definition of what should count as vibe coding. They acknowledge that all data came from English-language YouTube videos, dominated by Python and JavaScript, and that the performative nature of live-streaming may limit how far the findings transfer to industry settings with legacy code, governance and long-term maintenance.

For tool designers they suggest summarizing sent prompts within the IDE, adapting responses to users' expertise, supporting conflict resolution when prompts run in parallel, importing error messages and terminal output automatically, and making wrappers' hidden context, system prompts and token costs more transparent. For educators they argue that deductive education — teaching general principles before applying them with AI — remains essential, because a learner needs enough knowledge to ask the right questions and to spot suboptimal output.
