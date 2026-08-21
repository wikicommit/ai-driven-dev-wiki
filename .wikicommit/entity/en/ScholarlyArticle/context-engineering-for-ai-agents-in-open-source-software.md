---
title: "Context Engineering for AI Agents in Open-Source Software"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, context-engineering, configuration, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.21413'
    hash: sha256:7909394fa333078b9020474426f99bd50bbd8d63bcee81ee63930892a2f363a1
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A preliminary mining study of AI context files in open-source projects, finding only 5% adoption across 10,000 mature GitHub repositories and no established content structure in the AGENTS.md files it examined."
  author: ["Seyedmoein Mohsenimofidi", "Matthias Galster", "Christoph Treude", "Sebastian Baltes"]
  datePublished: "2026"
  abstract: "A preliminary study of the adoption of AI context files in 466 open-source software projects, analyzing what information developers provide in AGENTS.md files, how they present it, and how the files evolve over time."
  keywords: ["Software Engineering", "Generative AI", "AI Agents", "Open Source"]
---

"Context Engineering for AI Agents in Open-Source Software" is a preliminary empirical study by Seyedmoein Mohsenimofidi, Matthias Galster, Christoph Treude and Sebastian Baltes, published for the 23rd International Conference on Mining Software Repositories (MSR '26). Its subject is [[DefinedTerm/context-files]] as a new kind of software artifact, and its argument for studying them is methodological: because prompts are rarely preserved after content has been generated, versioned context files offer a rare chance to observe real-world [[DefinedTerm/context-engineering]] directly. The authors describe it as the first holistic empirical study analyzing context files used to guide different AI agents in open-source projects.

## Key Findings

**Adoption is early.** From a starting population of 228,890 non-forked, licensed, actively maintained GitHub repositories narrowed to 48,795 and then ranked down to a sample of 10,000 balancing popularity and maturity, only 466 — 5% — had adopted at least one of the four context-file formats the study scanned for (Copilot instructions, CLAUDE.md, AGENTS.md, GEMINI.md). The authors read this as an early stage of adoption and note their focus on four tools as a limitation. Among those 466, the language distribution roughly tracked the sample's overall composition, with Go slightly overrepresented: TypeScript led with 135 repositories, followed by Go and Python at 58 each, C# at 56, Java 36, JavaScript 34, C++ 32, Rust 29, PHP 19 and C 9. Certain formats clustered by language — C# repositories focused strongly on Copilot, while Claude Code was very popular for TypeScript — and the most common co-occurring pair was AGENTS.md with CLAUDE.md, in 25 repositories.

**File length varies most for AGENTS.md.** Copilot instruction files were longest on average (M = 310 lines, SD = 127), followed by CLAUDE.md (M = 287, SD = 112), with GEMINI.md shortest (M = 106, SD = 65). AGENTS.md averaged 142 lines but with a standard deviation of 231 — the highest variation of the four — which the authors suggest may reflect how much information developers choose to provide.

**There is no established content structure.** Analysing section headings from the 155 AGENTS.md files in the sample, the authors built a coding guide grouping semantically similar headings into categories. The most frequent were conventions (50 level-1 and level-2 headings), contribution guidelines (48), architecture or structure (47), build commands (40), then goals and purposes and test execution (32 each), metadata (29) and test strategy (24). Troubleshooting (8), patterns and examples (8) and security (6) were comparatively rare.

**Writing style splits five ways.** Examining all 50 sections labelled Conventions, the study characterises the writing along five stylistic dimensions, each illustrated from the corpus: *descriptive*, documenting existing practice without instruction ("This project uses the Linux Kernel Style Guideline"); *prescriptive*, direct imperatives ("Follow the existing code style and conventions"); *prohibitive*, stating what not to do ("Never commit directly to the main branch"); *explanatory*, adding a justification after a rule ("Avoid hard-coded waits to prevent timing issues in CI environments"); and *conditional*, encoding situational logic ("If you need to use reflection, use ReflectionUtils APIs"). The authors read this range as evidence that projects are still experimenting with how best to communicate expectations to agents.

**Most files are never revised.** Of the 155 AGENTS.md files, 77 (50%) had not been changed at all, 36 (23%) had been changed once, and 32 (21%) between two and seven times. The authors annotated 169 commits from the 10 files (6%) with at least ten commits, and found the dominant change categories to be adding instructions (78 occurrences) and modifying instructions (59), well ahead of adding sections (26), removing instructions (23) and modifying headings (23); removing sections and updating references occurred twice each. Most commits (111, or 66%) represented a single change category. For every file examined, adding or modifying instructions was the first or second change in its history, which the authors take as evidence that changes are mostly made to fine-tune and adjust instructions. Change tempo varied widely — one project made 49 changes over 19 days, another 11 changes over 148 days — and the authors state they identified no clear pattern in when or how often changes occur.

## Context

The paper's framing distinction is that prompt engineering concerns *how* a task is described to the model, while context engineering concerns *what* task-relevant information the model has access to — guidelines, configuration files, documentation, exemplary code snippets — which it defines as "the deliberate process of designing, structuring, and providing task-relevant information to LLMs". It argues that agent-based tools have an advantage over conversational ones precisely here, in allowing persistent, structured, task-specific context to be provided in a more fine-grained way.

Its conclusion is stated as a change in what developers are doing: in addition to READMEs for humans, "software developers are now writing and maintaining documentation for machines", and these files are versioned, reviewed, quality-assured and tested like any other artifact. The authors position open-source repositories as "natural laboratories" for studying how developers experiment with talking to agent-based tools, and set out open questions for future work — whether standard schemas could improve interoperability, whether a repository should maintain one context file or several, and how to coordinate instructions for multiple agents.

The study is explicitly preliminary and exploratory, with the authors stating they will extend it to answer their research questions more holistically. They also flag what they did not do: they did not label the intent behind a change, did not quantify changes per category, and did not analyse in detail the files with fewer than ten commits.
