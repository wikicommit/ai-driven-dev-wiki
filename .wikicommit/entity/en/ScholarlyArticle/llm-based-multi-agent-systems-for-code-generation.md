---
title: "LLM-Based Multi-Agent Systems for Code Generation: A Multi-Vocal Literature Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, multi-agent, surveys, code-generation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.16321'
    hash: sha256:02c42f738d81b8f2a6bc252e03f97ca3cafdfaffe66254423044bcd252353cbb
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A Multi-Vocal Literature Review of 114 academic and grey-literature studies on LLM-based multi-agent systems for code generation, synthesising nine categories of adoption motivation, the benchmarks and models in use, six categories of challenge and solution, and six categories of future research direction."
  author: ["Zeeshan Rasheed", "Muhammad Waseem", "Kai-Kristian Kemell", "Mika Saari", "Pekka Abrahamsson"]
  abstract: "Large Language Models have enabled multi-agent systems to perform autonomous code generation for complex tasks. Despite recent growth in research and industrial applications, there is little work synthesizing evidence from both academic and industrial sources. The authors conducted a Multi-Vocal Literature Review combining peer-reviewed studies and grey literature, selecting and reviewing 114 studies. The identified reasons for adopting multi-agent systems for code generation were classified into nine categories; the models and evaluation benchmarks used across the studies were systematically analyzed; the reported challenges and corresponding solutions were synthesized into six main categories and 26 subcategories; and future research directions were identified and organized into six main categories and 18 subcategories."
  keywords: ["Large Language Models", "Multi-Agent Systems", "Automation", "Multi-Vocal Literature Review"]
---

This review sets out to answer a question that a purely academic survey cannot: what does the
practitioner evidence say about multi-agent code generation, and does it agree with the research
literature? Its method is a Multi-Vocal Literature Review, which systematically analyses peer-reviewed
studies alongside grey literature — technical blogs, open-source repositories, industry reports — on
the argument, which the authors attribute to established MLR guidance, that grey literature should be
taken into consideration when a topic is fast-developing and strongly influenced by industrial
practice. The corpus is 114 studies, run through three phases: defining research questions and a
search string, conducting the peer-reviewed and grey-literature search, and performing data
extraction and analysis.

Seven research questions structure the results. They map the evidence base and its publication
trends, identify the motivations behind adoption, extract the evaluation benchmarks and metrics in
use, identify the language models employed, and then address the research gaps by analysing reported
challenges, the solutions proposed against them, and the future directions the literature names.

## Key Points

- The corpus splits 64.91% peer-reviewed to 35.09% grey literature. By affiliation across all 114
  studies, 57.02% are academic, 35.09% industry and 7.89% mixed academic-industry collaborations —
  a proportion the authors read as showing that cross-sector collaboration remains limited.
- The authors summarise the temporal pattern as academic attention arriving in 2024 and industry
  attention in 2025, with most peer-reviewed work appearing in conference venues and the grey
  literature largely industry-driven and mostly published as blogs.
- Among the grey literature, blogs account for 17 of 40 selected studies, which the authors read as
  evidence of an active role for practitioners and developers in documenting agent-based code
  generation techniques; arXiv is the most-used publication platform within that set.
- Twenty-nine of 114 studies (25.4%) state reasons for using multi-agent systems, yielding 36 reasons
  that thematic analysis groups into nine categories: operational efficiency and practical
  scalability, complex task handling, performance enhancement, context management, external tool
  integration, team collaboration, autonomous execution, adaptability, and future trends.
- Performance enhancement is the most frequently reported motivation (12 studies, 10.5%), followed by
  handling complex tasks through decomposition into smaller coordinated sub-tasks (9 studies, 7.9%)
  and operational efficiency and scalability (7 studies, 6.1%).
- The authors read the distribution of motivations as showing that multi-agent architectures are
  positioned mainly as a technical mechanism for accuracy, efficiency and workflow coordination,
  while adaptability, autonomous execution and long-term future-oriented development appear less
  often — aspects they describe as still emerging rather than central.
- Of 83 identified instances of LLM usage, 57 are closed-source and 26 open-source. OpenAI's GPT
  series accounts for 43 instances; among open-source models Meta's Llama is the most common at 17.
  The authors note that reliance on proprietary platforms may raise concerns about data privacy,
  security and dependency, and that open-source alternatives offer deployment control, cost
  efficiency and improved data privacy even where they do not match reported performance levels.
- Fifty-two of 114 studies (45.61%) use benchmarks to evaluate code generation capability, across a
  total of 37 distinct benchmarks.
- Correctness and reliability is the largest challenge category, reported by 26 studies (22.81%), led
  by hallucinations (10 studies), low accuracy (7), orchestration failure (5), lack of high-level
  planning (4), agent dependency (3), code inconsistency (2) and legacy code (1).
- Against orchestration failure the review reports structured and schema-based communication
  protocols — replacing unrestricted natural-language exchange with well-defined machine-readable
  message formats — plus dynamic communication structures and explicit assignment of responsibility
  for files, services or processes to prevent conflicts and non-terminating interactions.
- Security and privacy risk is reported by 11 studies (9.65%), led by privacy risks (4), then code
  vulnerabilities, code attacks and data leakage (3 each); the most commonly reported mitigations are
  isolated execution environments, monitoring across configuration files and generated code, and data
  protection measures such as data-loss prevention, audit logging and credential management.
- The other challenge categories it names are computational and resource constraints (cost,
  maintenance overhead, communication overhead), context and memory limitations (limited context
  window, short-term memory), benchmark challenges (limited real-world evaluation, limited language
  scope, security risk), verification challenges (non-deterministic behaviour, lack of human
  intervention, limited self-reflection, lack of task validation) and prompt design challenges
  (prompt sensitivity, prompt dependency, developer prompt interpretation).
- Advancing agent architecture and optimisation is the largest future-direction category (15 studies,
  13.16%), covering scalability, orchestration, edge deployment, parallel processing, fine-tuning,
  runtime stability and reinforcement-learning integration. Secure agents and advanced benchmarks
  follow at eight studies (7.02%) each, with smarter memory mechanisms at four (3.51%).
- On benchmarks the review argues for more realistic and multi-dimensional designs, including
  multi-modal benchmark construction, evaluation of safety, security and reliability, and assessment
  of collaborative capability across agents — coordination efficiency, communication effectiveness,
  task decomposition quality and reduction in human effort.

## Notes

The study is part of the MAISA project (2025–2027), funded by Business Finland, which investigates
the integration of LLM-based agents into software engineering and brings together academia with eight
Finnish companies; the authors describe the review as addressing that consortium's industry needs.

The authors publish a replication package containing study demographics, the extracted benchmarks and
models, and the categorised challenges, solutions and future directions, and refer readers to it for
more detailed descriptions than the paper itself carries.

Two limitations of the corpus are acknowledged in the paper's own framing. The distribution of
organisational affiliations is influenced by the review's focus on academic databases, where
industry-originating studies are less frequently indexed — so the industry share may understate
industrial activity rather than measure it.

See [[DefinedTerm/llm-based-multi-agent-system]] for the subject itself.
