---
title: "VibeCraft"
type: "schema:SoftwareApplication"
lang: en
tags: [vibe-coding, multi-agent-systems, non-programmers]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex_cloud_and_infra/articles/1084654/'
    hash: sha256:3a39bfbcaf9b1ab426e9dd699c371ca1c03d2891de020bf64c99fa2f2c088392
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A chat-driven platform from Yandex's SourceCraft team that lets people without programming experience create, deploy and iterate on web applications, using a manager agent and a programmer agent and deploying to Yandex Cloud."
  applicationCategory: "Application builder for non-programmers"
  featureList: "Single chat interface; clarifying interview before building; editable development plan; manager and programmer agents; Node.js/TypeScript full-stack code stored in a SourceCraft repository; deployment to Yandex Cloud with serverless YDB storage; chat recreation and loop detection"
  author: "[[Organization/yandex]]"
---

VibeCraft is a platform for building software products through a chat, aimed at specialists outside programming such as marketers, accountants and analysts. It comes from the team behind the SourceCraft developer tools, whose history began in Yandex Infrastructure, and [[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]] presents it as a response to the limits of [[DefinedTerm/vibe-coding]] with general-purpose coding assistants: those assume a developer who can check the result and knows that deployment, databases and domains also have to be dealt with, whereas VibeCraft is meant to take those concerns off the user entirely.

The platform works on a "one prompt" principle: code is stored in a SourceCraft repository, and the product is deployed to Yandex Cloud and uses that platform's services, such as serverless YDB for data. Typical products named are landing pages, online-course sites, personal-finance and workout trackers, games and CRM systems.

## Capabilities

Generation is handled by an ensemble of Yandex models trained to create and modify products, organized as two agents. A manager agent talks to the user — interviewing them, asking clarifying questions when the prompt leaves gaps, setting up the environment and presenting a development plan that can be edited or accepted — while a programmer agent writes the code, creates the environment in SourceCraft, runs it and checks that it works. Applications are generated as Node.js full-stack code, with TypeScript used for both browser and server.

Two recovery mechanisms are described: recreating the chat, so that a new agent with fresh memory reconstructs what is going on, and a loop detector that stops generation and restarts it when the model starts producing incoherent text. The team also deliberately constrained the manager agent: rather than being able to edit files, it has a file-writing skill that always returns an error telling it to assign the work to the programmer agent, because instructions in the prompt alone did not stop it from editing code.

The post reports that models and system prompts are tuned for quality of result over speed, with a first result in about ten minutes, a simple prototype in 7–10 minutes, and about 40 minutes for a task tracker, one of the most popular requests.

## Adoption & Ecosystem

VibeCraft is open for registration with a complimentary quota for creating projects, and the team collects feedback and feature votes in a chat. Features stated as in progress are image upload (to show the agent a picture with a request to "make it look like this"), templates, and connectors to external services such as payment gateways and neural networks.
