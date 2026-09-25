---
title: "Human-In-the-Loop Software Development Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, human-oversight, multi-agent, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2411.12924'
    hash: sha256:50d1957ea820f6e5f810bb7b7dfbb7a37c553436a744ca397d1443636efc1a41
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing HULA, a human-in-the-loop LLM-based software development agent framework deployed in Atlassian JIRA, and evaluating it offline on benchmarks, online on real JIRA issues, and through a practitioner survey."
  author: ["Wannita Takerngsaksiri", "Jirat Pasuksmit", "Patanamon Thongtanunam", "Chakkrit Tantithamthavorn", "Ruixiong Zhang", "Fan Jiang", "Jing Li", "Evan Cook", "Kun Chen", "Ming Wu"]
  abstract: "LLM-based multi-agent paradigms for software engineering have been introduced to resolve software development tasks automatically, but existing work is evaluated on historical benchmark datasets, rarely considers human feedback at each stage of the automated software development process, and has not been deployed in practice. The authors introduce a Human-in-the-loop LLM-based Agents framework (HULA) for software development that allows software engineers to refine and guide LLMs when generating coding plans and source code for a given task, and design, implement and deploy it into Atlassian JIRA for internal uses. Through a multi-stage evaluation, Atlassian software engineers perceive that HULA can minimize the overall development time and effort, especially in initiating a coding plan and writing code for straightforward tasks, while challenges around code quality remain a concern in some cases."
---

This paper, a collaboration between Monash University, the University of Melbourne and
[[Organization/atlassian]], starts from three limitations the authors see in LLM-based software
development agents: they are evaluated on historical benchmark datasets of open-source projects,
they rarely take human feedback at each stage of the process, and they have not been deployed in
practice. Rather than aiming for full automation, the authors — noting that Atlassian values human
expertise and the ability of humans to rule AI agents — design an agent that works with the engineer
as an assistant.

The resulting framework, [[SoftwareApplication/hula]], has an AI Planner Agent, an AI Coding Agent
and a Human Agent (the engineer assigned the task) cooperate to turn a JIRA issue into a pull
request, with the engineer able to review, edit and regenerate the relevant files, the coding plan
and the code at each stage. The authors deployed it into Atlassian JIRA for internal use and
evaluated it in three stages: offline on SWE-bench Verified and an internal dataset of 369 JIRA
issues without human feedback, online on 663 real issues where engineers used it over two months,
and through a survey of practitioners who had used it.

The paper concludes that the level of detail in the input strongly affects performance, that human
feedback can enrich the input context and is beneficial in practice, and that practitioners see
HULA as reducing development time and effort, while code quality remains a concern and HULA still
struggles to produce perfect code without human input.

## Key Points

- Offline, HULA completed its generation workflow for 97% of SWE-bench Verified issues and 100% of the internal dataset.
- On SWE-bench Verified, the AI Planner Agent reached 86% average recall in file localization and perfect file localization for 84% of issues, and 31% of issues passed all unit tests; the authors describe this as comparable to the agent ranked sixth on the leaderboard as of 26 September 2024.
- On the internal dataset, file localization recall was 30% and 30% of issues had generated code rated highly similar to the human-written code; the authors attribute the gap partly to shorter issue descriptions (median 75 tokens against 295), more files changed per issue, and more languages and repositories.
- Because the internal dataset has no unit tests, code similarity was judged with GPT-4 as an LLM-as-a-judge, which the authors validated against engineers' scores on 203 issues with a correlation of 0.7.
- In the online deployment, coding plans were generated for 527 of 663 issues and engineers approved 433 of them (82%); code was generated for 376, pull requests were raised for 95 (25%), and 56 of those were merged (59%), so 8% of the issues that used HULA ended with a merged HULA-assisted pull request.
- In the survey of 109 practitioners, 61% agreed the generated code was easy to understand and modify and 41% that the generated plans aligned with the issue description, while 33% agreed the code solved their task without human involvement.
- Reported benefits included reduced development time and effort and help with simple tasks and with starting plans and code; reported challenges included incorrect or incomplete code and the effort needed to write detailed issue descriptions.
- The authors argue that evaluating functional correctness should go beyond passing unit tests, because tests are costly to prepare in an enterprise setting, give only a pass or fail, and show the presence of defects rather than their absence.

## Notes

The authors state that the findings are limited to Atlassian's internal use of JIRA and may not
generalize to other contexts, that the experiments use GPT-4 as the backbone model, and that some
implementation details could not be disclosed for confidentiality reasons. Among future directions
they ask what information an LLM-based software development agent needs in its input and how it
could be supplied automatically. The framework is a concrete instance of
[[DefinedTerm/human-in-the-loop]] design applied to coding agents, and the paper places it against
fully autonomous systems such as [[SoftwareApplication/swe-agent]] and
[[SoftwareApplication/autocoderover]]. Its evaluation uses [[Dataset/swe-bench-verified]] and
[[DefinedTerm/llm-as-a-judge]].
