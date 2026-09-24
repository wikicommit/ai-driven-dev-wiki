---
title: "An Empirical Study of Generative AI Adoption in Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [survey, software-engineering, productivity]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.23327'
    hash: sha256:e96130efa6c3fec92e1611bb4b52119c2083403c51be885038969af4caabfcfb
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A questionnaire survey of 204 software engineering practitioners from 37 countries on how generative AI tools are used in practice, the benefits and challenges they bring, how organizations institutionalize them, and what practitioners expect their long-term impact on the profession to be."
  author: ["Görkem Giray", "Onur Demirörs", "Marcos Kalinowski", "Daniel Mendez"]
  abstract: "The study surveys software engineering practitioners on four questions: the status of GenAI adoption, its benefits and challenges, the institutionalization of GenAI tools and techniques, and anticipated long-term impacts on SE professionals and the community. It reports wide adoption concentrated on implementation work, substantial perceived benefits alongside limited objective measurement, persistent challenges around unreliable output, prompting and validation, and an expectation that GenAI will redefine rather than replace practitioners' roles."
  keywords: ["Generative AI", "LLM", "Software Engineering", "AI4SE", "Survey"]
---

This paper sets out to give an overview of how generative AI (GenAI) is actually being adopted in software engineering, on the grounds that despite increasing adoption there is still little empirical evidence on how these tools are used in practice, what they deliver, what problems they introduce and what they mean for organizations and the profession. Its authors frame the existing literature as scattered across these technical, human and organizational factors, and position the study as a single investigation covering all SE knowledge areas, a wide range of GenAI tools, usage and non-usage, benefits and challenges, measurement, institutionalization and expected long-term impacts at once.

The method is an internationally distributed online questionnaire mixing closed and open questions, available to practitioners from May to November 2025. Of 223 responses, 204 were used, from 37 countries — the largest groups from the USA (24), Brazil (21) and Türkiye (19). Participants were reached through convenience, purposive and snowball sampling, with at most two invitations sent to the same organization and promotion stopped in a country once it had enough responses. Open-text answers were coded following grounded-theory procedures; reported SE activities were mapped onto the software life-cycle processes of ISO/IEC/IEEE 12207, and reported challenges onto the quality characteristics of ISO/IEC 25059:2023, the quality model for AI systems. Because the sample is non-probabilistic, percentages are reported with bootstrapped confidence intervals, which the authors stress describe within-sample rather than population-level variability.

The headline picture is of adoption that is already routine but weakly governed and weakly measured: practitioners report faster cycle times and better quality, but most do not measure either objectively, and organizations are far better at handing out tool access than at training, policy or objectives. The authors conclude that practitioners, organizations and governments need to move beyond ad-hoc adoption towards more systematic approaches.

## Key Points

- About 80% of respondents (79.44%) use GenAI tools in their SE activities; the rest do not use any.
- Among the 38 non-users who gave reasons, the most common barrier was lack of required skills or time constraints (23.34%), followed by no perceived need (21.31%) and insufficient maturity of GenAI tools, including mistrust in output quality (18.78%). The authors contrast this with other surveys that portray trust and accuracy as the dominant inhibitors, reading it as a skill gap among their non-users rather than a trust gap.
- Implementation — coding, code generation, code completion — is by far the most reported use (71.01%), followed by verification and validation (24.13%), a "Personal Assistance" category the authors created for brainstorming, knowledge search, learning and problem solving (22.73%), and maintenance (22.11%). Use in early life-cycle phases such as requirements, design and project planning is less common.
- General-purpose conversational assistants dominate: ChatGPT was reported by 62.38% of users, well ahead of Copilot (19.85%), Gemini (19.08%) and Claude (15.84%); internally developed tools were reported by 3.65%.
- Use is frequent: 51.9% of users use GenAI tools "all the time", 14.4% once a day and 25.3% a few times a week.
- The most reported benefit is reduced cycle time (54.42%), followed by quality improvement (34.67%), support for learning (18.12%) and support for problem solving (16.05%).
- Asked how long a task that used to take eight hours now takes with GenAI, 43.05% answered four hours and 26.61% two hours; about 95% reported a perceived productivity increase. 82% agreed that GenAI tools let them achieve better quality work.
- 58.15% of respondents stated they use no objective metric for size, productivity or quality. Those who do mostly use agile metrics — story points (19.10%) and velocity (12.07%) — which the authors note were not designed to capture AI-induced changes.
- The most reported challenge is inaccurate output, including hallucination (47.70%), followed by difficulty interacting with and prompting the tools (31.48%) and the burden of validating and reviewing their output (25.89%).
- 64.57% of respondents report that their organization supports GenAI tool use. Among those, providing access to tools is the most common form of support (81.06%), ahead of developing or customizing tools (50.72%), training (45.47%), published policies and guidelines (41.08%), dedicated GenAI experts (21.27%) and objectives or KPIs tied to GenAI use (19.08%).
- 79% expect GenAI to redefine rather than replace their role within five years, while 21% foresee a threat of complete role automation; 54% nonetheless expect the number of SE jobs to decrease, and 84% are confident they can acquire the skills needed to integrate GenAI into their work.
- Views on compensation are mixed (45% expect no negative impact, 31% expect downward pressure), and there is no consensus on whether GenAI will reduce social interaction in the workplace (41% agree, 37% disagree).

## Notes

The paper's recommendations follow from its measurement and institutionalization gaps. For researchers it calls for measurement frameworks tailored to GenAI-assisted SE, longitudinal studies linking governance maturity to measurable outcomes, and longitudinal studies of skill and workforce effects, particularly for early-career practitioners. For team leads it recommends lightweight before-and-after measurement — defect rates, code review turnaround, rework frequency — and structured peer learning or internal prompt libraries. For organizations it recommends treating GenAI governance as a strategic priority, and for policymakers and professional bodies, internationally coordinated regulation and competency frameworks that recognize GenAI literacy and prompt engineering as skills.

The authors are explicit about the limits of their data. The sample is non-probabilistic and the bootstrapped confidence intervals describe within-sample variability only, so they avoid further generalizability claims and call for replications. They also caution that the reported productivity and quality improvements are perceptions, which become more questionable given how few respondents measure either objectively. The questionnaire, collected data and analysis scripts are published in an open science repository, and the paper declares that Gemini, ChatGPT, Claude and NotebookLM were used in its writing process.

The version extracted here is arXiv:2512.23327v2 [cs.SE], stamped 1 April 2026. Its authors give affiliations at Eindhoven University of Technology, Izmir Institute of Technology, PUC-Rio, Blekinge Institute of Technology and fortiss.
