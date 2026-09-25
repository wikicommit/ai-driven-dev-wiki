---
title: "Agent Skills"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, context-engineering, agent-tooling]
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview'
    hash: sha256:3f2567f8a7cd1948e582601407ccfd2804e66152973859636da7ba44f9ff235f
  - type: url
    url: 'https://developers.googleblog.com/closing-the-knowledge-gap-with-agent-skills/'
    hash: sha256:99da78c38e52825287d818db6e10f2cf2d633b7e9479102298bccb809800d651
  - type: url
    url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
    hash: sha256:e884d6fd1fe5becb8f432c99a20cf8b36e39d087e507037696b411e11d077ef5
  - type: url
    url: 'https://www.anthropic.com/news/skills'
    hash: sha256:d9203771b21f47f29f2864693735d485c5abe5e9b35eed91551ec1cbcc4099c2
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260427-mercari-pm-agent-design-automating-the-pm-workflow-with-claude-code-skills-and-mcp/'
    hash: sha256:f446b9545db9ce2a51b98a91bfe525a706f8f22bd2381f38543f927626b9b58a
  - type: url
    url: 'https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html'
    hash: sha256:33171882bb4809ae93923b09f4e1fe6315bf6de5690393243df5a995118678bc
  - type: url
    url: 'https://jonghoonpark.com/2026/03/29/agentic-engineering'
    hash: sha256:92fea29c2779ce511435e3c79aeb42f9b33855c8f3a1f24849a1c6993534b024
  - type: url
    url: 'https://arxiv.org/pdf/2605.07358'
    hash: sha256:096f5ed37573599d6a6c7ead31f91dbe0c836695066c0ed2890efe4a97108983
  - type: url
    url: 'https://developers.openai.com/codex/skills'
    hash: sha256:5ebdfc92d1486abd67e502b39443805551caddaedab7c0f36ee755769b80128f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A format, documented by Anthropic for Claude and since published as an open standard, for extending an agent with domain expertise: a directory holding a SKILL.md file of instructions plus optional scripts and reference material, loaded in stages so that an unused skill costs only its name and description in context."
---

Agent Skills is a format, documented by Anthropic for Claude, for packaging modular capabilities
that extend an agent's functionality. Skill packages are also written and published by parties other
than the agent vendor: Google's developer relations team writes that agent skills have surfaced as
an extremely lightweight but potentially effective way to close the gap between a model's fixed
training knowledge and fast-moving libraries and SDKs, and set out to show what any SDK maintainer
could do about that gap. Each Skill bundles instructions, metadata and optional resources such as scripts and
templates, which the model uses automatically when relevant. The vendor's documentation
distinguishes them from prompts on the basis of scope and persistence: prompts are
conversation-level instructions for one-off tasks, whereas Skills are reusable, filesystem-based
resources that load on demand, so the same guidance does not have to be repeated across
conversations. The stated benefits are specializing the model for domain-specific tasks, creating
guidance once rather than repeating it, and composing several Skills for multistep tasks.

Anthropic's own engineering account of the format ([[BlogPosting/equipping-agents-for-the-real-world-with-agent-skills]])
places it as a response to capability rather than to deficiency: once general-purpose agents can
operate full computing environments, the open question becomes how to equip them with domain
expertise composably, scalably and portably. That account offers an analogy — building a skill
resembles assembling an onboarding guide for a new hire — and argues that the alternative it
displaces is building a separately engineered agent for each use case. A note added to that post on December 18, 2025
records that Agent Skills has since been published as an open standard for cross-platform portability.
The product announcement ([[BlogPosting/introducing-agent-skills]]) carries its own note of the same
date recording two further additions alongside that one: organization-wide management for skills, and a
directory featuring partner-built skills.

