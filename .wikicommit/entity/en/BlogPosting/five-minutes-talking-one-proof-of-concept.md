---
title: "5 Minuten reden, ein Proof of Concept - unser KI-Experiment mit AI-Assisted Coding und Spec Driven Development"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, requirements-engineering, prototyping, ai-assisted-coding]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/poc-in-5-min-mit-ai-assisted-coding-und-spec-driven-development'
    hash: sha256:1ecee45754502ac5450634cac82b080a91a870746355e7e5f7a465bdb4b6f72b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A German-language codecentric blog post reporting an experiment in which a five-minute simulated customer interview, transcribed and processed with Claude Code following the BMAD method, produced planning artifacts and then a runnable proof of concept."
  author: ["Teoman Kinaci", "Sven Heinz"]
  datePublished: "2026-01-28"
  publisher: "codecentric AG"
---

This post, written in German by two codecentric consultants, reports an experiment asking how much can be drawn out of a five-minute conversation. The authors simulated a typical first requirements meeting in which a fictional customer described a digital calendar for parents of babies — documenting appointments, health events such as illnesses, vaccinations and vitamin intake, and other milestones, with text and voice input, photo and PDF attachments, colour-coded categories, support for several children, and a planned roll-out to about 100 beta testers. The recording's transcript became the input for AI-assisted work following the [[SoftwareApplication/bmad]] method with [[SoftwareApplication/claude-code]].

The post frames the experiment as a way of shortening the path from a vague idea to a specification in greenfield projects, which it describes as often long and full of loops, and presents [[DefinedTerm/spec-driven-development]] with BMAD as the means of getting from a rough idea to a structured, discussable solution quickly. Its conclusion is that the experiment was a complete success: from a simple five-minute conversation, a proof of concept emerged within a few hours that the authors say could be rolled out directly to up to 100 test users for feedback.

## Key Points

- The process had four steps: the recorded conversation served as input; BMAD with Claude Code generated four artifacts from the transcript — an implementation roadmap, a feature list split into core and optional features, a risk register, and a rough timeline; the artifacts were checked, assessed and discussed with the (fictional) client by the authors as a human-in-the-loop step; and a runnable proof of concept, including a user manual, was generated from the validated artifacts.
- The authors report that the AI recognised explicit requirements such as multi-child support and German localisation, and also implemented implicit wishes such as data backup and restore.
- They report that requirements were carried consistently across the roadmap, the feature list and the code.
- They report that the AI chose a tech stack on its own on the basis of the risk factors it had generated, and credit that choice with the proof of concept's simple setup and usability.
- They report that the AI prioritised features, separated must-haves from nice-to-haves and gave traceable reasons for its decisions.
- The main value claimed for the approach is that tangible requirements for a proof of concept emerge with minimal initial effort, helping to concretise ideas quickly, test feasibility early and estimate effort and risk in the early phase. All of these points rest on this single experiment as reported by its authors.

## Context

The post is written for decision-makers who need to act quickly in a dynamic market, and it pitches spec-driven development with BMAD and AI support as a way to make projects concrete, assess feasibility and effort early, and secure advantages through speed. It closes by inviting readers to try the approach in a workshop, so it is also promotional material from a consultancy. The artifacts it shows are an excerpt of the AI-generated feature list and a sample JSON data export from the resulting app.
