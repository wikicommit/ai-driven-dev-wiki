---
title: "Shire"
type: "schema:ComputerLanguage"
lang: en
tags: [coding-agents, orchestration, coding-tools]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/hybird-agents-build-ide-intelli-with-cloud-agent/'
    hash: sha256:865ae6df41b7d6f93ed92ec6423a7d6c9755713fef7d9af4b6743f0723d45619
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AI coding agent language that lets a large language model converse with and control an integrated development environment for automated programming, in which the interaction with the IDE and with remote agents is defined in code."
---

Shire is described as a simple AI coding agent language that lets a large language model (LLM)
converse freely with, and control, an integrated development environment (IDE) in order to automate programming.
In Shire, how information from the IDE is handled and how the IDE interacts with remote agents are defined the
way a program is written.

It is presented in [[BlogPosting/integrating-cloud-and-ide-agents]] as an implementation of collaboration between
cloud agents and IDE agents, in which an agent orchestration system on the IDE side calls agents running in the
cloud as well as local ones.

## Details

The example given in that post is a file that begins with a metadata header — a name, variables and an
after-streaming action — followed by the prompt text. One variable is filled by a `thread` function that runs a
shell script calling a remote agent deployed on the Dify platform and extracts the answer with `jsonpath`; the
prompt then combines that requirement with the user's database information and tables. After the model has
analysed the requirement, an `execute` function calls a second, local Shire agent (`gen-sql.shire`) that holds
basic SQL conventions, so that the generated SQL follows enterprise standards. Further examples are published in
the `shire-lang/shire-spring-java-demo` GitHub repository.
