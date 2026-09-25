---
title: "AgileGen"
type: "schema:SoftwareApplication"
lang: en
tags: [human-oversight, code-generation, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2407.15568'
    hash: sha256:3f6cdd2a21d8a672eee82d96802e4e5bae4cd18872ab60b3e3a9971595254f97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An interactive system for generative software development that turns an end user's brief requirement into Gherkin user scenarios the user decides on, generates a web application from the decided scenarios, and iterates on it through the user's acceptance and recommendations."
  applicationCategory: "Human-AI collaborative generative software development agent"
  featureList: "Gherkin scenario generation; Gherkin-to-natural-language interaction bridge; scenario decisions (confirm, add, delete, modify); memory pool of past scenario decisions stored in SQLite3; visual design (page design and visual description); consistency factors and automatic code modification; code execution link; design and function modification requests; code download"
---

AgileGen is an agent for generative software development — building software from an end user's
requirement — designed around human-AI teamwork, with its source code published at
<https://github.com/HarrisClover/AgileGen>. It is introduced in
[[ScholarlyArticle/empowering-agile-based-generative-software-development-through-human-ai-teamwork]],
whose authors built it so that end users make the decisions they are good at — clarifying
requirements and accepting results — while the agent generates the code in between. Its core idea is
to complete the acceptance criteria missing from users' requirements using Gherkin, the language of
behavior-driven development, and to use the resulting scenarios to steer code generation.

## Capabilities

The system has two core components, both built as chains of LLM prompts in the manner the authors
call an AI-Chain. The Scenario Design component takes the user's natural-language requirement,
looks up the most similar past requirement in a memory pool, generates Gherkin scenarios, and
translates them into natural language for the user, who can confirm, add, delete or modify each
scenario; the decided scenarios are stored back in the memory pool and converted into Gherkin
again. The Rapid Prototype Design component then plans the visual design — a page design and a
visual description guided by eight visual design principles — generates the code, derives
consistency factors (business-logic cases, at least one per scenario) from the Gherkin, and uses
them to modify the generated code automatically once.

The user interface is built on the Gradio library. It offers a requirement input area, a scenario
area where each scenario can be edited, deleted or supplemented, a log output area, and, after
generation, a code execution link to try the application, a code download link, and separate
design and function modification areas whose requests trigger a new iteration. The paper's
implementation generates web applications as an HTML, a CSS and a JavaScript file.

## Adoption & Ecosystem

The paper runs AgileGen on gpt-3.5-turbo and gpt-4-1106-preview, noting that the model can be
switched through a configuration parameter, and evaluates it with participants who used it on web
projects and on tasks from ChatDev's SRDD dataset. The authors describe plans to integrate the
Cucumber testing tool so the Gherkin scenarios can be run as automated tests, and to deploy the
system on a public testing platform to accumulate users' decisions over time; they also note that
the memory pool's SQLite3 database could be expanded to MySQL or another server-side system if
higher concurrency is needed.
