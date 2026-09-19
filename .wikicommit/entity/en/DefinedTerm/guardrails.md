---
title: "Guardrails"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, security]
sources:
  - type: url
    url: 'https://about.gitlab.com/the-source/ai/implementing-effective-guardrails-for-ai-agents'
    hash: sha256:fec4dd1d58e4a51a864185fa402e79f338ebea7e0e5f125356978be821500ca8
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
  - type: url
    url: 'https://github.com/NVIDIA-NeMo/Guardrails'
    hash: sha256:5e355c13851c1bcdbfecb01c03581fb7ca7d93a287620f15481e621963cc9832
  - type: url
    url: 'https://platform.openai.com/docs/guides/agent-builder-safety'
    hash: sha256:86e2fc5f860675a072304196ba8e912392902e82d2ffeb390665f20c928e7016
  - type: url
    url: 'https://www.anthropic.com/news/building-safeguards-for-claude'
    hash: sha256:6a49d6c32820761dc21bf0f49ae31d6b9fbf8fca45f239601c5fb33ac418abf1
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A term used at five different layers for the controls placed around an AI agent — organizational access controls, approval gates and audit trails; application-level classifiers screening what reaches and leaves the model; deterministic framework-level rules evaluated before a tool call runs; a programmable layer interposed between application code and the model, carrying its own configuration language; and enforcement the model provider runs on its own deployed models in real time, through classifiers, response steering and account-level action. The sources here do not share one definition, and none of them is the agreed one."
---

Guardrails are the policies, controls and mechanisms placed around an AI agent to constrain what it is permitted to do. The word is used at several layers and the sources here do not share one definition of it, so no single formulation below should be read as the agreed one.

One account, set out in [[BlogPosting/implementing-effective-guardrails-for-ai-agents]], is organizational and specific to software delivery: on it, guardrails are a comprehensive framework of policies, controls, and monitoring mechanisms that govern how AI agents interact with a development environment, and the concept is described there as extending beyond traditional security controls — ensuring AI systems operate safely and effectively while complying with organizational policies and regulatory requirements, as agents take on sensitive operations such as autonomous code generation and automated infrastructure management that traditionally required human oversight.

That is the first of four accounts, and they approach the word from different ends and are worth keeping apart. The first is organizational, describing the access controls, approval gates and audit trails an enterprise places around an agent's actions. A second is application-level, describing the classifiers and filters a developer places around an agent's inputs and outputs. A third is framework-level and deterministic, placing rules in code that runs outside the model and decides whether a tool call may execute at all. A fourth is a toolkit layer interposed between application code and the model, in which rails are declared in configuration and a purpose-built language rather than written as application logic. All use the same word for the same purpose — constraining what an agent can do — but they operate at different layers and none subsumes the others. A fifth source, taken up at the end of the next section, adds no fifth layer: it restates the application-level sense in a narrower, product-specific form. One further account does add a fifth layer the other four do not reach — enforcement the model provider applies in real time to its own deployed models — and it is set out under Provider-side enforcement below.

## Usage

Based on interviews with 54 DevSecOps practitioners and leaders, that first account groups guardrails for AI agents into four categories. User roles and access controls require two-factor authentication or single sign-on before granting an AI tool system access, plus role-based access control for AI operations touching secrets, credentials, or protected branches. Limits and controls constrain what an agent's actions can do directly: blocking direct production deployment without manual review, routing AI-generated changes through the same merge-request review process as human-authored changes, requiring manual approval above defined cost thresholds, applying multiple-review requirements to infrastructure or resource deletion, and maintaining rollback capability for all agent actions. Customization lets an organization adapt these boundaries to its own operational procedures: admin-configurable forbidden commands (e.g., erasing Terraform state, changing domain names), human touchpoints scaled to customer impact, and adjustable automation levels by user role. Logging, tracking, and transparency covers audit trails that capture both AI-initiated changes and the human approvals involved, explanations for AI decisions, licensing-compliance checks on AI-generated and third-party code, and granular, compliance-driven controls over production data access.

