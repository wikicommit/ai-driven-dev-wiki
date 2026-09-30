---
title: "Evaluation and Benchmarking of LLM Agents: A Survey"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, benchmarks, llm-agents, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2507.21504'
    hash: sha256:00c97fd4811938adb164dd79970d37227699e3c856283d589154116bb4e78ae6
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A KDD '25 survey from SAP Labs that organizes LLM agent evaluation along two dimensions — what to evaluate and how to evaluate — and highlights enterprise-specific evaluation challenges such as role-based access, reliability guarantees, long-horizon interactions and compliance."
  author: ["Mahmoud Mohammadi", "Yipeng Li", "Jane Lo", "Wendy Yip"]
  datePublished: "2025"
  keywords: ["LLM agents", "agent evaluation", "evaluation taxonomy", "agent behavior", "benchmarks", "safety", "enterprise AI"]
---

This survey, by authors at SAP Labs and published in the proceedings of KDD '25, sets out to bring
clarity to the fragmented landscape of LLM agent evaluation. The authors argue that evaluating an
agent is harder than evaluating an LLM in isolation, because agents reason, plan, execute tools, use
memory and collaborate with humans or other agents in dynamic environments — in their analogy, LLM
evaluation examines an engine while agent evaluation assesses the whole car under various driving
conditions — and that it also differs from traditional software testing, since agents behave
probabilistically rather than deterministically.

Their main contribution is a two-dimensional taxonomy. The **evaluation objectives** dimension (what to
evaluate) covers agent behavior (task completion, output quality, latency and cost), agent capabilities
(tool use, planning and reasoning, memory and context retention, multi-agent collaboration),
reliability (consistency and robustness) and safety and alignment (fairness, harm, toxicity and bias,
compliance and privacy). The **evaluation process** dimension (how to evaluate) covers interaction mode
(static and offline versus dynamic and online), evaluation data (datasets, benchmarks and
leaderboards), metrics computation methods (code-based, [[DefinedTerm/llm-as-a-judge]] and
[[DefinedTerm/agent-as-a-judge]], and human-in-the-loop), evaluation tooling, and evaluation contexts
ranging from mocked APIs and sandboxes to live deployment. For each category the survey lists
representative metrics and benchmarks, such as success rate, [[DefinedTerm/pass-at-k]] and
[[DefinedTerm/pass-hat-k]], tool selection accuracy, and benchmarks including [[Dataset/swe-bench]],
[[Dataset/tau-bench]] and [[Dataset/agentdojo]].

## Key Points

- The survey proposes organizing agent evaluation along two axes: evaluation objectives (what to
  evaluate) and evaluation process (how to evaluate).
- It treats task completion as a predominant measure of overall agent performance, while noting that it
  can give limited fine-grained insight into failures when most models achieve low success rates.
- For consistency it contrasts pass@k, the probability of succeeding at least once in k attempts, with
  the stricter pass^k from τ-bench, which requires success in all k attempts and which the authors say
  better captures the consistency requirements of mission-critical deployments.
- It notes that checking tool calls only for abstract-syntax-tree correctness can miss semantic errors
  such as hallucinated parameter values, and points to execution-based evaluation as a more grounded
  alternative.
- It characterizes code-based metric computation as the most deterministic and reproducible but
  inflexible for open-ended output, LLM-as-a-judge as scalable for subjective tasks, and
  human-in-the-loop evaluation as the gold standard for subjective and safety-critical judgments but
  expensive and hard to scale.
- It identifies enterprise-specific challenges often overlooked in research: evaluating agents under
  role-based access control, providing reliability guarantees despite stochastic behavior and the cost
  of repeated trials, assessing dynamic and long-horizon interactions, and verifying adherence to
  domain-specific policies and regulations.
- It names four future research directions: holistic evaluation frameworks, more realistic evaluation
  settings, automated and scalable evaluation techniques, and time- and cost-bounded evaluation
  protocols.

## Notes

The survey also describes Evaluation-driven Development, proposed in other work it cites, in which
evaluation is made an integral, continuous part of the agent development cycle both offline and online,
with an AgentOps component monitoring deployed agents. The paper states that it is licensed under a
Creative Commons Attribution 4.0 International License.
