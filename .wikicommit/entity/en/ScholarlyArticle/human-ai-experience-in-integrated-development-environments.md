---
title: "Human-AI Experience in Integrated Development Environments: A Systematic Literature Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [ide, surveys, human-ai-interaction]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2503.06195'
    hash: sha256:011a9a19088d9be5baec3768ee9867f029365ae36a53e3c32a2bb9ae60bbd2df
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A PRISMA-based systematic literature review of 90 studies on Human-AI Experience inside Integrated Development Environments, organising the field into three dimensions — Impact, Design and Quality — and analysing the study contexts, empirical methods and proposed future directions of the corpus."
  author: ["Agnia Sergeyuk", "Ilya Zakharov", "Ekaterina Koshchenko", "Maliheh Izadi"]
  abstract: "The review argues that research on Human-AI Experience in Integrated Development Environments (in-IDE HAX) remains fragmented and that a unified overview of current practices, challenges and opportunities is needed. It reviews 90 studies and organises their findings into Impact, Design and Quality: AI-assisted coding enhances developer productivity but introduces verification overhead and over-reliance; effective interfaces surface context, provide explanations and transparency, and support user control; and quality studies document risks in correctness, maintainability and security. Its research agenda calls for larger and longer evaluations, stronger audit and verification assets, broader coverage across the software life cycle, and adaptive assistance under user control."
  keywords: ["Human-Computer Interaction", "Artificial Intelligence", "Integrated Development Environment", "Programming", "User Studies", "User Experience"]
---

This paper is a systematic literature review of [[DefinedTerm/in-ide-hax]] — Human-AI Experience
inside Integrated Development Environments — conducted under the PRISMA framework for systematic
reviews and meta-analyses. It positions itself as the first systematic review of the topic,
distinguishing itself from existing reviews of large language models in software engineering on the
grounds that those summarise model capabilities, task coverage and evaluation techniques without
analysing the interaction experience inside developer workspaces. It extends an earlier
non-systematic survey by the same group, which covered 36 papers, in both scope and methodological
rigour.

The protocol restricted inclusion to English-language studies first publicly available between
January 2022 and November 2024, covering peer-reviewed journal articles and conference proceedings
plus preprints and unpublished dissertations where these offered unique relevant insights. The search
ran in November 2024 across the ACM Digital Library, DBLP, the IEEE Digital Library, ISI Web of
Science, ScienceDirect, Scopus, Springer Link and arXiv, using a two-part query pairing AI-assistant
and Human-AI terminology with IDE-related terms. Retained studies were scored on four quality
criteria — Reporting, Rigor, Credibility and Relevance — each on a 0 / 0.5 / 1 scale, with a cutoff
above 2 for inclusion. Of 223 papers entering screening, 30 were duplicates and 114 were out of
scope; 79 full-text articles were assessed for eligibility and 8 excluded on quality; backward
snowballing added 18 further in-scope papers, and a revision phase removed 2 and added 3, for a
final corpus of 90.

The review organises what those 90 papers found along three dimensions carried over from the earlier
survey's taxonomy — Impact (effects on developers, tasks and workflows), Design (how AI is integrated
into and interacted with in the IDE) and Quality (properties of AI outputs such as correctness,
security and readability) — and then analyses the corpus's study contexts, task types, empirical
methods, and the future work its papers propose.

## Key Points

- The corpus is heavily weighted toward Impact: 74 of the 90 studies address it, against 28 for
  Design and 19 for Quality. Impact-oriented studies report productivity improvements, especially
  among experienced users, alongside increased time spent verifying results and concerns about
  over-reliance.
- Research concentrates on professional settings (71 of 90) over educational ones (19 of 90), on the
  code implementation stage of the software development lifecycle, and on a single tool: GitHub
  Copilot is investigated in 36 of the 90 works. The review names this concentration as a risk of
  overgeneralisation, since findings may not translate to other AI-powered coding assistants.
- Within the professional subset, 46 of 71 studies do not specify a target lifecycle stage at all,
  evaluating AI tooling as general programming support. The review treats this missing stage
  information as a reporting gap that limits comparison, because the same interface may have
  different effects at requirements, implementation, testing or evolution.
- Design research converges on two interaction paradigms — autocompletion-based assistance and
  conversational agents — which the review presents as complementary rather than opposed, with
  studies advocating hybrid models that share context and allow movement between local edits and
  higher-level reasoning. It distils three recurring design principles from 17 of the 28 Design
  papers: context awareness, explainability and transparency, and user control and adaptability.
- Quality studies frame the central pattern as a trade-off between speed and assurance: AI-assisted
  coding accelerates workflows while increasing susceptibility to subtle errors, insecure patterns
  and reduced maintainability, with readability concerns arising from overly concise structures,
  unconventional variable naming and missing comments.
- The corpus's methods are 38 qualitative, 32 experimental and 12 survey-based, with 20 studies not
  fitting that dichotomy. The review reports interview sample sizes of 7 to 61 participants (median
  16), experimental designs of 17 to 214 (with two A/B studies far larger), and surveys of 68 to
  2,047 (median 507), and argues that sample sizes are often underpowered and rarely justified.
- Analysing 250 future-work statements extracted from the corpus yields 17 topics and 10
  methodological strategies. The most frequent topics are productivity factors (43), the design of AI
  assistance (29) and audits of AI-generated code (28); governance, user control and proactivity are
  the least frequent, at 3, 3 and 4 statements respectively.

## Notes

The review defines an IDE for its own purposes as any workspace that simultaneously offers code
editing, immediate execution or preview, and contextual AI feedback in the same window — a definition
that admits both traditional desktop IDEs and notebook-style environments while excluding tools that
push AI suggestions outside the primary editing surface. That scoping choice is also one of the
threats to validity the authors name: a recall-oriented query can bias the pool toward professional
contexts, because educational deployments do not always occur inside full IDEs.

The other stated threats are temporal bias from the 2022-2024 window, source reliability from
including non-peer-reviewed arXiv papers, interpretation bias in categorising a large corpus, and the
difficulty of conducting empirical work in industrial settings, where sponsors expect feedback within
one or two months. The authors make the full extraction table and search protocol available as
supplementary material, and their methodological recommendations include a priori power analysis for
confirmatory comparisons, preregistration where appropriate, and sharing versioned study materials.

The review also notes that a subset of its corpus conceptualises programming with AI as a form of
pair programming in which the AI acts as a collaborative partner rather than a tool, and treats that
framing as a growing trend in co-creative programming workflows.
