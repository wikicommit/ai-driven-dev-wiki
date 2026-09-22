---
title: "pfmls-stylepack"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-tools, context-engineering, claude-code]
sources:
  - type: url
    url: 'https://toss.tech/article/52631'
    hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A plugin built by a team at Toss Bank that stores that team's coding conventions as individual rule files and injects the relevant ones into a coding agent through hooks — immediately after a file is written, and again just before the agent finishes."
  applicationCategory: "Coding agent plugin"
  featureList: "One rule per file, each pairing trigger conditions with the text injected; regex and filename-pattern rule selection with no model call; injection immediately after a file write and again before the agent finishes; language-specific team context injected at session start; rule-firing logs used to tune triggers"
---

pfmls-stylepack — shortened to "Stylepack" in the post that describes it — is a plugin built by a
team at Toss Bank to make a coding agent follow that team's conventions. It is presented in
[[BlogPosting/making-ai-follow-team-rules]] as the answer to a problem that post sets out at
length: conventions written into a project-root instruction file are read at the start of a session
and then stop being applied as the session grows, a failure the post attributes to
[[DefinedTerm/lost-in-the-middle]].

Rather than making that file better, the plugin puts the conventions inside the agent's own loop,
using [[DefinedTerm/agent-hooks]] to deliver them at the moments the agent is actually writing
code. The design is explicitly borrowed from the older pattern of running a linter after a model
writes code and feeding its errors back: the flow is the same, and what is checked changes from
"this is syntactically wrong" to "this is not how our team does it".

The post does not describe the plugin as publicly available; everything recorded here is that
post's account of it.

## Capabilities

A rule is one file, which holds both the condition under which it fires and the exact text the
agent receives. Triggers are expressed as a filename pattern, one or more regular expressions
matched against the code, and an exclusion pattern; the injected text sits alongside them in the
same file under a separate key.

Rule selection deliberately does not call a model. Because the hook runs on every file write it has
to return immediately, so filename patterns and regular expressions do the narrowing. The post
reports that an earlier version which asked an AI to judge relevance added about ten seconds per
request, and argues the narrowing does not need to be accurate because the agent receiving the
rules makes the final judgement about whether they apply.

There are two injection points, described as differing in character rather than degree:

- **Immediately after a file is written** — the hook reads only the body of the file just written,
  runs fast, and injects at most two rules, with the same rule injected only once per session. Its
  purpose is to get the code fixed where it was written. The worked example is a `StrEnum` gaining
  a new member while a `match` statement elsewhere in the file silently loses coverage of it; the
  injected rule prompts the agent to add the missing branch and a `case _: assert_never(...)`
  fallback so the type checker catches the next omission.
- **Just before the agent finishes** — the hook takes the whole change as a `git diff`, runs more
  slowly, and injects at most four rules. This exists because a single-file hook cannot see a
  defect spread across files; the post's example is a service depending on a repository
  implementation rather than its interface, where each of the two files is correct read alone. The
  text injected here describes itself as a reminder to review rather than a hard failure.

Separately, at session start the plugin injects team-wide context selected by the repository's
language environment — the presence of `pyproject.toml` bringing in Python guidance and
`build.gradle` bringing in Spring guidance — on the grounds that rules for the wrong language are
only a distraction.

## Adoption & Ecosystem

Distribution is central rather than copied. The post rejects putting conventions in a template
repository on the grounds that a template starts ageing the moment it is copied and improvements to
the original never reach the repositories already cloned from it; instead the rules live in one
central repository, and the plugin fetches the current version in the background whenever a session
starts, so nobody has to do anything to be on the latest rules.

The team also instruments the plugin against itself, logging which rule fired, when, and on what
condition. Two corrections are reported from that log. One trigger matched Python f-string format
specifiers as well as the dictionary literals it was aimed at, firing across 21 sessions without
producing a single code change, and was fixed by requiring a whitespace character after the colon;
the post's conclusion is that a wrong suggestion is worse than none, because it teaches the agent
to disregard the rules. The other trigger was too narrow, matching only `for` and `.forEach` while
the N+1 queries the team actually caught in review appeared as `.map` and as list comprehensions.
From that second case the post draws a dividing line: defects recognizable from the shape of the
code belong in triggered rules, while defects that only show at runtime belong in always-loaded
context.

New rules come both from engineers adding them during refactoring and from a separate intake that
gathers review comments to find feedback being repeated across pull requests — the post gives one
rule, about stateful classes declared as `@dataclass`, that was created this way after the same
comment recurred on two pull requests in one repository.
