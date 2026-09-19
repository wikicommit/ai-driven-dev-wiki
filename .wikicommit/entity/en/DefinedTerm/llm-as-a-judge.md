---
title: "LLM-as-a-Judge"
type: "schema:DefinedTerm"
lang: en
aliases: ["LLM-as-Judge"]
tags: [agents, llm, code-quality]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:9d24a3bfa582cdeb35b5470314362e43ded1cceb6659830329c69fe72147a2e4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Having a separate model instance evaluate another's output against explicit rubrics and evidence, rather than accepting the output as produced — used in agent workflows as a quality gate between steps."
---

LLM-as-a-Judge is the practice of having a model evaluate output rather than produce it: a separate
instance scores or verifies work against structured rubrics, with the scoring expected to cite
evidence rather than assert a verdict. In agent workflows it is used as a gate between steps, where
a judge that withholds a pass sends the work back instead of letting it continue. The account below
is of how [[SoftwareApplication/context-engineering-kit]] applies the technique; that project treats
it as drawn from published research on evaluation patterns rather than as its own invention.

## Usage

The kit uses judging at two scales. As a quality gate it evaluates each planning and implementation
step of [[DefinedTerm/spec-driven-development]] against predefined verification rubrics before the
next step begins. As an execution primitive in
[[DefinedTerm/subagent-driven-development]] it appears in several forms: a judge run over finished
work with a structured rubric and evidence-based scoring; an independent judge paired with an
implementation sub-agent in a retry loop that repeats until the work passes; several judges in
iterative debate, which either build a consensus or report the disagreement rather than forcing one;
and a meta-judge sub-agent, used alongside judge sub-agents to generate specification material on
the fly. What the project asks of a judge in each case is
the same — a decision traceable to evidence and a rubric, not an opinion.

Independence is the property the arrangement depends on. The judge is described as separate from the
sub-agent that did the work, which is what makes the verdict worth more than the producing agent's
own confidence.

[[ScholarlyArticle/from-determinism-to-delegation]] places the technique in a wider evaluation
practice, alongside trajectory evaluation — which asks whether the agent chose a correct sequence of
tools even when the final answer varies — and semantic similarity against golden datasets. Its argument
for why any of this matters is that where evaluation is an afterthought in classical practice, it is
the central artifact in agentic practice, because outputs are non-deterministic and quality has to be
established through curated evaluation datasets, adversarial edge cases included, and automated grading.

A second account, from a production system rather than a toolkit,
[[BlogPosting/how-we-built-our-multi-agent-research-system]], describes what Anthropic's Research team
graded and how. Its reason for reaching for a judge at all is that research outputs are free-form text
that rarely has a single correct answer, so they resist programmatic evaluation. Its rubric had five
criteria — factual accuracy (do claims match sources?), citation accuracy (do the cited sources match
the claims?), completeness (are all requested aspects covered?), source quality (were primary sources
preferred over lower-quality secondary ones?) and tool efficiency (were the right tools used a
reasonable number of times?).

That team's reported finding about judge *structure* runs against the intuition that more judges are
better. It experimented with multiple judges evaluating separate components and found that a single
LLM call with a single prompt, emitting a score from 0.0 to 1.0 together with a pass-fail grade, was
the most consistent and aligned with human judgement. The approach is described as especially
effective where a test case does have a clear answer, so the judge is checking correctness rather than
forming an opinion — which is the same precondition the rubric requirement below states.

The same post is explicit that the technique does not stand alone. It reports human testers catching
what the automated evaluation missed, including a consistent tendency in early agents to choose
SEO-optimized content farms over authoritative but less highly-ranked sources such as academic PDFs or
personal blogs; the team resolved it by adding source quality heuristics to the research agents'
prompts. Its general position is that manual testing remains essential even where automated evaluation
is in place, because people testing agents find edge cases evals miss.

## When It Applies

It applies where the quality being checked can be written down as a rubric before the work is seen —
acceptance criteria, verification steps, review dimensions. Where the standard cannot be stated in
advance, there is nothing for a judge to score against, and the pattern degrades into asking a model
whether it likes the result.

The kit's guidance on evaluating agent systems lists LLM-as-a-Judge alongside multi-dimensional
rubrics and bias mitigation, without saying whose bias is at stake; where the kit does name a
direction, it is the judge sub-agent that mitigates bias in the work under review. Read the
strongest claims made for it with that in mind — the
project states that judge-based quality gates fully eliminate cases where an agent produces
non-working or incorrect solutions, which is its own assessment of its own tooling, based on
internal production use rather than independent evaluation, and stronger than the surrounding
material supports.

An independent source is blunter about the limits. [[ScholarlyArticle/from-determinism-to-delegation]]
states that the dominant grading mechanism is itself imperfect and that rigour requires acknowledging
it: surveys and empirical studies document systematic biases in LLM judges — position, verbosity and
self-preference among them — and judge choice can reorder model rankings. Using a model to grade models
therefore introduces a circularity that calibration, reference anchoring and judge ensembling only
partially mitigate. That paper's conclusion is that robustness must be quantified through testing,
evaluation, verification and validation frameworks that exceed static accuracy and evaluate reaction to
data, model and intent drift, and it lists evaluation validity among its open problems — establishing
construct-valid, reproducible, contamination-resistant evaluations for open-ended tasks, and avoiding
trajectory metrics that reward spurious tool sequences.

## Related Terms

- [[DefinedTerm/subagent-driven-development]] — where judging is used as an execution primitive
- [[DefinedTerm/spec-driven-development]] — where it is used as a phase gate
- [[ScholarlyArticle/from-determinism-to-delegation]] — source of the documented judge biases and the
  circularity caution above
- [[DefinedTerm/trajectory-evaluation]] — the complementary technique that paper names beside it
