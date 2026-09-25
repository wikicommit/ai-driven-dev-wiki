---
title: "Prompt Routing"
type: "schema:DefinedTerm"
lang: en
aliases: ["Routing"]
tags: [prompt-engineering, agent-design-patterns, workflows]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
  - type: url
    url: 'https://github.com/phodal/build-agent-context-engineering'
    hash: sha256:cac7baf9e9ec7a1bfb8c190343db878dcc207737e772a46a03276d7b4be6094a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A workflow pattern for LLM applications in which an input is first classified and then sent down the processing path best suited to it — a specialized prompt, a different model, a tool or a sub-agent."
---

Prompt routing is a pattern for building LLM applications in which an input is analysed first and then
directed to whichever downstream path suits it best, rather than one prompt trying to handle every
kind of request. Anthropic, which calls the pattern simply "routing" in
[[BlogPosting/building-effective-agents]], describes it as classifying an input and directing it to a
specialized follow-up task. A Chinese-language overview of agent construction by the developer phodal
defines prompt routing as an engineering pattern for multi-task, multi-agent or complex AI flows that
splits tasks, analyses the input and assigns it to the most suitable model or sub-task prompt; its core
idea, on that account, is to decide dynamically — from the input and its context — which processing
path, prompt, tool or sub-agent to use, so that execution becomes conditional rather than linear.

## Usage

Anthropic's case for the pattern is separation of concerns: routing lets each path have a more
specialized prompt, whereas without it, optimizing for one kind of input can hurt performance on
others. Its examples are sending different kinds of customer-service queries — general questions,
refund requests, technical support — into different downstream processes, prompts and tools, and
sending easy or common questions to a smaller, cheaper model while harder or unusual ones go to a more
capable one.

phodal's example is a question-answering system: questions unrelated to the system are told they are
unsupported, basic knowledge questions go to document retrieval and a QA model, and complex analytical
questions go to a data-analysis tool followed by a summary. The overview names LangChain's RouterChain,
and routing by semantic similarity, as framework support for the pattern, and presents routing as what
makes [[DefinedTerm/prompt-chaining]] possible for complex problems.

## When It Applies

Anthropic gives two conditions: the task has distinct categories that are better handled separately,
and the classification itself can be done accurately, whether by an LLM or by a more traditional
classification model or algorithm. Accurate classification is thus a precondition for the pattern, not
a by-product of it. phodal's account adds that routing lets a system pick the most suitable handling
for each type of question while keeping it modular and extensible.

Both descriptions are practitioner accounts: Anthropic's is drawn from patterns it reports seeing
across teams building agents, and phodal's from training material for developers learning to build
agents. Neither reports a measured comparison with a single, unrouted prompt.

## Related Terms

- [[DefinedTerm/prompt-chaining]] — the companion pattern for decomposing a task into fixed steps
- [[DefinedTerm/embedding-guided-tool-routing]] — a related technique that routes to tools rather than prompts
- [[DefinedTerm/augmented-llm]] — the building block each routed call is assumed to be
