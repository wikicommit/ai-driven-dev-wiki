---
title: "Agentic coding and persistent returns to expertise"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, evaluation, human-ai-collaboration]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/claude-code-expertise'
    hash: sha256:0a6863b8e2c10a2517ea14c69053f2df45ca56ecf794fbbe95c1dc977fbf3879
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An Anthropic study of roughly 400,000 Claude Code sessions from October 2025 to April 2026, measuring what the work consists of, who makes which decisions, and what predicts a session ending in success. Its central finding is that domain expertise, not a coding background, is what most predicts success."
  author: ["Zoe Hitzig", "Maxim Massenkoff", "Eva Lyubich", "Shaoyi Zhang", "Ryan Heller", "Peter McCrory"]
  datePublished: "2026-06-16"
  citation: "Hitzig, Z., Massenkoff, M., Lyubich, E., Zhang, S., Heller, R., & McCrory, P. (2026). Agentic coding and persistent returns to expertise. https://www.anthropic.com/research/claude-code-expertise"
---

This report introduces a framework for studying interactive [[DefinedTerm/agentic-coding]] and applies
it to a privacy-preserving analysis of roughly 400,000 [[SoftwareApplication/claude-code]] sessions
recorded between October 2025 and April 2026. It asks three questions of that data: what the work
actually consists of, how decision-making is divided between the person and the agent, and what
distinguishes sessions that end in success.

The division of labour it finds is asymmetric in a specific way. People make about 70% of the planning
decisions — what to do, which approach to take, what counts as done — while the agent makes about 80%
of the execution decisions: which files to change, what code to write, which commands to run. The
authors summarise this as people deciding what to build and the agent deciding how.

Its titular finding concerns who gets the most out of that arrangement. Sessions where the user
displays greater task-specific expertise succeed more often and set longer chains of agent work in
motion per instruction — and yet, on coding tasks, every major occupation succeeds at close to the rate
software engineers do. The authors read these together as evidence that a coding background is becoming
less relevant to successful programming while command of a domain is not.

## Key Points

- The study classifies each session into one of nine work modes. Roughly 56% of sessions write (25%),
  fix (26%), or test and orchestrate (5%) code; 17% operate software (deploying, configuring, running
  pipelines, monitoring); 14% plan or work out how an existing system behaves; and 13% produce data
  analysis or prose documents.
- Decision attribution is measured by a classifier that lists the meaningful decisions in a session,
  splits them into planning and execution, and attributes each to the person or the agent. The average
  result is about 70% of planning decisions to the person and about 20% of execution decisions.
- A typical session runs about four turns, and each user prompt sets off a chain of around 10 agent
  actions on average — sometimes over 100 — with the agent reading files, editing code, running commands
  and writing an average of 2,400 words of output per turn.
- How much the agent does between check-ins tracks who holds the decisions: where the user makes over
  80% of execution decisions the agent takes about eight actions per turn, and where the agent makes
  over 80% of planning decisions it takes about 16.
- Expertise is rated from the transcript on a five-point novice-to-expert scale and is explicitly
  task-specific rather than a proxy for job title or general ability — the authors' examples are a senior
  engineer asking a first Rust question (a beginner at Rust) and an accountant who has never used Python
  but can specify exactly which reconciliation rules a script must enforce (an expert at that task).
- The three signals the expertise classifier reads are how precisely the user frames directions, what
  they ask the agent to verify, and whether the user corrects the agent or the agent corrects the user.
- Expert sessions draw more work per instruction than novice ones: about 12 actions and 3,200 words per
  prompt against roughly five actions and 600 words. The gap appears within every kind of work and every
  band of task value, and survives a regression controlling for work mode, task value, month, occupation
  and model family at +9% actions and +13% output per expertise level, with standard errors clustered by
  user.
- Success is measured two ways from transcripts. *Judged success* comes from a classifier reading the
  full transcript; *verified success* additionally requires at least one hard verifiable signal — git
  commits or pull requests matching the work, passing test suites, or explicit user affirmation.
  Sessions judged to have no clear goal, about 7.7% of the sample, are excluded from the outcome
  analysis.
- Novice-rated sessions reach verified success 15% of the time and at least partial success 77% of the
  time; sessions rated intermediate or above reach verified success 28–33% of the time and partial
  success 91–92%. Most of the gain comes from moving novice to intermediate, with the slope decreasing
  between intermediate and expert.
- Among sessions that hit trouble — recorded failure signals such as errors, failed tests, repeated
  attempts, or user frustration — verified success rises from 4% for novice-rated sessions to 15% for
  expert-rated ones, and at least partial success from 60% to 80–81%.
- Sessions that are judged failures with zero lines of code written are counted as abandoned: 19% of
  novice-rated troubled sessions end that way against 5–7% for everyone else, which the authors read as
  part of the value of expertise being the ability to steer the agent rather than give up.
- Occupation separates outcomes much less than expertise does. People in software-related occupations
  reach verified success in about 30% of sessions against 26% for other professions, and in
  code-producing sessions 34% against 29%; under the looser measure both groups reach at least partial
  success in 89% and 88% of code-producing sessions. Every one of the ten largest occupations lands
  within seven points of software engineers.
- That five-point gap is reported as neither widening nor narrowing across the seven months observed,
  even as success rates rose in both groups. Management occupations score highest on verified success,
  slightly above software engineering — which the authors suggest may reflect transferable skills in
  directing an agent, but caution may partly reflect measurement, since verification rests partly on
  explicit confirmation in the transcript.
- Over the seven months, the share of sessions spent debugging fell by nearly half and usage shifted
  toward more end-to-end agentic work — deploying and running code, analyzing data, and writing non-code
  documents — while the estimated value of the typical task, derived by comparison with freelance job
  postings, rose about 25% on average.

## Notes

The authors state the findings are preliminary and name their limitations directly. Real-world outcomes
are not observed: the study cannot say whether code written in a session was used or discarded, or
whether it produced anything economically valuable. Non-interactive usage, described as a substantial
share of activity, is excluded entirely, and building a framework to measure it is named as a priority
for future work.

Every classification depends on a model reading a transcript. The authors report that their classifiers
track independent telemetry in the expected directions — more than 90% of sessions labelled as creating
or modifying code showed code changes in telemetry — and agree with a strong reference model on the
majority of sessions, while cautioning that classifiers remain hard to validate at scale and that these
sessions may be too long and complex for human labels to serve as ground truth. The expertise and
success measures are also correlational: the study addresses the worry that experts simply pick
different tasks by comparing sessions matched on work mode, estimated task value, month, subject and
broad occupation group, but this is a matching strategy rather than an experiment.

The report frames its own measures as instruments for tracking change rather than settled results,
naming two shifts it expects to watch: a fall in the returns to expertise, which would suggest models
are starting to supply judgment users currently bring, and continued growth in successful coding
sessions by people outside software occupations, which would suggest software production is becoming
part of ordinary work in every field. Examples in its classifier tables are drawn from a public dataset
of agentic coding sessions, [[Dataset/swe-chat]].
