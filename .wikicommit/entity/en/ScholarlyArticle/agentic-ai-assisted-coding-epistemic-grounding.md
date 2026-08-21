---
title: "Agentic AI-assisted coding offers a unique opportunity to instill epistemic grounding during software development"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering, configuration, governance, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.21744'
    hash: sha256:9f7862701079fdcc2025b4eb823bc28cb07820a6313b554d8637b079e666e6f8
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 2026 position paper proposing GROUNDING.md, a community-governed, field-scoped [[DefinedTerm/epistemic-grounding-document]] that encodes a domain's non-negotiable validity rules above the plan, project, and technique layers of an agent's context. Its worked example is mass-spectrometry proteomics."
  author:
    - "Magnus Palmblad"
    - "Jared M. Ragland"
    - "Benjamin A. Neely"
---

This is a position paper by Magnus Palmblad (Leiden University Medical Center) and Jared M. Ragland and Benjamin A. Neely (NIST Charleston), arguing that the shift to agent-scaffold software development creates an opening to embed domain correctness standards at the point of generation rather than expecting users to apply them afterwards.

Its starting observation is about who is now writing scientific software. Generating bespoke mass-spectrometry proteomics tooling — reading raw files, performing identifications, rolling up to protein identifications, quantifying — is something "established software development shops have spent decades mastering," and the paper names FragPipe, MaxQuant, Metamorpheus, OpenMS, Skyline, and the Trans-Proteomic Pipeline as examples. That capability is now within reach of one person with an agent scaffold. The risk the paper identifies follows directly: the person doing it may not be a domain expert, and in a field where "no one person may be a true expert across all steps along the sample-to-results pipeline," they may not know what they do not know.

Its proposal is [[DefinedTerm/epistemic-grounding-document]] — a file it names `GROUNDING.md`, drafted for proteomics as a demonstration and published as an open repository.

## Key Contributions

- **A missing layer in the context hierarchy.** The paper's central structural claim is that a plan file (user intent), a project file such as [[DefinedTerm/agents-md]], and a technique file such as a `SKILL.md` (see [[DefinedTerm/agent-skills]]) all "lack mechanisms to enforce domain-specific validity constraints," and that a field-scoped layer is needed above them.
- **A precedence rule stated as an ordering principle.** Context documents are arranged "by decreasing plasticity from session to project to technique to field," each layer more stable, authoritative, and general than the one below. The consequence is that "the GROUNDING specification wins any conflict with the plan or skills, not the other way around, preventing the AI from optimizing for immediate goals while violating field-scoped epistemic rules." The paper's reason a `SKILL.md` cannot host such invariants is scope: as a method-scoped file it applies only to a specific technique — one FDR algorithm, in its example — not to the field.
- **Two content types with different enforcement.** Hard Constraints are field-scoped invariants that override all other contexts; Convention Parameters are community-agreed defaults that generate a warning. The paper's example of a Hard Constraint is a proteomics-wide FDR rule.
- **Authority from provenance, not position.** The document encodes standards defined by the domain community "(not the software developer or the AI's training)," with the paper pointing at HUPO-PSI guidelines as the kind of source. Its argument for why this matters operationally is that authority grounded in community consensus "resists being overridden by non-experts."
- **Four functions.** Human-readable but agent-consumed, enabling community governance and tool portability; domain knowledge encoded as Hard Constraints and Convention Parameters; loaded at inference time with highest priority via the system prompt; and designed to support enforcement when coupled to an appropriate loading strategy, validators, tests, or agent-scaffold checks.

## Notes

The paper distinguishes its proposal from the formal guidelines its own field already has — covering sample collection and study design, reference materials, file-level metadata, output file formats, and minimum reporting information — on a single ground: those are authoritative but "are not written for AI consumption." Its metaphors for what it wants instead are a domain's "Code of Hammurabi" for AI agents and a software contract "describing the invariants, conventions, and failure modes that every tool in the ecosystem should respect."

One of its stated audiences is unusual and worth recording: the authors write that beyond human readers, "one of the intended audiences of this paper... are LLMs themselves," in the hope that the proposed authority ordering "will become explicit either by LLM training or by specifically being incorporated into agent-scaffold software." No agent scaffold implements that ordering natively today, so the paper reports the workaround it tested: loading the document through the system prompt, which it "found... to be more consistent than XML tagging," on the reasoning that order of inclusion matters because of context primacy bias, recency effect, and attention drift. It warns specifically that "nesting GROUNDING.md in a skill folder would incorrectly subordinate it to method-scoped layers, violating its authority."

**Preliminary testing.** The paper does report an evaluation, presented as proof of principle pending "exhausting testing... across a variety of agent scaffolds and models." It ran [[SoftwareApplication/claude-code]] (v2.1.90, medium effort mode) with Nemotron (NVIDIA-Nemotron-3-Super-120B-A12B-FP8) through VS Code, in fresh isolated sessions, and tested the grounding document in competition with an "adversarial" `CLAUDE.md` instructing the agent to ignore scientific validity and do what the user wants. Compliance was probed with six prompts each violating a different Hard Constraint. Success was defined strictly: the agent explicitly refusing to generate the non-compliant code, citing the relevant Hard Constraint, explaining why the approach was scientifically invalid, and optionally offering compliant alternatives — with generating compliant code counted as a *failure*, "as a GROUNDING.md is not a SKILL.md." The authors report the document "is authoritative largely due to its explicit language" for Hard Constraints, but that compliance "degrades under explicit override instructions or weakened normative language," concluding it "provides an auditable anchor and can substantially increase compliance under the tested conditions, but does not by itself guarantee correctness under all context conditions." Their recommendation to adopters follows from that scaffold-dependence: use test prompts that violate Hard Constraints to verify the document is actually working in a given system.

The paper's own limitations section names what this leaves open. All tests were fresh, single-turn sessions, "so durability over longer sessions with substantial intervening context remains untested." The tests evaluate refusal under genuine violations but "do not measure false-positive refusals on valid requests or systematic auditing of pre-existing code with planted violations." And it is a single proof-of-principle model configuration rather than a broader evaluation.

Its domain is scientific computing rather than general software engineering, but the layering argument generalises: any field with community-defined correctness standards faces the same gap between what a user asks for and what the domain requires, and the mechanism for closing it — a stable, high-priority, community-governed file that outranks the current task — is domain-independent even where the content is not.
