---
title: "FIDES"
type: "schema:DefinedTerm"
lang: en
aliases: ["Flow Integrity Deterministic Enforcement System"]
tags: [agents, security, agent-safety, agent-architecture]
sources:
  - type: url
    url: 'https://github.com/microsoft/agent-framework/blob/main/docs/decisions/0024-prompt-injection-defense.md'
    hash: sha256:51eb7a8188be72cbaed8c44f9f3fb847df2aaacf057d21f16ab59e9312c5d6d9
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A label-based information-flow-control defence against prompt injection, proposed for Microsoft Agent Framework in an architecture decision record. It attaches integrity and confidentiality labels to content, propagates them through middleware, holds untrusted content outside the model's context behind variable references, and processes it only in a quarantined path."
---

FIDES — expanded in the source as Flow Integrity Deterministic Enforcement System — is a
label-based security design intended to stop untrusted external content from influencing what an
AI agent does. It is the option chosen in an architecture decision record in Microsoft's
`agent-framework` repository, dated 14 January 2026 and carrying the status *proposed*, which
credits the design to Costa et al. (2025) and lists that work on information-flow control for AI
agents among its references.

The problem the ADR states is that traditional defences against [[DefinedTerm/prompt-injection]]
rely on heuristics and prompt engineering, which are not deterministic and can be bypassed. What
it sets out to obtain instead is a systematic mechanism that prevents untrusted content from
influencing agent behaviour, gives verifiable security guarantees, maintains audit trails for
compliance, and integrates non-invasively with the framework's existing middleware pipeline while
staying opt-in and backwards compatible.

## Usage

The ADR describes four core components:

- **Content labelling** — an `IntegrityLabel` (TRUSTED / UNTRUSTED) and a `ConfidentialityLabel`
  (PUBLIC / PRIVATE / USER_IDENTITY), combined under a most-restrictive-wins policy.
- **Middleware-based enforcement** — a `LabelTrackingFunctionMiddleware` that propagates labels
  automatically, and a `PolicyEnforcementFunctionMiddleware` that checks policy before a call
  executes.
- **Variable indirection** — a `ContentVariableStore` and `VariableReferenceContent` that keep
  untrusted content physically isolated from the LLM's context.
- **Quarantined execution** — `quarantined_llm` and `inspect_variable` tools that process
  untrusted data in isolation, with audit logging.

For remote MCP integrations the ADR adds two mechanisms. MCP `ToolAnnotations` such as
`readOnlyHint` and `openWorldHint` are mapped onto FIDES tool properties
(`source_integrity`, `accepts_untrusted`, `max_allowed_confidentiality`), and a server's
`_meta.ifc` result metadata is parsed into per-item `security_label` values so that
provider-supplied labels are enforced by the middleware. Its implementation notes state that a
`SecureMCPToolProxy` applies these labels automatically on connecting an MCP tool or URL, that for
servers advertising `X-MCP-Features: ifc_labels` the `_meta.ifc` labels are authoritative, and
that any tool not explicitly marked `readOnlyHint=True` is treated as a potential sink defaulting
to `max_allowed_confidentiality=PUBLIC` to prevent exfiltration. Unlabelled content defaults to
UNTRUSTED.

The ADR weighs FIDES against four alternatives it rejects: prompt engineering defences, which it
calls non-deterministic and bypassable; content sanitization, which it calls computationally
expensive, high in false positives and unable to handle novel attacks; separate agent instances,
which it accepts give strong isolation but at high overhead and with difficult cross-instance
state; and runtime monitoring alone, which it calls reactive rather than proactive and says cannot
provide preventive guarantees.

## When It Applies

The ADR presents FIDES as opt-in and fully backwards compatible: agents without the security
middleware function normally, no core content types or agent logic change, and policies are
configurable per agent or tool. Its stated prerequisites are the framework's existing
`FunctionMiddleware` base class, labels carried on `additional_properties` so no schema changes
are needed, and `SerializationMixin` for label persistence.

Its own list of drawbacks is equally explicit. The middleware adds latency to every tool call and
the variable store consumes memory for untrusted content; developers must understand the label
system and configure tool policies by hand, including an explicit allowlist of tools that accept
untrusted input; most-restrictive-wins propagation may be overly conservative in some cases; and
the design does not defend against all attack vectors, training-data poisoning being the example
it gives. Two items — performance benchmarks and user acceptance testing — are left unchecked in
the document.

How well-established this is, is stated by the document's own header: it is an architecture
decision record carrying the status *proposed*, so what it records is a decision put forward
within a single framework. The record says nothing either way about whether the design has
shipped or been evaluated outside it.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack class this design targets
- [[DefinedTerm/indirect-prompt-injection]] — the variant that arrives through retrieved content
- [[SoftwareApplication/microsoft-agent-framework]] — the framework this ADR belongs to
- [[DefinedTerm/model-context-protocol]]