As Anthropic documents it for Claude, the format is filesystem-based by design: Skills exist as
directories in Claude's virtual machine environment, and Claude interacts with them using ordinary
shell commands — reading `SKILL.md` to bring its instructions into context, reading further files
when the instructions reference them, and running bundled scripts through the shell so that only
their output, never their code, enters the context window. Other harnesses reach a skill by other
means; Google's evaluation, for instance, gave the model an `activate_skill` tool and a `fetch_url`
tool for downloading the docs.

## Usage

Every Skill requires a `SKILL.md` file with YAML frontmatter carrying two required fields, `name`
and `description`. The documentation states the constraints on each: a name of at most 64
characters, restricted to lowercase letters, numbers and hyphens, with no XML tags and no reserved
words; and a non-empty description of at most 1024 characters, again with no XML tags. The
description must state both what the Skill does and when it should be used, because it is what the
model matches a request against when deciding whether to trigger the Skill.

Content is organized into three levels, each loaded at a different time — the arrangement the
documentation calls [[DefinedTerm/progressive-disclosure]]. Metadata is always loaded, at a stated
cost of roughly 100 tokens per Skill; the `SKILL.md` body loads when the Skill is triggered, at a
stated budget of under 5,000 tokens; and bundled resources cost nothing until read. The documented
consequence is that many Skills can be installed without a context penalty, and that a Skill may
bundle extensive material — comprehensive API documentation, large datasets — that is never charged
against context unless used.

The vendor's engineering post works the arrangement through a concrete case: the PDF skill behind
Claude's document-editing abilities. Its `SKILL.md` refers to two further bundled files,
`reference.md` and `forms.md`, and the post's stated reason for moving the form-filling instructions
into `forms.md` is to keep the core of the skill lean, on the expectation that the model reads that
file only when actually filling a form. The same skill bundles a Python script that reads a PDF and
extracts its form fields, which the model can run without either the script or the PDF entering
context — an arrangement the post justifies on two grounds, that generating tokens to perform an
operation code already does is far more expensive, and that many applications need the determinism
only code provides.

For authoring, that post recommends starting from evaluation — running agents on representative
tasks to find where they struggle, then building skills incrementally against those observed gaps
rather than anticipating what will be needed. It advises splitting a `SKILL.md` into separate
referenced files once the file has become unwieldy, adding that where contexts are mutually exclusive
or rarely used together, keeping those paths separate reduces token usage; and it notes that bundled code serves as
both executable tool and documentation, so a skill should make clear which of the two a given script
is. It singles out `name` and `description` for particular attention, on the grounds that these are
what the model uses to decide whether to trigger the skill at all. Its final suggestion is to have
the model itself capture successful approaches and recurring mistakes into a skill as work proceeds,
and to ask it to self-reflect when it goes off track.

Availability differs across the vendor's products. On the API, Skills require the code execution
tool and are selected by a `skill_id` in the container parameter, with pre-built document Skills for
PowerPoint, Excel, Word and PDF, and custom Skills uploaded through a Skills API and shared across a
workspace. In [[SoftwareApplication/claude-code]] custom Skills are filesystem-based and need no
upload, placed in a personal or project directory, while the pre-built document Skills are not
available there. On claude.ai both kinds work, with custom Skills uploaded as zip files and
individual to each user rather than centrally managed: the
documentation states they are not shared organization-wide and cannot be centrally managed by admins,
and that claude.ai does not support centralized admin management or org-wide distribution of custom
Skills. That sits unreconciled against the product announcement's December 2025 note recording that
organization-wide management for skills has been added; the two sources say different things and
neither dates itself against the other. The engineering post states that at
publication the format was supported across Claude.ai, Claude Code, the
[[SoftwareApplication/claude-agent-sdk]] and the Claude Developer Platform.

The product announcement fills in how each surface is reached. In Claude apps the format is stated as
available to Pro, Max, Team and Enterprise users, with Team and Enterprise admins having to enable it
organization-wide first; invocation is automatic rather than manually selected, and the announcement says
skills appear in Claude's chain of thought as it works. On the Developer Platform, Skills can be added to
Messages API requests, a `/v1/skills` endpoint gives programmatic control over custom skill versioning
and management, and Skills are stated to require the Code Execution Tool beta, described as providing the
secure environment they need to run. In Claude Code they are installed via plugins from the
`anthropics/skills` marketplace or manually by placing them in `~/.claude/skills`, and shared with a team
through version control.

