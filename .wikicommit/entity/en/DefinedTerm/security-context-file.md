---
title: "Security Context File"
type: "schema:DefinedTerm"
lang: en
tags: [security, vibe-coding, context-engineering, guardrails]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/vibesec-reckoning.html'
    hash: sha256:8b0b15082b94ab255952a28ff66291626d4cd44d1fdb475bbe0893fe4d77ca26
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A structured file of an organisation's technical security rules, loaded into every AI coding session before any code is written so the agent treats them as non-negotiable guidance. It is versioned, loaded by default, reviewed, and paired with automated checks that validate what the agent produces."
---

A security context file is a structured document compiling an organisation's technical security rules
in a form an AI coding agent can act on, loaded into every AI coding session before any code is
written. As described in [[BlogPosting/the-vibesec-reckoning]], what distinguishes it from a casual
prompt telling the AI to be secure is operational discipline: the file is versioned, loaded by default,
reviewed, and paired with automated checks. It contains non-negotiable rules meant to make the agent
refuse requests that violate policy — for example bypassing a check, disabling logging, or setting
something to public access — and explain why.

## Usage

The article's authors built one after two near-miss incidents in which an AI suggested insecure
configurations while their team was scaling a vibe-coded prototype. Theirs covers zero trust
enforcement, secrets management, harness engineering and supply chain integrity; the coverage they
recommend for any such file adds AI accountability:

- **Zero trust and least privilege** — strict identity verification and minimum access rights on every
  service account and storage resource.
- **Secrets management** — the AI refuses to generate or store API keys, passwords or tokens in code and
  routes them to environment variables or a secrets manager.
- **Harness engineering gates** — SAST scanning, credential scanning and infrastructure validation must
  pass before deployment, with no reliance on prompt instructions alone.
- **Supply chain integrity** — only well-established libraries, with regular audits of every dependency
  for known vulnerabilities.
- **AI accountability** — all AI-generated code is flagged for peer review and automated security
  scanning before deployment.

In practice the article suggests loading it as "Rules" in tools such as Claude, Cursor or Replit, and
later investing in a shared default layer across all tools.

## When It Applies

The practice applies wherever AI agents generate code — including prototypes built by non-technical
citizen builders, which the article argues must still meet enterprise security standards. It assumes
the organisation has security requirements it can work through and restate in a form the AI can act
on. In the [[DefinedTerm/guides-and-sensors]] terms the article borrows from harness engineering, the
file is an inferential guide: it tells the agent what good looks like but cannot by itself confirm the
output is acceptable, so it misfires when relied on alone — prompts can be overridden, misunderstood
or ignored, and the deterministic checks and deployment gates must still catch an issue if the agent
fails to follow the file. Its standing is one team's report: the practice is proposed by the authors of
that article on the basis of their own incidents and the platform they subsequently rolled out.

## Related Terms

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/guardrails]]
- [[DefinedTerm/deterministic-quality-gate]]
- [[DefinedTerm/vibe-coding]]
