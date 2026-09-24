---
title: "Vibe coding: programming through conversation with artificial intelligence"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, ai-assisted-programming, empirical-study, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2506.23253'
    hash: sha256:7d7ba02b9f8314bc08e972beb8a33d6aaaa26d4e697a4b41a334c3d682890e68
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A PPIG 2025 paper presenting what its authors call the first empirical study of vibe coding, based on a framework analysis of about 8.5 hours of think-aloud vibe coding videos from YouTube and Twitch."
  author: ["Advait Sarkar", "Ian Drosos"]
  datePublished: "2025"
  keywords: ["[[DefinedTerm/vibe-coding]]", "[[DefinedTerm/material-disengagement]]", "[[DefinedTerm/context-momentum]]", "framework analysis", "think-aloud"]
  citation: "Sarkar, Advait, and Drosos, Ian. 2025. Vibe coding: programming through conversation with artificial intelligence. In Proceedings of the 36th Annual Conference of the Psychology of Programming Interest Group (PPIG 2025)."
---

A paper by Advait Sarkar and Ian Drosos, published in the Proceedings of the 36th Annual Conference of the Psychology of Programming Interest Group (PPIG 2025), which presents itself as the first empirical study of [[DefinedTerm/vibe-coding]]. The authors take vibe coding to be an emerging paradigm in which developers primarily write code by interacting with code-generating large language models rather than writing it directly, and trace the term to Andrej Karpathy's February 2025 post, which they call "the Karpathy canon". Because the practice is still being negotiated by the community, the only criterion they use to identify it is that the programmer describes their own activity as vibe coding.

The data are think-aloud videos of vibe coding sessions from YouTube and Twitch. Searches for "vibe coding" and "vibe coding session" between 17 March and 2 April 2025 produced a longlist of 35 videos (about 35 hours and 46 minutes). Two researchers used four of them to develop an analysis framework and four inclusion criteria — capturing much of the workflow, few timeline edits, rich think-aloud reflection, and a project with some realism or seriousness. Six videos met all four criteria; one was withdrawn from Twitch in the meantime, leaving five videos of about 8 hours and 27 minutes, two of which were parts of one project and were analysed together. The framework analysis used nine top-level categories — goals, intentions, workflow, prompting, debugging, challenges, expertise, trust, and definition and performance — organised into 20 subcategories.

The paper's overall claim is that vibe coding does not remove the need for programming expertise but redistributes it, and that it is an early instance of what the authors call [[DefinedTerm/material-disengagement]]: practitioners orchestrate the production of code through an AI intermediary while keeping selective, strategic oversight.

## Key Points

- Vibe coding follows what the authors describe as iterative goal satisfaction cycles: formulate a goal or sub-goal, prompt the model, review the generated code, accept or reject it, test it in the application, identify bugs or improvements, then refine the prompt or switch to manual debugging and editing — repeating until the sub-goal is satisfied or abandoned.
- Prompts mix vague, high-level directives (including aesthetic or subjective descriptions) with detailed technical specifications, and a single prompt can carry several unrelated objectives at different levels of detail.
- Typed text was the main input mode despite the Karpathy canon's emphasis on voice; transcribed speech and screenshots were also used.
- Debugging stayed a hybrid of AI assistance and conventional techniques such as reading error messages, using browser developer tools, forming hypotheses and inspecting code; pasting errors to the model sometimes replaced manual debugging altogether.
- Code review during vibe coding was rapid and impressionistic — scanning diffs by the size and shape of the highlighted changes, and looking for key identifiers — rather than line-by-line reading.
- Expertise was redirected rather than replaced: toward context management, rapid code evaluation, and deciding when to switch between prompting and manual work. Besides programming expertise, the programmers drew on AI expertise and product-management expertise.
- The authors name [[DefinedTerm/context-momentum]]: earlier prompts and the model's interpretations of them steer later generation, creating path dependence that can be hard to escape but can also spark new goals.
- Trust in the tools was granular, dynamic and contingent, built through repeated verification rather than blanket acceptance; lightweight code review was observed across all participants.
- The authors speculate that programmers may be developing "ambient competence", a sense of being able to take on tasks they would not have attempted before because an AI system might accomplish them.
- They also propose a speculative gestalt account of the "vibe": programmers perceive the generated code, commentary and agent actions as an organised whole and rely on a continuous "vibe check".
- Creators performing on streaming platforms engaged in impression management — demonstrating expertise and control — which the authors read as a response to social penalties for AI use in knowledge work.

## Notes

The authors call their analysis preliminary and a snapshot of an early moment in a fast-changing practice. They list three main limitations: the corpus is small (about 35 hours of vibe coding content, of which about 8.5 hours were analysed in detail); the videos were performed for an online audience, which may skew the workflows shown; and none of the selected videos featured non-programmers, so the conclusion that programming expertise is essential to successful vibe coding holds only for vibe coders who have that expertise. They suggest laboratory experiments, interviews and diary studies as future data sources.

The paper also argues that programming may be "the canary in the coal mine" for how generative AI changes knowledge work more broadly, while noting that other domains such as text lack the structural aids — identifiers, tests, compilation — that help programmers audit generated output.
