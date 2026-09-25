---
title: "Assessing internal quality while coding with an agent"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, technical-debt, human-oversight]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html'
    hash: sha256:7ea8a1ed00a8a82a1cd5c918dc9ccc8a4e1c4ff443010387ad6a0351210ba291
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A January 2026 article by Erik Doernenburg in the \"Exploring Gen AI\" series on martinfowler.com that follows a coding agent adding a feature to an existing Mac application and examines the internal quality of the code it produced, arguing that without careful oversight agents tend to introduce technical debt."
  author: ["Erik Doernenburg"]
  datePublished: "2026-01-27"
  publisher: "martinfowler.com"
---

In this article, part of the "Exploring Gen AI" series on martinfowler.com, Erik Doernenburg asks a
question he says reports on AI coding agents rarely address: not whether the generated code implements
the desired features, but what its internal quality is. He argues that internal quality is crucial for
development to continue at a sustainable pace over years, and examines it by having an agent add GitLab
support to CCMenu, an existing Mac application written in Swift that shows the status of CI/CD builds in
the menu bar and already supported GitHub Actions. He tried the experiment with
[[SoftwareApplication/windsurf]] and Sonnet 3.5 in the summer and later with
[[SoftwareApplication/claude-code]] and Sonnet 4.5, breaking the task into smaller chunks each time.

He is explicit that this is an anecdote and not a study, while holding that much of what he saw falls
into patterns that can be extrapolated, at least in his experience.

## Key Points

- Asked to implement GitLab equivalents of the existing GitHub API wrapper, feed reader and response
  parser, the agent handled key differences between the two APIs — that a GitHub repository is a
  GitLab project, and that the two return their arrays of runs in differently shaped JSON — and the
  code compiled.
- The generated wrapper functions nonetheless declared the authentication token as non-optional in
  every function, although tokens are optional and the shared request function underneath had been
  generated correctly with an optional token. The flaw only surfaced as a compiler error once calling
  code passed an optional token.
- Given that error, the agent's fix substituted an empty string at the call site when no token was
  present. The author calls this a "vibe fix": it compiles and works, but it introduces new semantics
  in which an empty string means "no token", which he describes as not idiomatic, not
  self-documenting and unsupported by Swift's type system, and it required changes at every call site.
  The correct fix was to make the token optional in the wrapper's declaration, a one-character change.
- He reports this as one of many such cases: the agent proposed an unnecessary cache it could not
  justify, built complicated logic for a GitHub user/organization overlap that does not exist in
  GitLab and resisted being talked out of it, and replicated URL-construction logic in several places
  instead of reusing existing functions, often missing non-obvious functionality such as overriding
  the base URL for testing.
- In each case the generated code worked and implemented the required functionality, but would have
  added unnecessary complexity and missed non-obvious functionality, lowering the quality of the
  codebase. His conclusion is that an agent left to itself would have changed the codebase for the
  worse, that it took an experienced developer to notice and redirect it, and that without careful
  oversight AI agents seem to have a strong tendency to introduce technical debt that makes future
  development harder for humans and agents alike.
- Both agents stumbled badly over a difference in API design — GitLab keeps the triggering user's
  avatar URL out of the build response and requires a separate call — with Claude Code trying at length
  to convince him the URL was in the response; he ended up implementing that part without the agent.
- His comparison of the two setups: Windsurf with Sonnet 3.5 sped up writing code but needed careful
  prompt planning, constant switching between it and Xcode, and produced code with significant quality
  issues, so that on the whole he did not feel he was getting much out of it. Claude Code with Sonnet
  4.5 needed less prompting and produced code that was better, though by no means high quality, and
  running it in a terminal alongside Xcode felt more natural — enough, for him, to use it regularly.

## Context

The author frames the piece against reports of agents writing large amounts of code quickly, which he
says rarely discuss non-functional requirements and even more rarely assess the quality of the generated
code. His argument rests on his own long experience that investing in the internal quality of a
codebase is worthwhile, because humans and agents alike find a complicated codebase harder to work with.
