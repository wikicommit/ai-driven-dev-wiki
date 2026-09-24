---
title: "The Semi-Executable Stack: Agentic Software Engineering and the Expanding Scope of SE"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-engineering, software-engineering, governance, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.15468'
    hash: sha256:aa9d37128ca41d514105f0cdba213b9927d9c67a443d492554454b40d545252f
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A conceptual paper, written up from a keynote at the Agentic Engineering 2026 workshop, arguing that agentic AI expands what software engineering engineers — from executable code outward to semi-executable artifacts — and introducing the Semi-Executable Stack, a six-ring diagnostic reference model for locating where a contribution or bottleneck sits."
  author: ["Robert Feldt", "Per Lenberg", "Julian Frattini", "Dhasarathy Parthasarathy"]
  abstract: "AI-based systems driven by LLMs and tool-using agentic harnesses are increasingly discussed as a threat to software engineering. The paper argues instead that the thing being engineered expands beyond executable code to semi-executable artifacts — combinations of natural language, tools, workflows, control mechanisms and organizational routines whose enactment depends on human or probabilistic interpretation. It introduces the Semi-Executable Stack, a six-ring diagnostic reference model, develops the argument through three worked cases, reframes familiar objections as engineering targets, and closes with a preserve-versus-purify heuristic for legacy software engineering practices."
  keywords: ["agentic software engineering", "semi-executable artifacts", "reference model", "socio-technical systems", "SE4AI"]
---

This paper is the write-up of a keynote titled "Agentic Software Engineering Will Eat the World:
AI-Based Systems as the New Operating System of Society", given at the Agentic Engineering 2026
workshop in Rio de Janeiro on April 14, 2026; its authors are affiliated with Chalmers University of
Technology and Volvo Group. It starts from the anxiety that stronger foundation models and
tool-using agents make tasks such as scaffolding, routine test generation, straightforward bug fixing
and small integration work look exposed, and that experienced practitioners worry their expertise
will lose value. The authors take those concerns seriously but draw a different conclusion: agentic
systems do not make software engineering smaller, they expand the engineering object outward, from
code and tests toward prompts, workflows, controls, organizational operating logic and eventually
societal and institutional fit.

The paper's central concept is the [[DefinedTerm/semi-executable-artifact]] — an artifact that helps
specify, coordinate or constrain a software-intensive system's behavior but whose enactment depends on
interpretation by humans, probabilistic models or both. Around it the authors build the Semi-Executable
Stack, a six-ring reference model whose purpose is diagnostic: to show which ring a contribution or
bottleneck primarily inhabits and which adjacent rings it depends on. The paper describes itself as
diagnostic and agenda-setting rather than empirical, and explicitly not a maturity model, a complete
process framework or an evaluation rubric.

## Key Points

- The paper argues that three observations push the engineered object outward even before any agentic
  system matches expert engineers: organizational change is triggered by adequacy against how scarce
  expert attention is actually allocated, not by parity with the best human engineer; thousands of
  low-friction uses compound into capability that sporadic access to a top expert cannot match; and
  lowering the barrier to creation, as end-user software engineering showed, raises rather than lowers
  the demand for engineering discipline.
- The stack's six rings are executable artifacts (code, tests, schemas, configurations); instructional
  artifacts (prompts, natural-language specifications, task descriptions, exemplars); orchestrated
  execution (tool use, retrieval, agent workflows, multi-agent protocols, human-agent loops); control
  systems (guardrails, monitoring, evaluation harnesses, policy layers, escalation rules); operating
  logic (decision preparation, coordination routines, delegation structures); and societal and
  institutional fit (regulatory fit, institutional legitimacy, cross-organizational integration).
- The rings mark regions on a spectrum of specification completeness and execution determinism, with
  blurry boundaries; the authors state that they are not lifecycle phases, maturity levels or runtime
  layers. Historically software engineering centered on ring 1 and partly ring 2; the claim is that
  rings 2–5 increasingly become first-class engineering objects while ring 6 increasingly constrains
  what succeeds.
- A contribution's primary ring is identified by asking whether the system's value would collapse if
  that ring's artifact were removed or poorly designed. The paper pairs the rings with a behavioral
  question — whether a change mainly affects individual cognition, team coordination or organizational
  routines — treating behavioral software engineering as a cross-cutting lens rather than a seventh ring.
- Three worked cases illustrate the diagnosis: an automated automotive API-testing pipeline sits mainly
  at rings 2–3, an LLM-based multi-agent system for automotive release go/no-go decisions sits at
  ring 5 supported by rings 3–4, and a field experiment on AI and teamwork outside software sits at
  ring 5. As the primary object moves outward, the authors argue, the evaluation criteria, required
  skills and unresolved bottlenecks shift with it.
- Five common objections are reframed as engineering moves: reliability failures (rings 1–3) make
  verification and oversight core artifacts; maintenance debt (rings 2–4) calls for versioning prompts
  and workflow logic and tracking evaluation suites alongside code; organizational inertia (rings 4–5)
  makes adoption an engineering concern; power and politics (rings 4–6) make governance one; and the
  judgment that resists automation (rings 5–6) moves the center of gravity outward. The authors add
  that where failures would be catastrophic and irreversible, or the needed controls cannot yet be
  built, some deployments should not happen yet.
- The preserve-versus-purify heuristic keeps durable principles — explicit reasoning about requirements,
  modularity and interfaces, validation and verification, traceability, lifecycle thinking and
  socio-technical realism — and purifies practices that mainly compensated for older constraints, such
  as those optimized for manual code production, process artifacts built for low-bandwidth human
  coordination, and strict phase boundaries inside interactive human-agent loops.
- For researchers, the paper names SE4AI work at rings 5 and 6 — decision routines, operating logic,
  governance and institutional fit — as the most underserved frontier. For practitioners it suggests a
  diagnostic: name the ring whose failure would kill a project and the adjacent rings it depends on,
  and compare them with the ring receiving most of the engineering effort; when they diverge, the
  authors say, projects tend to stall.

## Notes

The authors position the stack alongside several literatures rather than replacing them: AI4SE surveys
and agentic-coding benchmarks such as [[Dataset/swe-bench]], which they place mainly in rings 1–3;
MLOps and holistic evaluation work at ring 4; socio-technical and behavioral software engineering; and
work on AI governance, including the EU AI Act and NIST's AI risk-management framework, at rings 5 and
6. They also point to developer systems such as [[SoftwareApplication/claude-code]], where prompts,
repository instructions, tool permissions and reusable skills partly encode how work should proceed,
as evidence that the shift is already visible in practice.

Limitations the authors state: the stack is a reference model rather than an empirical result; two of
the three cases share an automotive industrial context and the third demonstrates portability rather
than full generalization; the evidence base for the outer rings is thinner, so claims there are
directional; and ring assignment is often ambiguous, with the stack meant to support that discussion
rather than adjudicate it.
