---
title: "The VibeSec Reckoning"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, security, harness-engineering, guardrails]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/vibesec-reckoning.html'
    hash: sha256:8b0b15082b94ab255952a28ff66291626d4cd44d1fdb475bbe0893fe4d77ca26
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A May 2026 article on martinfowler.com by members of Thoughtworks' Global Marketing AI applications team, arguing that prompting an AI to \"be secure\" is not enough for vibe-coded applications. It recommends a security context file, caution with AI-suggested permissions, a daily security intelligence feed, and secure-by-default templates and harnesses backed by deterministic checks."
  author: ["Gautam Koul", "Lucian Moss", "Neil Drew-Lopez", "Daberechi Ruth Edeokoh"]
  datePublished: "2026-05-27"
  publisher: "martinfowler.com"
---

The article starts from the authors' own experience. Their AI applications team in Thoughtworks' Global
Marketing function was asked to scale a video-assembly prototype that a "citizen builder" — a
non-technical user building with AI — had created with Gemini, Replit AI and Claude. Twice the AI
suggested a path with serious security implications, and both times it took a human asking the right
question to catch it. From this the authors argue that [[DefinedTerm/vibe-coding]] without
enterprise-grade guardrails introduces risks organisations cannot overlook, and that telling an AI
agent to be safe is not the same as enforcing that it is safe.

Their answer is to give agents technical security rules as context from the first prompt and to
validate the output through deterministic checks in the development workflow — framed through
[[DefinedTerm/harness-engineering]] and its [[DefinedTerm/guides-and-sensors]] model — plus habits and
organisational changes that make the secure path the easy one.

## Key Points

- In the first incident the AI recommended making a storage bucket public, or setting cloud file
  storage to "anyone with the link", and justified it by saying every company does it; only a firm
  rejection produced a secure alternative. In the second, a service account was given the Access Token
  Creator role, far broader access than the task needed, which the team caught before running the code.
- The authors' key insight is that AI tools often suggest the path of least resistance, which is not
  always the secure one; human judgment remains essential but should not be the only control.
- Prompts can be overridden, misunderstood or ignored, so a constraint that matters must be codified
  as non-negotiable rules somewhere in the development lifecycle — a prompt is a suggestion, a
  build-tool threshold is a gate.
- Short-term habits the article recommends: feed the organisation's security guidelines into every
  session as "Rules" in tools such as Claude, Cursor or Replit; question every permission the AI
  suggests; and ask the AI to role-play a bad actor and pen-test what it just built.
- Medium-term, the team built a [[DefinedTerm/security-context-file]] loaded into every AI coding
  session, and an automated daily security intelligence feed digesting new CVEs, platform advisories
  and security bulletins for the languages, cloud platforms and AI coding tools the team uses.
- Long-term, the authors recommend moving from prompts to pipelines — when a computational sensor such
  as a security scanner triggers, the agentic loop should force the model to self-correct until it
  passes — along with secure-by-default templates and a shared starter harness built jointly by business
  functions, engineering and security.
- The article cites industry figures, drawn from third-party 2026 reports, for the scale of the risk —
  among them that 25% of AI-generated code has confirmed vulnerabilities and that one in five
  enterprise breaches is now caused by AI-generated code.

## Context

The recommendations rest mainly on the authors' own two near-miss incidents and the resulting
platform, which they report was rolled out to 150 users during a hackathon; the statistics are
secondhand, taken from the reports the article cites. The article is addressed to business functions
such as marketing as much as to engineers, arguing that lightweight internal prototypes must still meet
enterprise security standards such as ISO 27001, and that neither the security context file nor the
security intelligence feed requires an engineering background to adopt.
