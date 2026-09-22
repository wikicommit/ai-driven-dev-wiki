---
title: "AIエージェント向けコーディングルールをArchUnitで機械的に検証する運用"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, guardrails, ai-ide-rules]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/verify-ai-agent-coding-rules-with-archunit'
    hash: sha256:24dfa5099ece90e3a7f95765c99bee45ad8dc9ddd142924e79cb91050675908c
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account of moving the coding rules a team gives its AI agents from prose checked by reviewers to architecture tests enforced as a required CI gate. It argues that the reader of such rules is the agent, so each should stand alone rather than cross-reference, and that a rule which cannot be checked mechanically is only as good as whichever review happens to catch a violation."
  author: "藤本"
  datePublished: "2026-09-07"
  publisher: "[[Organization/zozo]]"
---

The team's starting position was one many have: naming conventions and inter-layer dependency constraints written up as Markdown rule documents for a coding agent — principally Claude Code — to read. Two problems appeared as the rules multiplied. Rules began contradicting and duplicating each other, which is catchable by eye while there are few and increasingly not as they accumulate. And compliance rested on review: checking agent-generated code by eye every time makes the reviewer's load grow without limit, and whatever review misses stays in the implementation.

The first shift is a premise rather than a technique. The team had been writing rules the way one writes documentation for people — cross-referencing between rules, adding background explanation — because a human reader assembles understanding by walking between related documents. But an agent reads the rules every time it implements or reviews, and each additional hop is another opportunity to miss or misread something. Taking the reader to be the agent, they rewrote the rules so each one stands alone with everything needed to apply it. The author reports the duplication they had feared did not noticeably materialize, and that human reviewers' experience of the documents did not change either.

The second shift follows from the first: having changed how rules are written, they still could not say whether rules were being followed, so they began compiling the ones that can be expressed structurally into ArchUnit tests that run at build time. The post is candid that this is partial — not every natural-language rule can be checked mechanically — and its position is that constraints expressible in terms of package structure and relationships between classes are the ones this method covers.

## Key Points

- The stated premise change is that rules for an agent should be self-contained rather than cross-referenced, because the agent re-reads them on every implementation and review, and each reference hop adds a place to misread. The author reports the predicted cost — the same explanation repeated across several rule documents — did not noticeably appear in practice.
- The argued reason for mechanizing is load, not correctness in principle: agents produce a lot of code quickly, so violations arise at the same rate, and checking by eye means reviewer burden rises with volume until it cannot keep up. The author's summarizing claim is that expressing rules executably lets verification speed match the speed at which code is generated.
- A worked example shows why the obvious encoding can be wrong. A rule banning reflection in the domain layer, written as a prohibition on depending on the reflection package, also caught code that merely declared a field of a reflection type — including O/R-mapper-generated code that never calls a reflection API itself. The team replaced it with a condition that inspects actual method calls instead of type references, enumerating by hand the dynamic lookup methods on a class that live outside the reflection package, and widened the scope to all code units so constructors and field initializers are covered too.
- Other rules converted the same way are given as: forbidding a direct call to a date/time class's `now()` without a clock argument, so tests can fix the time; requiring a null check in the compact constructor of records implementing a particular interface; and requiring a transaction annotation on particular methods in the use-case layer, so a transaction boundary cannot be forgotten.
- The post names a three-way consistency problem the mechanization creates: the rule document, the test, and the real code sit in different files and drift apart. Its concrete instance is an exception — one use-case class permitted a raised isolation level — which has to be written both as an exception in the document and as an exclusion condition in the test. The team's current answer is a note in the rule document telling whoever adds an exception to update the test's exclusion too, and the author states plainly that this is still something a person has to read and act on, and that holding the exception declaration in code for the test to reference directly would remove the need for the note. It is recorded as an open improvement.
- A second answer to the same problem is to state the guarantee's coverage inside the rule document: a rule file says which of its constraints are already checked by tests and which still rely on review. The stated benefit is that both an agent and a human reviewer can tell from the document alone where the machine's guarantee ends.
- The knowledge base was split from the rules. Background explanation and implementation patterns — why an architecture was chosen, what each layer's patterns are — went to one directory, and constraints that must be followed to another, on the stated grounds that when both live in one document there is no telling which statements are candidates for verification. The author notes the rules directory is one Claude Code loads by default while the knowledge directory is that project's own convention, and that the resulting reference from a rule file to its knowledge counterpart does not violate the self-containment premise, because the enforceable standard is complete on the rules side and the background is optional.
- A planned rollout was abandoned and the reasoning is reported rather than the plan quietly dropped. The team intended to distribute rules to other repositories through a self-built marketplace-style mechanism with a management tool, and found the obstacle was not the tooling but adoption: almost no team took up another repository's rules. Two causes are offered, which the author is explicit are the team's own retrospective inference rather than measured: fewer rules were genuinely portable across repositories than expected, and importing a rule brings the ongoing cost of keeping it consistent with its test and the local code.
- The stated condition for revisiting that decision is not that more shareable rules happen to accumulate, but that the materials for generalizing are in place — each team recording the background behind its rules, plus a mechanism for comparing those records across teams. The author's stated lesson is that generalizing rules first and then rolling them out does not work before examples from several teams have accumulated.
- Verification is made a required gate rather than merely existing. The team hit a case where a rule was wired into the build's `check` task but not `test`, so running tests locally passed while the violation surfaced only in CI; they standardized on running `check` before pushing and wrote that into the rule document, and the CI job that verifies rules is set as a required status check so a violating pull request cannot merge. When adding a rule, they also confirm the check actually fires by planting a deliberately violating dummy class and seeing it fail, and confirm the existing code has zero violations before merging.
- The closing position is that the consistency work itself gets delegated too: the team asks an agent to cross-check the rule document, the test code and the real code for contradictions, mismatches between description and implementation, and gaps still resting on review — the agent being governed by the rules also helping maintain them. These are the author's account of one team's practice, with no measured before/after reported.

## Context

The post is a concrete instance of what this wiki records under [[DefinedTerm/ai-ide-rules]], and it pushes that idea in a specific direction: rather than treating the rule file as the artifact, it treats the rule file as a specification whose enforceable part should be compiled into a test. Its framing that verification must keep pace with generation puts it alongside this wiki's material on [[DefinedTerm/review-bottleneck]] and on deterministic [[DefinedTerm/guardrails]], and its distinction between rules that can be mechanized and rules that cannot is the boundary it leaves explicit rather than implied.

The author states the intent to widen mechanical verification to conventions still checked by eye, by means not limited to ArchUnit.
