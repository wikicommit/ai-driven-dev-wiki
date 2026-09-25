---
title: "SWE-bench Multimodal: Do AI Systems Generalize to Visual Software Domains?"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, coding-agents, multimodal]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.03859'
    hash: sha256:964b7d943c0765ada1470231e72a7d8173927be5bc04def7158213ddca7a6fa5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing SWE-bench Multimodal, a benchmark of visual, user-facing JavaScript bug-fixing tasks, and using it to test whether systems built for the Python-only SWE-bench generalize to other languages and to problems that include images."
  author: ["John Yang", "Carlos E. Jimenez", "Alex L. Zhang", "Kilian Lieret", "Joyce Yang", "Xindi Wu", "Ori Press", "Niklas Muennighoff", "Gabriel Synnaeve", "Karthik R. Narasimhan", "Diyi Yang", "Sida I. Wang", "Ofir Press"]
  abstract: "Autonomous software engineering systems are commonly evaluated on SWE-bench, which uses only Python repositories with problem statements presented predominantly as text. The authors propose SWE-bench Multimodal (SWE-bench M) to evaluate systems on their ability to fix bugs in visual, user-facing JavaScript software, with task instances collected from JavaScript libraries for web interface design, diagramming, data visualization, syntax highlighting and interactive mapping, each containing at least one image in its problem statement or unit tests. They find that top-performing SWE-bench systems struggle with SWE-bench M, revealing limitations in visual problem-solving and cross-language generalization, and that SWE-agent's flexible language-agnostic features let it substantially outperform alternatives, resolving 12% of task instances compared to 6% for the next best system."
---

This paper, by authors from Stanford University, Princeton University, Cornell University, the
University of Tübingen and Meta AI, asks whether AI systems for software engineering generalize
beyond the setting they are usually evaluated in. [[Dataset/swe-bench]] draws only on Python
repositories, and the paper notes that only 5.6% of its tasks contain an image, even though many
domains of software development — user interface design, games, data visualization — rely on
visual assets. To probe this, the authors build [[Dataset/swe-bench-multimodal]] (SWE-bench M):
real GitHub issues from user-facing JavaScript libraries, filtered so that every task has an image
or video in its problem statement or tests, and checked by human annotators.

The authors then try to run the top open-source systems from the SWE-bench leaderboard on it. Some
proved so tailored to Python and SWE-bench that they could not be adapted: AutoCodeRover and
Moatless rely on Python-specific program analysis, and the authors chose not to benchmark them,
while Agentless needed a JavaScript parser written from scratch. They evaluate RAG, three
configurations of [[SoftwareApplication/swe-agent]] (Base, a JavaScript-adapted editor, and a
multimodal version with a browser, screenshots and image viewing) and their adapted
Agentless JS, with GPT-4o and Claude 3.5 Sonnet.

The interactive SWE-agent configurations clearly outperform the others, and the paper draws a
design conclusion from this: generalizable LM-based systems for software engineering should
emphasize interaction rather than fixed problem-solving workflows, leaving the burden of problem
solving on the LM instead of manually engineered, language-specific pipelines.

## Key Points

- SWE-bench M contains 619 task instances from 17 JavaScript repositories, split into a 517-instance test set from 12 repositories and a 102-instance development set from 5 repositories (the abstract states 617 instances).
- Human annotators judged the images necessary for solving the task in 83.5% of the 557 instances whose problem statements contain images.
- Annotators estimated that SWE-bench M tasks take longer to solve than SWE-bench tasks, and its reference solutions edit more files, functions and lines; 28% of them modify two or more file types.
- Several leading SWE-bench systems could not be adapted without extensive redesign, because their localization steps depend on Python-only parsing; the paper argues that such rigid workflows fail under minor distribution shifts.
- On the test set the SWE-agent configurations resolve 9.2–12.2% of tasks, against 3.1–6.2% for Agentless JS and 5.0–6.0% for RAG.
- Swapping the underlying LM, or adding JavaScript-specific and multimodal tooling to SWE-agent, made little difference to overall resolution in the main results, and the authors describe the effect of the multimodal tools as ambiguous overall.
- Removing images from the input lowered performance for both RAG and SWE-agent JS on the development set, especially where annotators judged the images necessary.
- A temporal analysis found no evidence that solutions leaked into the models' training data gave an advantage on the test set.

## Notes

The paper's related-work section places SWE-bench M at the meeting point of repository-level
software engineering benchmarks and multimodal code generation, and argues that web navigation and
software engineering agents have usually been studied separately. The authors list as limitations
that the benchmark covers only JavaScript, only images and videos among possible media, and a
limited set of domains, and that adding tasks was labor-intensive. They also ask practitioners to
iterate on the development split and evaluate on the test split only once an approach is final.
The multimodal SWE-agent extends the [[DefinedTerm/agent-computer-interface]] idea with browser
and image tools.
