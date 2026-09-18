---
title: "IBM Watsonx Orchestrate Agent Development Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2504.15546'
    hash: sha256:39549788a2452ec0fb8ea5da808b3e0e1e78cd4676d00b50ff2c06f8b85de2cd
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A set of command-line utilities and a Python-based library, built for the tool-builder persona, for configuring, deploying, and managing agents and tools within IBM Watsonx Orchestrate; its alpha release incorporates the REST-API-as-LLM-tool testing framework described in [[ScholarlyArticle/testing-rest-apis-as-llm-tools]]."
  applicationCategory: "Agent tool development kit"
  author: "IBM"
---

The IBM Watsonx Orchestrate Agent Development Kit (ADK) is a set of Command Line Interface (CLI) utilities and a Python-based library that gives tool builders a tooling environment to configure, deploy, and manage agents and tools within Watsonx Orchestrate. [[ScholarlyArticle/testing-rest-apis-as-llm-tools]] describes a REST-API testing framework deployed as part of the ADK's alpha release and specifically designed for the tool-builder persona.

## Capabilities

As part of the ADK, the framework in [[ScholarlyArticle/testing-rest-apis-as-llm-tools]] lets a tool builder test a tool with an agent. Currently, that support is provided through a CLI, where a builder can generate test cases for a tool and further evaluate the tool with an agent; the builder then receives a categorized error report — see [[ScholarlyArticle/testing-rest-apis-as-llm-tools]]'s error taxonomy — along with template-based recommendations for improving the tool's definition.

## Adoption & Ecosystem

As of the paper's writing, tool builders using the ADK's testing feature had wrapped more than 600 APIs as tools spanning a range of domains, including IT, human resources, finance, procurement, and sales. Before this testing feature was introduced, builders manually created tools and tested only 5-6 test cases per tool; the paper reports the automated test generation and recommendations reduced build effort per tool by about 30% (roughly two days per tool), for a reported total of over 1,200 person-days saved to date. The generated test cases are also reused for continuous and regression testing to verify updated tools continue functioning correctly.
