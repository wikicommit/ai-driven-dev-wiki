---
title: "MarsCode Agent: AI-native Automated Bug Fixing"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, program-repair, multi-agent, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2409.00899'
    hash: sha256:2014b1e14f5cc4a5abb1174a2723cac2db5dc19b8d6647801539698c9f80a0ef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A ByteDance report introducing MarsCode Agent, an LLM-based framework that automatically identifies and repairs bugs through planning, bug reproduction, fault localization, candidate patch generation and validation, evaluated on SWE-bench Lite."
  author: ["Yizhou Liu", "Pengfei Gao", "Xinchen Wang", "Jie Liu", "Yexuan Shi", "Zhao Zhang", "Chao Peng"]
  abstract: "The authors introduce MarsCode Agent, a framework that leverages LLMs to automatically identify and repair bugs in software code, combining LLMs with code analysis techniques to localize faults and generate patches. The approach follows a systematic process of planning, bug reproduction, fault localization, candidate patch generation, and validation, and is evaluated on SWE-bench, where the authors report a high success rate in bug fixing compared to most existing automated approaches."
---

This report, written by researchers at ByteDance with a co-author from the Harbin Institute of
Technology (Shenzhen), introduces [[SoftwareApplication/marscode-agent]], a framework that uses
LLMs to automate bug fixing in real-world code repositories. The authors start from the observation
that fixing bugs in real projects requires understanding complex codebases, dependencies between
files and context-specific issues, and that developers' tasks — failing tests, output that does not
match expectations, feature extensions, simple defect fixes — cannot all be handled well by one
fixed approach.

Their answer is a multi-agent collaboration framework with six roles (Searcher, Planner,
Reproducer, Programmer, Tester and Editor), each given only the tools its task needs. The Planner
classifies each issue into either a dynamic debugging workflow, in which a reproduction script is
run in a Docker-based sandbox and the Programmer iterates until the Tester confirms the issue is
resolved, or a static repair workflow, in which the Editor generates several candidate fixes and a
vote selects one. Supporting this are code retrieval through a code knowledge graph and the
language server protocol, an edit tool called AutoDiff, and LSP-based static diagnostics of each
edit.

Evaluated on SWE-bench Lite, the report states that MarsCode Agent resolved 102 of the 300 issues
(34%), and it compares its file and code-snippet localization with other publicly traceable
solutions.

## Key Points

- The framework allocates a static or a dynamic solving pipeline to each issue according to its nature, instead of using one fixed approach for every issue.
- Agents are deliberately not given every tool: each role's toolset is limited to reduce the difficulty of each phase and improve stability.
- A code knowledge graph, built with program analysis over code and documentation, represents code entities as vertices and their relationships (calls, references, inheritance, file structure) as edges; the report states it supports 12 programming languages.
- LSP-based retrieval is added to cover definitions outside the target project and same-named entities, with fuzzy positioning because the agent's numerical positioning is weak.
- The authors report that asking LLMs for unified diffs, for start and end line numbers, or for whole-file rewrites all failed or were impractical in their experience, which led to the AutoDiff edit format modelled on Aider's approach.
- On SWE-bench Lite, the report states 102 of 300 issues resolved (34%), correct file localization in 265 of 300 (88.3%) and correct code-snippet localization in 206 of 300 (68.7%).
- 84 of 300 issues (28%) were judged suitable for dynamic solving and 216 (72%) for static solving; dynamic debugging resolved 32 of 84 (38.1%) and static repair 70 of 216 (32.4%), which the authors attribute to the reproduction and verification steps in dynamic debugging.

## Notes

The evaluation is confined to SWE-bench Lite, a 300-instance subset of [[Dataset/swe-bench]]. The
report's own results table lists the share of issues that progressed to static repair as 202 of 300
(72.0%), while its analysis gives 216 of 300; the resolution figures above are the ones stated in
the text. The authors list future work on reducing LLM call costs, improving user-agent
collaboration, supporting dynamic debugging within real user workspaces to avoid environmental
contamination, and improving the accuracy of error localization and code modification. The work
belongs to the line of LLM-based [[DefinedTerm/automated-program-repair]] and
[[DefinedTerm/software-issue-resolution]] systems, and the report situates it alongside
[[SoftwareApplication/swe-agent]], [[SoftwareApplication/autocoderover]] and
[[DefinedTerm/agentless]].
