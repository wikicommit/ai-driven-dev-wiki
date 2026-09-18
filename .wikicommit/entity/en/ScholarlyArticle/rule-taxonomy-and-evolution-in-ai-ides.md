---
title: "Rule Taxonomy and Evolution in AI IDEs: A Mining and Survey Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-tools, context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A mixed-methods study of AI IDE rules that mines 7,310 rules from 83 open-source projects into a 5-by-25 category taxonomy, triangulates it against a 99-practitioner survey, and measures how software-artifact compliance changes after a rule is updated."
  author: ["Guangzong Cai", "Ruiyin Li", "Peng Liang", "Zengyang Li", "Mojtaba Shahin"]
  datePublished: "2026-06-10"
  keywords: ["AI IDEs", "Rules", "Prompt Engineering", "Agentic Coding"]
---

This study treats [[DefinedTerm/ai-ide-rules]] as a software artifact in its own right and asks two
questions about them: what categories they fall into, and how they evolve. Its motivation is that rules
are an emerging artifact whose taxonomy was either drawn from small samples or restricted to a single
IDE, and that nothing had examined what drives their change or whether changing them has any measurable
effect.

The method is mixed. On the mining side, the authors queried the GitHub Repository Search API using a
time-slicing strategy to work around its 1,000-result limit, filtered by inclusion and exclusion
keywords and by the presence of the relevant rule files, and manually verified that each remaining
project's README or description declared it was developed using an AI IDE. That yielded 83 projects
from an initial 25,587, containing 325 rule files from which 7,310 individual rules were segmented by
hand. On the survey side, they mined the email addresses of developers who had committed changes to
rule files between June 2025 and January 2026, dispatched a questionnaire in English and Chinese, and
after filtering screening failures and straight-lining responses retained 99 valid responses from 30
countries.

Three analyses follow. Open coding over the 7,310 rules produced a hierarchical taxonomy of 5 primary
and 25 secondary categories. Evolution analysis extracted 1,894 changed rules from the commit histories
of 117 rule files, retained 1,540 after discarding chore-only edits, and classified the drivers behind
a determinable subset of 504 of them into six reason categories. A longitudinal compliance assessment
then tracked how far software artifacts adhered to 160 rules across the five commits before and after
each rule change, using an LLM-as-a-judge pipeline validated against human labelling at each filtering
stage.

## Key Points

- The rule taxonomy has five primary categories — Architecture & Design, Code Implementation,
  Development Workflow & Project Management, Quality Assurance, and AI Collaboration Specifications —
  subdivided into 25 secondary ones.
- Mined rules are concentrated in the concrete categories: Code Implementation (26.28%) and Development
  Workflow & Project Management (25.96%) hold the most rules, while AI Collaboration Specifications
  holds the fewest (11.49%). Workflow Conventions is the single largest secondary category at 9.29%,
  followed by Testing Strategy at 8.76%.
- Surveyed developers rank the opposite way: Architecture & Design receives the highest mean importance
  rating (4.16 of 5) and Quality Assurance the lowest (3.79), despite the latter's high rule count. At
  the subcategory level the three highest-rated are System Architecture (4.25), Design References &
  Constraints (4.19) and AI Context Management (4.17); the first and third account for only 2.67% and
  1.76% of mined rules respectively, which is the contrast the paper's own discussion draws.
- The paper reports a statistically significant negative correlation between a subcategory's mean
  importance and its standard deviation, reading this as higher consensus on the rules developers rate
  most important — while noting it may be partly a ceiling effect of the 1–5 scale.
- Most developers do not write rules from scratch: 71.72% generate them with AI and then refine, and
  48.48% add rules only when the AI makes mistakes.
- Rules change frequently, and adding dominates: Added is the most frequent operation in most
  categories, typically 50–80%. Business Logic (39.42%) and Directory Structure (37.15%) have the
  highest change rates; Logging Standards (6.90%), Performance Optimization (6.97%) and Security
  Practices (7.24%) the lowest. Where those last two do change, deletion dominates — 65.22% and 61.90%
  respectively, with Performance Optimization showing a 0% modification rate.
- Mined commit evidence and surveyed self-report disagree on why rules change. In the mining data
  Expansion (29.17%) and Context Enrichment (26.59%) account for more than half of changes and
  Correction only 6.35%; in the survey, 77.78% of respondents name Correction as a primary trigger. The
  paper attributes the gap to a negativity bias — fixing AI errors leaves a stronger impression than
  routine expansion.
- Updating a rule raises the average compliance of software artifacts by 22.99%, from 49.14% to 72.13%,
  a change the paper reports as statistically significant. The effect is strongest for concrete,
  statically verifiable rules — Dependency Management gains 64.82%, Testing Strategy 52.73% — and
  weakest for abstract ones, with Project Documentation gaining 6.25% and System Architecture 3.33%.
- Compliance peaks at the commit that introduces the rule (76.03%) and declines over the following
  commits to around 65%, which the paper attributes to rule staleness and to growing context-window
  complexity.

## Notes

The paper's practitioner recommendations follow from the gaps it measures: delegate formatting and
syntax checking to conventional linters rather than spending context window on them; avoid abstract
natural-language statements of non-functional requirements, converting them into concrete code patterns
or leaving them to static analysis tools; regularly refactor and prune rule files rather than only
adding to them; and write rules with explicit trigger conditions tied to specific file paths or code
syntax rather than high-level statements.

Its recommendations to tool builders are the mirror image: automatically extract architectural
constraints from dependency graphs, abstract syntax trees and commit histories so that the high-level
rules developers value but rarely write get written; parse existing configuration files such as
`.eslintrc` or `tsconfig.json` into rule constraints instead of asking developers to duplicate them;
provide conflict detection and deduplication for rule files, since corrections accumulate as additions;
and decompose high-level developer intent into the low-level atomic constraints models actually follow.

The authors record threats to validity across four categories. On internal validity: the open coding
involves subjective judgment, mitigated by negotiated agreement between two coders; LLM-based filtering
risks hallucination, mitigated by an ensemble of three models with majority voting validated against
human ground truth; and the longitudinal compliance analysis observes temporal trends rather than
establishing causality, since an improvement could equally come from manual developer adjustments in
the same commit. On construct validity: repository identification relied on keyword matching, missing
projects that use AI IDEs without declaring it; rule segmentation introduces boundary ambiguity; and
the Likert scale risks a ceiling effect. On external validity: the dataset is predominantly TypeScript
and web-development projects built by solo developers or teams of one to three, so the findings may not
generalise to large-scale enterprise systems, and the ecosystem itself is changing rapidly. The
compliance sample carries a separate caveat, recorded under internal validity rather than external: it
was filtered down to 160 rules whose adherence an automated script could measure without false
positives, which the authors note leaves it dominated by statically verifiable categories such as
Directory Structure and Dependency Management, so the improvements may not generalise to more abstract
rules.
