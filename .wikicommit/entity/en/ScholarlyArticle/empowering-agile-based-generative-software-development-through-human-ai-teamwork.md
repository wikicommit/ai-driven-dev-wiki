---
title: "Empowering Agile-Based Generative Software Development through Human-AI Teamwork"
type: "schema:ScholarlyArticle"
lang: en
tags: [human-oversight, code-generation, software-process, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2407.15568'
    hash: sha256:3f6cdd2a21d8a672eee82d96802e4e5bae4cd18872ab60b3e3a9971595254f97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper from Tianjin University and CSIRO's Data61 proposing AgileGen, which uses Gherkin scenarios from behavior-driven development to complete the acceptance criteria missing from end users' requirements and involves the user in scenario decisions and iterative acceptance of generated web applications."
  author: ["Sai Zhang", "Zhenchang Xing", "Ronghui Guo", "Fangzhou Xu", "Lei Chen", "Zhaoyuan Zhang", "Xiaowang Zhang", "Zhiyong Feng", "Zhiqiang Zhuang"]
  keywords: ["Agile", "Human-AI Teamwork", "Generative Software Development", "User Requirement", "Gherkin"]
  abstract: "Raw requirements proposed by users are frequently incomplete. Recent methods following the top-down waterfall model use questioning for requirement completion, but users constrained by their domain knowledge fail to supply effective acceptance criteria, and cumulative errors of the waterfall model can make generated code diverge from requirements. The authors propose AgileGen, an agile-based generative software development approach through human-AI teamwork that initiates the end-user perspective to complete acceptance criteria, uses the Gherkin language as testable requirement descriptions bridging requirements and code, lets users take part in the decisions they do well, derives consistency factors from Gherkin to drive code generation, and introduces a memory pool that recommends past users' decision scenarios to new users with similar requirements. AgileGen is reported to outperform the best existing methods by 16.4% and to receive higher user satisfaction."
---

This paper, written as a manuscript submitted to ACM, addresses generative software development —
producing software directly from an end user's requirements — and starts from the observation that
such requirements are usually incomplete. It sorts existing agents into four categories: passive
agents that execute whatever users command, auto-thinking agents such as AutoGPT that decompose and
execute tasks autonomously, multi-agent collaboration agents such as
[[SoftwareApplication/metagpt]] and [[SoftwareApplication/chatdev]], and questioning agents such as
GPT-Engineer and gpt-pilot that ask users questions to expand requirements. The authors argue that
all of them lack acceptance criteria, that the waterfall-style agents let LLM hallucinations
accumulate from stage to stage, and that questioning agents demand domain knowledge end users often
lack.

Their proposal, [[SoftwareApplication/agilegen]], borrows from Agile methodologies and
behavior-driven development. From a one-line requirement it generates user scenarios in Gherkin,
the formal BDD language, which supply acceptance criteria; an interaction bridge translates the
scenarios into natural language so the user can confirm, add, delete or modify them, then
translates the decided scenarios back into Gherkin. Those scenarios guide visual design, the
generation of "consistency factors" — testable business-logic cases used to automatically revise
the generated code once — and code generation, after which the user tests the running prototype and
requests design or functional changes in further iterations. End users are thus placed at the two
ends of each iteration, with the agent handling the middle, and a memory pool stores past users'
decided scenarios and recommends them for similar new requirements.

Using web application development as the demonstration domain, the authors evaluate AgileGen on 30
projects from the open-source "50projects50days" collection plus 10 requirements written by
participants, and on 20 projects sampled from ChatDev's SRDD dataset, combining automatic metrics,
human ratings of executability and user experience, ablations and case studies. They report that
AgileGen outperforms the compared agents on CodeBLEU and Pass@1 and receives high user satisfaction.

## Key Points

- The paper classifies generative software development agents as passive, auto-thinking, multi-agent collaborative or questioning, and argues that all of them fail to capture acceptance criteria while completing user requirements.
- AgileGen completes acceptance criteria by generating Gherkin scenarios from the user's requirement, which the authors present as the first introduction of BDD concepts into generative agents for this task.
- Users take part in three decisions: proposing the requirement, deciding on the scenarios (confirm, add, delete or modify), and accepting the prototype or recommending changes.
- Consistency factors — business-logic test cases derived from the decided Gherkin scenarios — drive an automatic modification of the generated code before the user sees it.
- A memory pool records each requirement with the scenarios users decided on and supplies the most similar past entry, by Jaccard similarity above a 0.7 threshold, as an example for new scenario design.
- On the 30 "50projects50days" projects, AgileGen with GPT-3.5 reports 0.339 CodeBLEU and 62.5% Pass@1, which the authors state exceed the latest ChatDev version with GPT-3.5 by 0.089 and 16.4%; with GPT-4 it reports 0.362 and 71.5%.
- In human ratings of code executability, AgileGen's applications scored 2 on 45% and 3 on 50% of the "50projects50days" tasks, and 2 on 85% and 3 on 15% of the sampled SRDD tasks, with generation run without human interaction for fairness.
- In the ablation, removing the Gherkin scenario design lowers Pass@1 from 62.5% to 20.6%, and removing the consistency factor lowers it to 47.0%, which the authors read as the framework's design, rather than the base model, driving performance.

## Notes

The evaluation targets static web applications (HTML, CSS and JavaScript), though the authors state
the design is not limited to web development. The memory pool was deliberately left empty during
the experiments for fairness, so its effect on reducing user decision costs is not measured. In the
user-experience questionnaire the lowest-scoring dimension was novelty, which the authors attribute
to LLMs tending to generate common code they were trained on. Generated applications often rely on
placeholder multimedia because model-generated resource links fail, and the authors point to
user-supplied APIs and, for future work, the Cucumber tool for automated testing of the Gherkin
scenarios.