A practitioner account reaches the same structural advice from the other direction, and is the only
source here that reports testing it. [[BlogPosting/mercari-pm-agent-design]] describes building a
skill that carries a product manager's workflow end to end, and reports first consolidating all
definitions into a single `SKILL.md` and then finding, through scoring by a separate evaluation
skill, that the longer the file, the worse the output accuracy became. The author's response was to
separate the behaviour definition — what to do and in what order — from reference data and
templates held in a `references/` directory, and reports that this structural change alone produced
a clear improvement in score. The post frames this as applying separation of concerns from software
engineering to prompt design, and relates the underlying problem to the phenomenon often called
"Lost in the Middle", in which models fail to attend properly to information in the middle of a long
context. It also notes writing `SKILL.md` in English on the grounds that English instructions tend
to produce higher accuracy with Claude. What that account adds to the vendor's advice above is not a
different rule but a reason to follow it: the vendor recommends splitting a file once it has become
unwieldy, while this author reports measuring the cost of not doing so.

That post's other design claims concern what a skill's instructions should forbid rather than how
they are filed. Its stated position is that the most dangerous risk in embedding an LLM in a
business workflow is plausible but unfounded output — a model producing reasonable-looking numbers
where no data exists — and that this cannot be solved by telling the model not to lie: the skill
must specify how to behave when it recognizes missing data. The rules it uses are that unconfirmed
data must be labelled "Not provided" or "To be validated" and that numbers and sources must never be
fabricated, alongside an instruction barring the agent from inferring completeness, so that only
explicit confirmation from the user allows progression to the next step. The author's summary is
that designing a skill is close to writing a behaviour specification, and that clearly defining what
the model must *not* do improves accuracy more directly than commands do.

