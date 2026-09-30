---
title: "Automated Code Review Using Large Language Models at Ericsson: An Experience Report"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, industry-experience, static-analysis]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2507.19115'
    hash: sha256:bc569e7fe7082584b4fa5adb5bc9e4eb0798da7061f99c7427875c825d9812f4
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An experience report on a lightweight automated code review tool built at Ericsson that feeds open-source LLMs the changed lines together with their enclosing method, extracted by static program analysis, and evaluates it through surveys of experienced developers."
  author: ["Shweta Ramesh", "Joy Bose", "Hamender Singh", "Ak Raghavan", "Sujoy Roy Chowdhury", "Giriprasad Sridhara", "Nishrith Saini", "Ricardo Britto"]
  keywords: ["code review", "large language models", "program analysis", "automated code review", "LLM", "llama"]
---

This experience report describes how a team at Ericsson built a lightweight tool for automatically
generating code reviews with large language models, deliberately avoiding expensive pre-training and
instruction fine-tuning. The motivation is that code review depends on experienced developers whose
time is scarce, so reviews become a bottleneck and take senior developers away from writing features
and fixing bugs; automating part of it is meant to reduce that cognitive burden and give developers
timely, consistent feedback as they commit code to version control systems such as Gerrit and Git.

The authors report that a naive prompt such as "Please generate a code review for the following code"
did not work well in practice, and organize their approach around three questions: what data to prompt
on, how to prompt, and how to validate the results. Their answer to the first is context: the tool
passes the modified Java lines together with the method that encloses them. The pipeline fetches
changes and diffs from the Gerrit API, uses the Tree-Sitter parser to build an abstract syntax tree and
find the method(s) enclosing the modified lines, prompts an open-source model such as Code Llama with
that enclosing function, and then post-processes the output by presenting, saving and summarizing the
reviews. Prompt variants included a simple, a detailed, a security-focused, a few-shot and an
issue-topics prompt, aimed at keeping reviews short, tied to the enclosing method and free of generated
code. The tool is exposed through a web interface and a Visual Studio Code plugin.

## Key Points

- Adding contextual information — the enclosing method of the changed lines, extracted by static
  program analysis — to the prompt helped the LLM generate better reviews than prompting on the code
  alone.
- In a survey in which experts rated LLM-generated reviews of 10 Java methods from Ericsson's code
  repository, comments were mixed: experts appreciated suggestions such as meaningful variable names,
  but criticized reviews that got variable types or input parameters wrong, were irrelevant or
  incorrect, missed abstractions, or were too verbose.
- In 36 blind pairwise comparisons among Llama 2 13B, Code Llama 13B, Llama 2 7B and Code Llama 7B,
  the initial results indicated that Code Llama 13B seemed better than the others.
- After nine expert developers used the tool in their day-to-day work for fifteen days, four said it
  saved them time and four found it effective or highly effective for their coding efficiency; when
  reviews fell short, the complaints were that they merely explained the code, were factually
  incorrect, or focused on irrelevant areas.
- In additional experiments the LLM found deliberately injected bugs in 10 short and 5 medium snippets,
  though the authors note these were relatively easy logical bugs; it kept its comments to the changed
  lines; and it took around 5-6 seconds per review for both short and large (100-300 line) snippets.
- The authors conclude that LLM-powered code review can be scalable, cost-efficient and integrated into
  existing workflows without extensive fine-tuning, and that it avoids relying on an external black-box
  tool that they cannot use due to security concerns.

## Notes

The authors describe their results as preliminary and the work as ongoing. Their research roadmap has
phases of about six months each: broader ongoing user surveys and prompt experimentation (zero-shot,
few-shot, chain-of-thought), retrieval-augmented generation and Graph-RAG over documentation, past
review decisions and dependency graphs, a multi-agent framework using a system such as Crew AI for
parallel specialized review agents, and integration with internal software engineering tools.
