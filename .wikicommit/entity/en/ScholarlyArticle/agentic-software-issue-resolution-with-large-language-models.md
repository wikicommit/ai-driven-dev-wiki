---
title: "Agentic Software Issue Resolution with Large Language Models: A Survey"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, surveys, evaluation, reinforcement-learning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.22256'
    hash: sha256:9a5a75e55b1a5f5818704198234c0c775aeeaaf8ae884348416af572766c9cd2
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A systematic survey of 242 papers on LLM-based agentic software issue resolution, modelling the task as five logical phases and building taxonomies across benchmarks, techniques and empirical studies. It documents the field's shift from scaffold design toward training domain-specific models with reinforcement learning, and argues that reported resolution rates overstate real capability."
  author: ["Zhonghao Jiang", "David Lo", "Zhongxin Liu"]
  abstract: "The survey treats software issue resolution — addressing real-world issues in software repositories from natural-language descriptions — as a task in its own right rather than a sub-case of automated program repair or repository-level code generation. It outlines the task's general workflow and establishes a taxonomy across three dimensions: benchmarks, techniques and empirical studies. It highlights how reinforcement learning has become an increasingly important training paradigm for agentic systems in software engineering, and summarises key challenges and promising future directions."
---

This survey reviews LLM-based agentic systems for **software issue resolution** — understanding,
locating and resolving issues in real code repositories from developers' natural-language
descriptions. Its stated case for treating the task on its own terms is that existing surveys divide
issue-resolution research into pre-existing areas such as automated program repair, whereas issue
resolution covers more diverse maintenance activities, including efficiency optimisation and feature
addition, and — even for bug-fixing issues — does not assume the existence of tests that can trigger
the bug. The authors also argue that existing surveys missed a recent paradigm shift, from
prompt-engineering-based scaffold design toward training dedicated models.

The corpus was built by seeding search strings from papers submitted to a public leaderboard, then
searching IEEE Xplore, the ACM Digital Library, arXiv and DBLP with four query combinations pairing
software-engineering terms with AI terms. That returned 5,176 raw hits, reduced to 1,238 by
deduplication and venue filtering, to 278 by inclusion and exclusion criteria applied independently
by two authors under a conservative union rule, and to 235 by type-adapted quality assessment;
backward and forward snowballing added 7 more, for a final set of 242 papers spanning October 2023 to
May 2026. Taxonomies were constructed by open coding, deriving each from 70% of the relevant papers
and independently labelling the rest, with reported inter-rater agreement of 0.87, 0.90 and 0.91 for
the benchmark, technique and empirical-study taxonomies.

The survey's organising device is a five-phase model of the task — repo preprocessing, localization,
repair, patch validation and patch selection — which it describes as logical functions rather than a
fixed execution order, so that a system may execute them sequentially or interleave them dynamically.
Each technique is then placed against the phase it addresses.

## Key Points

- The survey divides agentic systems by how their control flow is designed: in **pipelines**, human
  designers predefine the control flow as staged steps or state-machine-like workflows and the model
  performs the assigned subtask at each stage; in **agents**, the model determines the next action
  during execution from environmental feedback, so the control flow emerges dynamically. Pipelines
  emphasise determinism and controllability, agents offer greater autonomy and flexibility.
- On cost, it reports that under matched settings — same benchmark, same backbone — pipeline-based
  methods deliver comparable effectiveness at lower and more predictable cost, because a pipeline
  bounds the number of model calls per phase while an agent trajectory accumulates context over
  multiple rounds of tool interaction. It cautions that the highest reported resolved rates come from
  agent-based scaffolds that also adopt the strongest and most recent backbones, so scaffold type and
  backbone capability are confounded in those numbers.
- It documents a training-driven paradigm shift with two figures: the number of training studies grew
  11.4-fold since February 2025 against 3.1-fold for scaffold-design studies, and reinforcement
  learning is used by none of the four representative models released before February 2025 but by 24
  of the 39 released between then and May 2026.
- It separates reinforcement-learning approaches by reward type. **Outcome reward models** execute a
  rollout's patch against fail-to-pass and pass-to-pass tests and use the binary result as the reward
  for the whole trajectory, which scales because outcomes are automatically verifiable but is only as
  reliable as the underlying test oracle. **Process reward models** reward intermediate states or
  actions, giving finer credit assignment, but the survey notes their adoption lags far behind
  because intermediate correctness has no execution oracle and must itself be approximated by rules
  or a learned critic.
- Benchmark validity is treated as a first-class concern. The survey distinguishes raw benchmarks
  built from unfiltered pull requests, which are closer to real development but where issue
  descriptions may leak their own solutions and overly broad test suites may pass incorrect patches,
  from human-filtered benchmarks, which alleviate this but discard the harder, more ambiguous
  instances. It recommends raw benchmarks for robustness evaluation and filtered ones for reliable
  comparison across models and methods, and static benchmarks for method comparison under a stable
  protocol against dynamic ones for assessing the latest models where contamination is the primary
  concern.
- It reports that evaluation across the surveyed papers is almost exclusively automatic, that
  end-to-end evaluation is entirely execution-based, and that 76.4% of the papers report a
  resolved-percentage metric, making it the most common single measure for the task. Localization is
  evaluated exclusively with match-based metrics, and statistics-based metrics such as token count,
  cost and time serve only as complements — which the survey reads as current practice prioritising
  effectiveness over efficiency.
- Its synthesis of empirical studies concludes that reported resolution rates support controlled
  comparison but do not certify practical capability, because weak tests, contamination, unrealistic
  task framing and unreliable trajectories can each make a resolved instance overstate real ability;
  and that performance variation is driven more by information access, control design and recurrent
  process-level failures than by the backbone model alone.
- The survey ranks its open challenges by how many of the 242 papers explicitly raise each: training
  domain-specific models (65 papers, 26.9%), repository knowledge representation (60, 24.8%) and
  validation via tests (49, 20.2%) lead, while the two evaluation-related challenges are raised by 37
  and 25 papers. The authors treat that gap between limited attention and foundational importance as
  a finding in its own right, since unreliable evaluation makes progress on the other challenges hard
  to assess.

## Notes

The authors name two threats to validity. Internally, manual screening and classification involve
subjective judgement, which they mitigate with independent application of the criteria by two
authors, reported Cohen's kappa at each independent stage, adjudication by a third author, and public
release of the paper lists from every filtering stage. Externally, they note that 50.8% of the
collected papers are arXiv preprints that have not undergone peer review, and report that
reconstructing the taxonomy from the peer-reviewed subset alone leaves the top-level taxonomy
unchanged. They also treat their conclusions as a snapshot as of the collection cut-off, given how
quickly the area moves.

Among the directions the survey proposes is **software engineering for agentic systems**: extending
testing, debugging, versioning and continuous integration to agent lifecycles, and porting classical
debugging techniques to agent trajectories — counterfactual replay that intervenes on a single step
and re-executes the remainder in the spirit of delta debugging, statistics over large collections of
successful and failed trajectories to rank suspicious action patterns after the manner of
spectrum-based fault localization, and process invariants mined from normal runs that can be
monitored at runtime to abort abnormal executions early.
