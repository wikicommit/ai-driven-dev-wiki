---
title: "Refute-or-Promote: An Adversarial Stage-Gated Multi-Agent Review Methodology for High-Precision LLM-Assisted Defect Discovery"
type: "schema:ScholarlyArticle"
lang: en
tags: [security, multi-agent, adversarial-review, defect-discovery]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2604.19049'
    hash: sha256:8b98fff24a051f64694939444ff9377ab2d09dce06d28a0b01e64f0d4a393028
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A paper presenting Refute-or-Promote, an inference-time multi-agent review pattern that filters false positives out of LLM-assisted defect discovery through adversarial promotion gates, cold-start reviewers, cross-model critique and a mandatory empirical gate, evaluated by external acceptance of its findings over a 31-day campaign."
  author: ["Abhinav Agarwal"]
  datePublished: "2026-04-21"
  keywords: ["LLM-assisted defect discovery", "adversarial review", "multi-agent", "cross-model critic", "false positives"]
---

This paper starts from what it calls a precision crisis in LLM-assisted defect discovery: plausible-but-wrong reports overwhelm maintainers and degrade the credibility of real findings. Its answer is Refute-or-Promote, an inference-time reliability pattern that puts external structure around LLM agents so that their persistent false positives are filtered out before anything is reported.

The pattern combines Stratified Context Hunting (SCH) for generating candidates, adversarial "kill mandates" under which agents try to disprove a candidate at each promotion gate, context asymmetry, and a Cross-Model Critic (CMC). Cold-start reviewers are intended to reduce anchoring cascades, and review by a different model family is meant to catch correlated blind spots that same-family review misses. The author stresses that no vulnerability was discovered autonomously; the contribution is the filtering structure, and outcomes are evaluated by external acceptance rather than by benchmarks.

## Key Points

- Over a 31-day campaign across seven targets — security libraries, the ISO C++ standard and major compilers — the pipeline killed roughly 79% of 171 candidates before they advanced to disclosure; the paper labels this a retrospective aggregate.
- On a consolidated-protocol subset (lcms2 and wolfSSL, n=30) the prospective kill rate was 83%.
- Reported outcomes include 4 CVEs (3 public, 1 embargoed), an issue (LWG 4549) accepted into the C++ working paper, 5 merged C++ editorial PRs, 3 compiler conformance bugs, 8 merged security-related fixes without a CVE, an RFC 9000 erratum under committee review, and at least one FIPS 140-3 normative compliance issue under coordinated disclosure.
- The paper's most instructive failure: ten dedicated reviewers unanimously endorsed a non-existent Bleichenbacher padding oracle in OpenSSL's CMS module, which was killed only by a single empirical test — the motivation for making an empirical gate mandatory.
- As a preliminary transfer test beyond defect discovery, a simplified cross-family critique variant solved five previously unsolved SymPy instances on [[Dataset/swe-bench-verified]] and one SWE-rebench hard task.

## Notes

The results come from a single author's campaign over one month, and the headline kill rate is a retrospective aggregate, with the prospective figure measured on a 30-candidate subset. The unanimous-but-wrong endorsement episode is the paper's own argument for putting an empirical test, rather than agreement among LLM reviewers, at the final gate. The paper lists 10 pages and 3 tables, with artifacts published alongside it.