[[TechArticle/a-practical-guide-to-building-agents]] treats guardrails at the level of a single application, and as a layered defence rather than a single control: OpenAI's position there is that one guardrail is unlikely to provide sufficient protection, and that multiple specialized guardrails used together create more resilient agents. Its worked configuration combines LLM-based guardrails, rules-based protections such as regex, and a moderation API to vet user input before a function call proceeds. That guide names seven types:

- **Relevance classifier** — keeps responses within the intended scope by flagging off-topic queries.
- **Safety classifier** — detects jailbreak and prompt-injection attempts, its example being a request to role-play as a teacher reciting the system instructions.
- **PII filter** — vets model output for personally identifiable information.
- **Moderation** — flags hate speech, harassment and violence in inputs.
- **Tool safeguards** — rate each available tool low, medium or high risk on factors such as read-only versus write access, reversibility, required account permissions and financial impact, then use the rating to pause for checks before high-risk calls or escalate to a human.
- **Rules-based protections** — deterministic measures such as blocklists, input length limits and regex filters against known threats.
- **Output validation** — prompt engineering and content checks that keep responses aligned with brand values.

The same guide gives a three-step heuristic for building them: focus first on data privacy and content safety, add new guardrails as real-world edge cases and failures appear, and optimize for both security and user experience as the agent evolves. It also stresses that guardrails are not a substitute for ordinary security engineering, and should be coupled with robust authentication and authorization protocols, strict access controls, and standard software security measures. In [[SoftwareApplication/openai-agents-sdk]] this is realised as an `@input_guardrail` function whose `tripwire_triggered` output interrupts the run, with guardrails executing concurrently with the primary agent rather than ahead of it.

The last safeguard in that guide's treatment of guardrails is not a filter at all: it treats planning for [[DefinedTerm/human-in-the-loop]] intervention as a critical safeguard, naming two triggers — exceeding failure thresholds, and high-risk actions that are sensitive, irreversible or high-stakes.

A third account places guardrails lower still, in the agent framework itself rather than in a classifier or an organizational process. On this framing, described in [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]], a guardrail expressed as prose — in a system prompt or a tool's docstring — is input the model interprets and re-decides on every call, so it constrains nothing reliably; that post's example is an agent that confirms a booking without the payment its tool docstring requires, and reports success. The guardrail it proposes instead is a deterministic rule evaluated by a pre-execution interceptor, which cancels the call before the tool runs and returns the violation to the model as the result. What distinguishes this sense from the classifier-based one above is not the layer alone but the kind of decision: these rules are boolean predicates over a tool call's parameters rather than probabilistic judgements about content, and the post reports zero false positives and zero false negatives across its three demonstration scenarios. That determinism is bounded by what has been written down — the post states that a rule must be explicitly defined for each operation to be protected, so an operation nobody wrote a rule for is not covered. See [[DefinedTerm/neurosymbolic-validation]] for the pattern and [[DefinedTerm/agent-hooks]] for the interception mechanism it relies on.

A fourth account comes from a toolkit rather than a framework or a policy document, and its
distinguishing move is to place the guardrails *between the application code and the LLM* as a layer
of their own. [[SoftwareApplication/nemo-guardrails]] calls these **programmable guardrails**, or
rails, and defines them as specific ways of controlling a model's output — its examples being not
talking about politics, responding in a particular way to specific requests, following a predefined
dialog path, using a particular language style, and extracting structured data. What this account
adds to the three above is a taxonomy by position in the request rather than by organizational
layer: input rails, which may reject or alter user input; dialog rails, which influence how the model
is prompted and may substitute a predefined response; retrieval rails, which reject or alter
retrieved chunks in a RAG pipeline; execution rails, which apply to the input and output of tools;
and output rails, which may reject or alter what the model produced. Rails are declared in a
configuration folder — YAML naming the active flows, plus definitions written in
[[DefinedTerm/colang]] — rather than expressed as prose in a prompt, which places this account
closer to the deterministic third one than to the classifier-based second, while still admitting
model-based checks such as self-checking facts among its configured flows.