A second practitioner account describes the format used as shared organizational infrastructure
rather than by an individual author. [[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]
reports a centralized skill collection at [[Organization/zalando]], grouped into plugins and
addressing common tasks or concerns across disciplines — the post names data, engineering,
frontend and SRE — and across programming languages. It states that migration skills, which guide
teams in adopting new platform tools or infrastructure practices such as multi-arch builds, are a
widely popular type. Distribution is by managed configuration settings or a CLI command that
installs the needed symlinks, which the post attributes to some agents not supporting plugin
marketplaces.

What that account adds beyond distribution mechanics is a second-order effect it attributes to
encouraging broad contribution: the collection became a way to discover and disseminate best
practices across the organization, on questions such as validating plugin syntax in CI/CD
pipelines and where the separation between skills and scripts should fall — the post's example is
where OAuth token generation belongs. Teams writing their own skills are said to use the
collection as a reference and inspiration. These are the author's own observations of one
organization's practice, with no evaluation reported.

Authoring is supported by a skill of its own. The announcement describes a `skill-creator` skill that
gives interactive guidance — asking about the workflow, generating the folder structure, formatting the
`SKILL.md` file and bundling the resources — with no manual file editing required. That is the format
applied to itself: the procedural knowledge for writing a skill is packaged as a skill.

A third practitioner account is the smallest scale the format appears at here — one developer rather
than a team or an organization. [[BlogPosting/lessons-from-releasing-a-product-with-ai-agents]]
reports templating repeated prompts as Skills once retyping them became tedious, its example being a
standing request to analyse uncommitted changes and write tests for them, and says what such a skill
is, is not a mere prompt but an engineer's know-how transplanted into coding conventions.
Its second use is of a skill someone else wrote: the author, a backend developer, ran a third-party
SEO skill against their own site to produce a list of improvement points, then handed that list back
to the agent to apply against the source, repeating the loop about once a week. The observation drawn
is that the format helps most in a domain that is not one's own — which is the knowledge-gap argument
Google's account makes about fast-moving SDKs, reached here from the direction of a developer's own
expertise rather than a model's training cutoff. That account reports no evaluation and does not
identify which harness feature set it is describing beyond naming Claude Code as the agent.

The format is not confined to Anthropic's products. OpenAI's documentation for building skills in
ChatGPT and [[SoftwareApplication/openai-codex]] says its skills build on the open agent skills
standard and describes the same shape: a directory with a `SKILL.md` file, which must include `name`
and `description`, plus optional `scripts/`, `references/` and `assets/` directories and an optional
`agents/openai.yaml` file for UI metadata, invocation policy and tool dependencies. It also describes
progressive disclosure — ChatGPT and Codex start with each skill's name and description and load the
full `SKILL.md` only when they decide to use the skill — and adds a limit specific to Codex: the
initial skills list, which in Codex also carries each skill's file path, uses at most 2% of the model's
context window, or 8,000 characters when the window is unknown, with Codex shortening descriptions
first and possibly omitting some skills when many are installed. Activation is either explicit, by
naming the skill in the prompt, or implicit, when the task matches the skill's `description`, which
setting `allow_implicit_invocation: false` in `agents/openai.yaml` turns off while leaving explicit
invocation working. Codex reads skills from repository locations (`.agents/skills` in every directory
from the working directory up to the repository root), a user location, an admin location and a set
bundled with Codex; the documentation treats these locations as for authoring and local discovery,
and points to plugins, which can bundle several skills with MCP server connections, for distributing
skills to others (compare [[DefinedTerm/agent-plugins]]). Its best-practice list is to keep each skill
focused on one job, prefer instructions over scripts unless deterministic behaviour or external
tooling is needed, write imperative steps with explicit inputs and outputs, and test prompts against
the skill description to confirm it triggers correctly.

## A Research Framing

The academic literature uses the term more broadly than any one product's file format.
[[ScholarlyArticle/comprehensive-survey-on-agent-skills]] defines agent skills as reusable procedural
artifacts that coordinate tools, memory and runtime context under task-specific constraints, and
formalizes a skill as a tuple of three parts: a root instruction document the agent can load and
follow, a set of auxiliary resources such as reference documents, templates or executable scripts,
and applicability conditions governing when the skill should be retrieved and applied — expressed as
metadata, natural-language descriptions or embeddings. The survey notes that the tuple need not be
fully instantiated in every system. Read against the format described above, a `SKILL.md` body
corresponds to the instruction document, bundled files to the resources, and the frontmatter
`description` to the applicability condition; the survey itself refers to `SKILL.md` files and skill
folders among the artifacts its methods evolve, without tying the concept to them.

On the survey's account the case for skills is what it calls the [[DefinedTerm/procedural-gap]]:
access to tools does not say when a capability should be invoked, how tools should be coordinated, how
failures should be handled or how outputs should be validated. It casts the agent as the high-level
planner and skills as the operational layer beneath it, and distinguishes skills from raw tools and
MCP servers on the grounds that skills encode situated know-how — triggers, sequencing, fallbacks and
pitfalls — while tools only expose operations. It also allows skills that are not tool-centric at all,
such as review checklists, which mainly draw on the model's own knowledge but still supply structure
beyond ad-hoc prompting.

Where the vendor documentation describes how a skill is written and loaded, the survey organizes the
research around a lifecycle: how skills are represented (text-backed, code-backed or hybrid, by what
their resources contain), acquired (from human experts, from an agent's own past runs, on demand for
the current task, or from external corpora), retrieved and selected from a large pool, and evolved
after they exist — revised, validated, propagated through shared repositories and governed at
runtime. The problems it identifies are lifecycle problems rather than authoring ones: weak trigger
conditions that leave a useful procedure routed poorly, drift between a skill's main document and its
attached scripts, low-quality skills accumulating faster than libraries can curate them, and systems
that are far better at adding skills than at safely rewriting or retiring them.

## When It Applies

The format applies where an agent needs domain expertise — workflows, context and best practices —
that would otherwise be restated in every conversation. In the arrangement Anthropic documents, it
assumes an execution environment giving the model filesystem access and the ability to run
commands.

The documentation is direct about the security assumption the format carries: Skills should be used
only from trusted sources, because they give the model new capabilities through instructions and
code, and a malicious Skill can direct the model to invoke tools or execute code in ways that do not
match its stated purpose. It advises auditing every bundled file, singles out Skills that fetch data
from external URLs as particularly risky since fetched content may itself contain malicious
instructions, and
recommends treating installation like installing software. Enterprise organizations are offered
content scanning for custom Skills uploaded through claude.ai and Claude Cowork; the documentation
notes it does not cover Skills uploaded through the Skills API or the Console. The engineering post
gives the same advice in its own terms, warning that a malicious skill may introduce vulnerabilities
in the environment where it is used, exfiltrate data, or direct the model to unintended actions, and
asking that a skill from a less-trusted source be read through before use with attention to its code
dependencies, its bundled resources such as images or scripts, and any instruction connecting to
untrusted external network sources. Both accounts propose manual audit rather than any mechanism the
format itself supplies.

## Evidence and Limitations

Google reports building a skill for the Gemini API
([[SoftwareApplication/gemini-api-developer-skill]]) and evaluating it against a harness of 117
code-generation prompts, finding that it raised results markedly for its newer models with strong
reasoning support and much less for older ones — a result Google reads as skills working, but
depending on the model's reasoning ability rather than on the skill alone. The method and figures
are on [[BlogPosting/closing-the-knowledge-gap-with-agent-skills]].

The Mercari account above is the only source here reporting an evaluation of a skill's own
*structure* rather than of what a skill adds. Its method is worth the caveat: the scores come from
an evaluation skill the same author wrote, run against a dataset the same author assembled from real
improvement topics, against criteria — understanding accuracy, spec specificity, feasibility, UX
validity — the same author defined before implementing. The post gives no figures, describing the
improvement as clear rather than quantifying it, and reports the author's own reasoning about why a
shorter file scored better rather than an experiment isolating that variable. Defining the criteria
first is itself presented as a method, which the post calls Prompt TDD.

Anthropic's own engineering post reports no evaluation or measurement of the format. Its claim that
the context bundled into a skill is effectively unbounded is an architectural argument about what a
filesystem-backed agent need not read, not a measured result, and its account of the format's
benefits is the designer's own.

Two limitations are named by the Google authors. They say they know from Vercel's work that direct
instruction through [[DefinedTerm/agents-md]] can be more effective than using skills, and that they
are therefore exploring other routes to supplying live SDK knowledge, such as MCP servers for
documentation. The Vercel evaluation itself is not among this wiki's sources, so what is recorded
here is what the Google authors say they take from it.
The second is maintenance: Google states there is no good skill update story beyond asking users to
update manually, and warns this could in the long term leave stale skill information in users'
workspaces, doing more harm than good. That concern cuts against the purpose the format is being put
to here, since a mechanism adopted to keep an agent current can itself go out of date in place.

Anthropic states two directions as intentions rather than shipped behaviour: exploring how Skills can
complement [[DefinedTerm/model-context-protocol]] servers by teaching agents workflows that involve
external tools, and enabling agents to create, edit and evaluate Skills on their own.

## Related Terms

- [[DefinedTerm/progressive-disclosure]] — the loading strategy the format is built around
- [[DefinedTerm/context-engineering]] — the broader concern this format addresses
- [[DefinedTerm/agents-md]] — another file-based convention for giving an agent standing instructions
- [[SoftwareApplication/claude-code]] — one of the products the format is available in
- [[SoftwareApplication/openai-codex]] — another product documented as supporting the format
- [[DefinedTerm/procedural-gap]] — the shortfall the research literature presents skills as bridging
- [[ScholarlyArticle/comprehensive-survey-on-agent-skills]] — a survey organizing agent-skill research around a lifecycle
