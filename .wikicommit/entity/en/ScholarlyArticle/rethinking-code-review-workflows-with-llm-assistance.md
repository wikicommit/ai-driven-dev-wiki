---
title: "Rethinking Code Review Workflows with LLM Assistance: An Empirical Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, llm, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.16339'
    hash: sha256:78406c6d65c0482ec67f587e57301d001b7a19588940081a8a9344bd02816f28
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A two-phase field study and field experiment at WirelessCar Sweden AB comparing two interaction modes for LLM-assisted code review — an AI-led co-reviewer that summarises a pull request upfront and an on-demand interactive assistant — finding the AI-led mode generally preferred but the preference conditional on reviewer familiarity and pull request severity."
  author: ["Fannar Steinn Aðalsteinsson", "Björn Borgar Magnússon", "Mislav Milicevic", "Adam Nirving Davidsson", "Chih-Hong Cheng"]
  datePublished: "2025-05-22"
  keywords: ["Large Language Models", "Code Review", "Empirical Software Engineering"]
  citation: "arXiv:2505.16339"
---

This paper asks how large language models can be integrated into code review workflows in a way
developers actually want, rather than how well a model performs at review as a task. Its premise is
that manual review struggles as systems scale and delivery accelerates, and that while LLMs have
moved smoothly into coding activities their use in review remains underexplored. The authors frame
two questions: what characterises current review practice and where developers see room for AI
assistance, and how developers perceive and interact with LLM-assisted review tools.

The method is a two-phase qualitative study at WirelessCar Sweden AB, a company where some but not
all teams are permitted to use AI in development. Phase 1 was an exploratory field study of seven
participants — software engineers, an application developer, a security engineer and a quality
assurance specialist across four teams — interviewed semi-structuredly and analysed thematically,
with the authors reporting data saturation after the seventh interview. Phase 1's findings then
drove the design of two prototype interaction modes, which Phase 2 evaluated in a field experiment
with ten participants, five returning from Phase 1 and five recruited through internal Slack
channels. Each participant reviewed two pull requests of comparable size from the company's own
codebase, one in each mode, with mode assignment rotated to mitigate ordering effects, and four of
the ten belonged to the team that owned the code so that familiarity could be compared.

Both modes ran on the same artifact: a web-based chat interface over OpenAI's o4-mini, with a
retrieval-augmented generation index built on LlamaIndex that had to be prepared and indexed
manually before the experiments, exposing three semantic tools — one for pull request diffs and
metadata, one for the repository's full source, and one for the Jira ticket motivating the change.
Mode A, the co-reviewer, added a fourth tool containing a sub-agent that produced a structured
review upfront from the complete pull request data injected into its context, so that no file
change could be missed by retrieval. Mode B, the interactive assistant, stayed passive and
answered only when asked, a design the authors chose both to match Phase 1's request for a
lightweight on-demand tool and to avoid the reported risk that automatically highlighted lines
lead reviewers to overlook other areas.

## Key Points

- Phase 1 interviews identified delayed reviews, large or complex pull requests that reviewers
  avoid picking up, context switching, and missing context in pull request descriptions as the
  recurring challenges in the company's existing review practice.
- No interviewed team had formally integrated AI into code review, although general AI coding tools
  were in common use for development tasks, and teams permitted to use them did so through an
  enterprise subscription under which their data is not used for training.
- Developers proposed pull request summarisation, checking code against stated requirements, and
  detection of subtle defects such as race conditions as the assistance they would want; their
  concerns were mostly about security risk and about false positives eroding attention.
- In the field experiment the AI-led co-reviewer mode was generally preferred, particularly for
  large or unfamiliar pull requests and for low-risk changes, while the interactive mode was
  favoured by participants already familiar with the codebase or wanting to retain full control.
- Preference was context-dependent rather than uniform, varying with reviewer familiarity with the
  codebase and with the severity of the pull request; some participants wanted both modes combined.
- Participants reported the assistant surfacing issues they would not otherwise have caught, and
  also reported incorrect or unclear suggestions, difficulty separating important findings from
  minor ones in long summaries, and a risk of being anchored by the AI's initial framing in the
  AI-led mode.
- Participants asked for the assistant to be embedded in tools they already use — GitHub, Slack,
  the IDE — rather than presented as a new interface, and cited long response times as a barrier to
  adoption.
- Participants independently proposed uses outside the study design: running the AI-led mode as a
  pre-review aid before submitting a pull request, and running a human-led review first and then
  using the assistant to catch what was missed.
- The authors conclude that LLMs can meaningfully augment, rather than replace, human reviewers,
  and state that they do not treat LLMs as replacements largely because of hallucination.

## Notes

This is a qualitative study at a single company, with seven interview participants in Phase 1 and
ten in Phase 2, recruited by convenience sampling; the authors position it as capturing how
developers interact with an assistant rather than as a performance measurement, explicitly setting
it apart from prior work that measured issue detection or compared against existing tools. The two
pull requests in the experiment were selected for moderate and comparable size, and the paper's
remarks about large pull requests come from participant statements. The
artifact was built for the study rather than as a production system, and one participant questioned
how well such an assistant would hold up against very large codebases and heavy business logic.
