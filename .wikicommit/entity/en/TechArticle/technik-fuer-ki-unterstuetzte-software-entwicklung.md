---
title: "Technik für KI-unterstützte Software-Entwicklung"
type: "schema:TechArticle"
lang: en
tags: [ai-assisted-development, llm, open-source, fine-tuning]
sources:
  - type: url
    url: 'https://www.ossbig.at/wp-content/uploads/2025/08/Technik-fuer-KI-unterstuetzte-Software-Entwicklung-V1.0.pdf'
    hash: sha256:7c8de00fd94555d11c322bdb8d1b58eeea14c17a666703d5b7cc52eec52d612f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A German-language guide, version 1.0, from an OSSBIG working group on the technical use of generative AI in organizations with a focus on AI-assisted software development. It covers how LLMs work and fail, how to operate them, prompt engineering, integration, MLOps and security, and reports the group's own experiments."
  author: ["OSSBIG working group \"KI-unterstützte Softwareentwicklung\""]
  publisher: "OSSBIG"
---

*Technik für KI-unterstützte Software-Entwicklung* ("technology for AI-assisted software development"),
version 1.0, is a German-language guide produced by the OSSBIG project "KI-unterstützte
Softwareentwicklung". That project began in autumn 2023 as an OSSBIG working group, prompted by the
finding that a lack of technical know-how was a major obstacle to adopting this new branch of IT. The
contributors state that they worked on it
voluntarily and without commercial interest, and that parts of the text were produced with generative AI
from a base text the team wrote and then revised by the group.

The guide presents itself as a practice-oriented guide to integrating generative AI into software
development, aimed at IT managers, operations staff, decision-makers and developers who want to plan,
implement or oversee its use in an enterprise setting. Its focus is automating recurring tasks such as
code completion, error detection and testing. Governance is explicitly out of scope and is left to a
separate OSSBIG recommendation document.

## Details

- **Benefits.** The guide lists the potential of AI across the development process — code generation and
  completion, automated testing and debugging, security analysis, CI/CD, documentation, refactoring,
  migration between languages, and low-code/no-code development — and summarizes it as faster, more
  efficient development. It notes that hallucinations are a smaller problem for code completion because
  quality can be enforced with, for example, unit tests.
- **How LLMs work and fail.** It explains the transformer architecture at a general level, describes ways
  of evaluating LLM output (user feedback, A/B testing and word-based metrics), and lists weaknesses:
  inaccuracy with no built-in way to verify output — which it calls a major problem for generated code,
  since hard-to-spot security holes or bugs can slip in — hallucination, poor recognition of document
  structure and loss of context in long dialogues, gaps in domain knowledge, overfitting and
  underfitting, bias, lack of transparency, and resource intensity.
- **Operating LLMs.** It contrasts closed-source models, reachable only through a provider's endpoint and
  billed per input and output token, with open-source models — strictly, open-weights models — that can
  run on-premise or with an external provider. It weighs on-premise operation (data stays in-house, no
  vendor dependency, but maintenance, patching and in-house security) against cloud operation
  (pay-as-you-go, less infrastructure upkeep, easy experimentation, but models that change underneath
  the application and vendor lock-in), and notes that finding providers with enough GPU capacity was
  difficult.
- **[[DefinedTerm/prompt-engineering]].** It distinguishes the system prompt, usually hidden from the end
  user, from the user prompt, and stresses that small changes in wording can change the result
  substantially. For most applications, it concludes, developing or fine-tuning a model is unnecessary,
  and prompt engineering can often improve answer quality instead.
- **Integration and MLOps.** It names [[SoftwareApplication/langchain]] as a well-known framework for
  building an LLM into business logic, including retrieval-augmented generation over one's own documents,
  and notes that MLOps for LLMs differs from DevOps: models are rarely retrained, but resources are more
  expensive, prompt engineering is added, and monitoring and evaluation must deal with tasks that have no
  single correct answer.
- **Security.** It points to the OWASP Top 10 for LLM applications, notes that retrieval over internal
  documents with a closed-source model sends those documents to an external provider while a locally run
  model keeps them in-house, and warns operators of public chatbots against
  [[DefinedTerm/prompt-injection]].

The final chapter reports the working group's own experiments:

- **An open-source coding assistant.** The group ran Hugging Face's open-source IDE plugin against
  LLMs served over HTTP. The IntelliJ version had to be forked and patched to work behind a corporate
  proxy with self-signed certificates, and later became incompatible when the shared language server was
  adapted for the VS Code version. Hosted inference endpoints were used to test models including
  StarCoder and CodeLlama.
- **Fine-tuning on a codebase.** A StarCoder model fine-tuned on two open-source projects began suggesting
  those codebases' data structures, but the overall quality of its suggestions was much worse than before
  fine-tuning; the group attributes this to training on whole codebases without analysis, training past
  the optimal point, and too little time to tune parameters.
- **Other experiments.** Offloading the main matrix multiplications of the llama2.c inference program to
  the GPU with CUDA roughly tripled generation speed, from about 6 to about 17 tokens per second, and
  showed why a model has to be held entirely in GPU memory; a self-hosted web chatbot proved easy to
  build; and deploying a GPT-3.5 model on Azure was quick, though Azure's many options were hard to keep
  track of.