OpenAI's safety guidance for Agent Builder, its node-based product for building multi-agent
workflows, returns to the
application-level sense in a narrower form — and is notable less for what it adds to the taxonomy
than for how modestly it scopes the claim. There a guardrail is a node placed in a workflow to
sanitize incoming input, the two jobs named being redacting personally identifiable information
and detecting jailbreak attempts, and the same page says those nodes alone are not foolproof,
calling them an effective first wave of protection. It also draws the boundary differently from the account
above: where OpenAI's own guide treats human intervention as a guardrail-chapter safeguard, this
page keeps tool approval in a section of its own, asking that approvals stay on when MCP tools are
in use — through a dedicated approval node, so a person confirms every operation, reads included. Combining these
techniques, it says, significantly reduces the risks of [[DefinedTerm/prompt-injection]], malicious
tool use and unexpected agent behaviour — while stating separately that structured outputs and
isolation greatly reduce but do not fully remove the risk, and that even with these mitigations an
agent can still make mistakes or be tricked. That guidance is tied to a product OpenAI says it is
deprecating, with shutdown scheduled for 30 November 2026.

## Provider-side enforcement

A layer the accounts above do not cover is the one the model provider operates itself, in real time,
on its deployed models. (The four accounts above are written from the point of view of whoever builds on
a model; this one is written from the provider's. Both that contrast and the decision to treat this as a
further sense of "guardrails" are this page's own framing: the post below uses the word only of
safeguards it might build in future, and calls the mechanisms described here enforcement actions.)
[[BlogPosting/building-safeguards-for-claude]] describes Anthropic's implementation of this layer.

Its detection mechanism is a set of **classifiers** — prompted or specially fine-tuned Claude models
designed to detect specific types of policy violation in real time. Several can be deployed at once,
each monitoring a different type of harm while the main conversation flows naturally. The engineering
constraint is stated plainly: they must process trillions of input and output tokens while limiting
both compute overhead and enforcement on benign content.

What a classifier can trigger is what distinguishes this layer from a filter. **Response steering**
adjusts how the model interprets and responds to a prompt while the request is in flight — the post's
example is automatically adding instructions to the system prompt when a classifier detects an apparent
attempt to generate spam or malware — and in a narrow set of cases the provider can stop the model
responding at all. Beyond the single request, patterns of violation can lead to account-level action,
including warnings and, in severe cases, termination. So the same word covers a control that alters a
request while it is in flight rather than only screening what goes in or comes out, which is what makes
this a distinct sense rather than the application-level one relocated. The post describes this list of
enforcement actions as an "including", not an inventory, and describes separate hash-matching detection
for known child sexual abuse material alongside the classifiers on Anthropic's first-party products.

The post also places this runtime layer inside a lifecycle rather than treating it as the whole of the
work: policy development, influence on model training, pre-deployment testing, and post-deployment
monitoring surround it. One reported instance of the testing layer changing a shipped product is the
computer use tool, where pre-launch evaluation found the capability could augment spam generation and
distribution, and new detection methods, enforcement mechanisms and prompt-injection protections were
added before launch. [[DefinedTerm/computer-use]] covers the capability itself, as documented by other
vendors.

No effectiveness figures accompany any of this — the post gives no classifier precision or recall and no
false-positive rate on benign traffic — so what it establishes is that the layer exists and what it can
do, not how well it works.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/agentic-engineering]], [[DefinedTerm/neurosymbolic-validation]], [[DefinedTerm/agent-hooks]], [[BlogPosting/implementing-effective-guardrails-for-ai-agents]], [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]], [[TechArticle/a-practical-guide-to-building-agents]]
