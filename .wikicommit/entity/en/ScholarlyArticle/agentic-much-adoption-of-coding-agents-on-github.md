---
title: "Agentic Much? Adoption of Coding Agents on GitHub"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, empirical-study, ai-adoption, open-source]
sources:
  - type: url
    url: 'https://upsilon.cc/~zack/research/publications/tosem-2026-agentic-much.pdf'
    hash: sha256:d47db1332f6875b844e179b1401cd02f6dabf6838a032776f53c385572ae7187
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A large-scale mining study of 128,018 GitHub projects that uses the traces coding agents leave in files, commits, branches and pull requests to estimate that 22.20% to 28.66% of the projects had adopted coding agents as of 21 February 2026, and characterizes where adoption occurs and what agent-assisted commits look like."
  author: ["Romain Robbes", "Théo Matricon", "Thomas Degueule", "Andre Hora", "Stefano Zacchiroli"]
  datePublished: "2026-06"
  keywords: ["Coding Agents", "AI4SE", "Large Language Models", "Software Repositories"]
---

The paper sets out to measure how widely coding agents have been adopted in open-source practice. Its
starting observation is that, unlike IDE code completion, which leaves no explicit trace, coding agents
such as Claude Code, Codex or Cursor leave abundant traces in software repositories: configuration,
rule and guidance files such as `AGENTS.md` and `CLAUDE.md`, co-authorship trailers and author metadata
in commits, conventional branch names, and pull request labels. Drawing on a set of heuristics the
authors maintain for 63 coding agents — 79 author-based, 93 file-based, 20 branch-based and 4
label-based — validated by two-author manual annotation of samples of about 400 flagged files, commits
and pull requests, it mines 128,018 active, non-fork GitHub projects with at least 5,000 lines of code
and 100 commits, over a study period from 1 January 2025 to 21 February 2026.

It defines a coding agent as an LLM running in a loop with tool access that aims to complete a given
goal, and distinguishes it from code completion by the scale of the tasks undertaken and the degree of
autonomy — up to submitting a complete pull request for a bug report. The study is organized around six
research questions covering overall adoption, its relation to project characteristics, its contexts
(organizations, GitHub topics, languages), its evolution over time and across tools, the size of
agent-assisted contributions, and the types of those contributions. The authors argue throughout that
their figures are more likely to undercount than overcount real use.

## Key Points

- As of 21 February 2026, 12.08% of the projects showed coding agent traces at the file level
  (including agent files listed only in `.gitignore`) and a further 11.51% only at the commit level,
  giving a conservative adoption estimate of 22.20% and a high estimate of 28.66%; a footnote reports
  an updated estimate of 31.63% to 38.23% as of the end of May 2026.
- File-level and commit-level detection overlap only partly: of projects with visible agent files,
  64.54% were also detected by commit-level heuristics.
- The paper classifies a project's commit-level adoption by its AI-assisted commit ratio since adoption
  into Experimental (below 1%), Limited (1–5%), Consistent (5–20%) and Pervasive (above 20%); among
  file-level adopters with at least 10 post-adoption commits and some AI-assisted commits, 23.97% were
  Pervasive.
- File-level adoption is higher for younger projects (26.37% in the youngest decile versus 7.96% for
  projects over a decade old) and, contrary to the expectation that agents suit greenfield work, also
  higher for larger projects by lines of code, contributors, commits, issues and pull requests.
- Larger and more established adopters show more Experimental and less Pervasive commit-level adoption,
  so higher file-level adoption in large projects does not translate into a higher commit ratio.
- Across the repositories of 20 top organizations, file-level adoption is 17.21% against 12.08% overall,
  a relative increase of about 42%, with wide variation between organizations.
- Adoption is broad across GitHub topics and programming languages, with few topics showing very low
  adoption; commit ratios vary much less across topics than file-level adoption rates do.
- Cumulative adoption shows inflection points at the end of February 2025, around mid-May 2025, a
  slowdown in autumn 2025, and a renewed sharp rise at the start of 2026.
- A few tools account for most adoption: GitHub Copilot and Claude Code together account for more than
  half, and the top five tools — assuming most "Generic" `AGENTS.md` use is Codex — for more than 80%;
  a third of adopting projects use more than one tool, the most common pair being Claude Code with
  Copilot.
- AI-assisted commits are larger than human-authored ones — a median of 31 added lines against 11 —
  and also delete more lines and touch more files, which the authors read as pointing toward increased
  churn.
- In a sample of 790 commits co-authored by Claude Code, 35.7% were features and 29.9% bug fixes and
  only 7.1% chores, so feature commits are about twice as common as in a prior study of human-authored
  commits, a comparison that rests on that other study's figures.

## Notes

The authors discuss reasons their estimates could be too high — projects that tried agents and
stopped, and uncertainty about how much of a detected commit the agent actually wrote — and reasons
they could be too low: agents that do not sign commits (Codex, for instance), settings that turn
attribution off, developers who commit agent work by hand, agent configuration kept in separate
dotfiles repositories, and agents for which they have no heuristic. They conclude an undercount is
more likely, citing their finding that half of a sample of projects whose commit ratio fell to zero
had added or modified an agent guidance or configuration file after
the drop. They also caution that open-source use may differ from
industry use, which they expect to be higher given the cost of running agents.

The study counts the guidance files that make agents visible but cannot always attribute them: because
`AGENTS.md` is now read by many agents, the authors file its users under a "Generic" category rather
than crediting them to Codex, which originally introduced it (see [[DefinedTerm/agents-md]]). They
close with a call for practitioners to document rather than hide their use of coding agents, and for
agent providers to keep standardizing while defining mechanisms to identify individual agents.
Related empirical work in this wiki includes [[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]].
