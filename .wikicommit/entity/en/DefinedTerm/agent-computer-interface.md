---
title: "Agent-Computer Interface"
type: "schema:DefinedTerm"
lang: en
tags: [agents, coding-agents, llm, interface-design]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2405.15793'
    hash: sha256:ebb2c6da508182de8f896253125e9ab51d33562a0f61627a99fbb416053c71ec
  - type: url
    url: 'https://swe-agent.com/0.7/background/aci/'
    hash: sha256:98bb48cfdcafb83fda7977db28b9df4186991b9423b723e9295fb6eb87f69773
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An interface built specifically for a language model agent to operate software through, rather than one designed for a human user — the term introduced by the SWE-agent paper for the layer through which its agent creates and edits code files, navigates repositories, and runs tests and other programs."
---

An agent-computer interface (ACI) is an interface designed for a language model agent to work
through, as opposed to one designed for a human. The term is introduced in
[[ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering]],
whose framing argument is that LM agents represent a new category of end users with their own needs
and abilities, and that — just as humans benefit from powerful software applications such as
integrated development environments when doing complex work — those agents would benefit from
interfaces built specifically for the software they use.

## Usage

The paper that introduces the term applies it to [[SoftwareApplication/swe-agent]]'s own custom
interface layer, and names the capabilities that layer is responsible for: creating and editing code
files, navigating entire repositories, and executing tests and other programs. The authors state
that this custom ACI significantly enhances an agent's ability to do those things.

The term also names a design variable rather than only a component. The paper's stated purpose is to
investigate how interface design affects the performance of language model agents, and it reports as
a contribution its insight into how the design of the ACI can affect agents' behavior and
performance — that is, ACI design is presented as something that can be varied and that changes
outcomes, not as a fixed part of an agent's architecture.

The SWE-agent project's own documentation (for version 0.7) describes its ACI as simple, LM-centric
commands and feedback formats that make it easier for a language model to browse a repository and to
view, edit and execute code files, and it draws the analogy to prompting explicitly: just as language
models need good prompt engineering, good ACI design leads to much better results when using agents.
It lists four features the team found immensely helpful while designing the interface:

- a **linter** that runs whenever an edit command is issued and rejects the edit if the resulting code
  is not syntactically correct;
- a **purpose-built file viewer** in place of plain `cat`, which the team found works best showing 100
  lines per turn, paired with a file editor that has commands for scrolling and for searching within
  the file;
- a **directory-wide search command** that succinctly lists only the files with at least one match,
  because showing the model more context about each match proved too confusing for it;
- an explicit message — "Your command ran successfully and did not produce any output." — returned
  when a command's output is empty.

The same documentation points to Interactive Agent Tools as a later extension of the interface.

## Related Terms

- [[SoftwareApplication/swe-agent]] — the system whose custom ACI the term was introduced to describe
