---
title: "Gemini Cloud Assist"
type: "schema:SoftwareApplication"
lang: en
tags: [cloud-operations, ai-assisted-programming]
sources:
  - type: url
    url: 'https://codelabs.developers.google.com/sdlc/instructions'
    hash: sha256:ed5d01ab1f229b1c0f5543df1541841ed81d141c60c442f41d9ad008c38881ee
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An AI assistant in the Google Cloud console, opened as a chat pane, that Google's own workshop uses both to design an application's cloud architecture from a prompt — producing a diagram and Terraform code — and to help operate the deployed application through log analysis, performance and cost questions."
  applicationCategory: "Cloud console AI assistant"
  author: "[[Organization/google]]"
---

Gemini Cloud Assist is an AI assistant from [[Organization/google]] built into the Google Cloud
console, opened from a "Cloud Assist Chat" control at the top right of the console. The source
available here is a Google Codelabs workshop, "AI Agent End to End", which uses it at the two ends of
the software development lifecycle: first to turn an idea for an application into a cloud
architecture, and later as an operational assistant for the running application.

## Capabilities

In the workshop's design step, a user describes the application they want in a prompt — in the
example, a Python backend and React frontend hosted separately on Cloud Run, communicating over
WebSocket, with generated images stored in a Cloud Storage bucket and a way to store an API key — and
Cloud Assist generates an architecture diagram. From an "Edit app design" view the user can then
download the corresponding Terraform code, which the workshop describes as the machine-readable version
of the same plan. The workshop treats that code as a reference blueprint rather than something the
participant runs.

In the operations step, after the application is deployed, the workshop uses Cloud Assist on the live
Cloud Run service with prompts for three kinds of task: summarising recent errors in the service's
logs, investigating high startup latency, and analysing the costs of the service and its storage bucket
for savings. Enabling it is shown as a "Get Gemini Assist" step with an option to enable Cloud Assist
at no cost.

## Adoption & Ecosystem

The workshop pairs Cloud Assist with [[SoftwareApplication/gemini-cli]], which it uses for writing
code, tests, deployment scripts and a CI/CD pipeline in between the design and operations steps, and
with [[SoftwareApplication/agent-development-kit]] for the agents the application contains. Its framing
is that the same AI assistant that helped build an application is also a partner for monitoring,
troubleshooting and optimising it in production. This is Google presenting its own tools in a training
workshop, not an independent account of how they are used.
