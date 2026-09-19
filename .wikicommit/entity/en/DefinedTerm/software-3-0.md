---
title: "Software 3.0"
type: "schema:DefinedTerm"
lang: en
tags: [llm, terminology, context-engineering, prompting]
sources:
  - type: url
    url: 'https://karpathy.bearblog.dev/sequoia-ascent-2026/'
    hash: sha256:5f0fc28c7d2ce3663820af50aba485b5ec93384a47528a92d2935967dd678dc4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Andrej Karpathy's name for programming a large language model through prompts, context, tools, examples, memory and instructions, as the third step after hand-written code and learned weights — with the context window as the lever and the model as the interpreter that computes over it."
---

Software 3.0 is the third step in a sequence Andrej Karpathy sets out for how a computer gets
programmed, after Software 1.0, in which humans write explicit code, and Software 2.0, in which
humans assemble datasets, objectives and neural network architectures and the program is learned
into weights. In Software 3.0 the program is expressed as prompts, context, tools, examples, memory
and instructions, and the large language model is the interpreter: what sits in the context window
is the lever over it, and the computation it performs is over digital information. His account of
how this became possible is that a model trained on a sufficiently large set of tasks — the
internet containing many — becomes, implicitly, a programmable computer.

## Usage

The example Karpathy uses to make the shift concrete is installation. Targeting many platforms and
machine configurations with a shell script, he argues, forces the script to balloon with
conditionals because the Software 1.0 universe requires spelling out every detail in exact code.
The alternative he points to is an install procedure distributed as a block of text to paste into
an agent: the agent reads the local environment, takes intelligent actions, debugs errors in the
loop and completes the setup. He describes that as a different kind of program — less precise, but
more adaptive — and draws the practical consequence that "what is the piece of text to copy-paste
into your agent" is itself now a programming question.

His second example runs the argument further, to software that stops existing. A menu-photo app he
built in the ordinary way needed OCR, an image generator, a frontend, deployment, auth, payments,
secrets and infrastructure; the Software 3.0 version is handing the photo to a multimodal model and
asking it to render the dish images onto the menu image directly. On his reading the old stack was
scaffolding around a transformation the model can now perform itself, and the founder-facing
consequence is that some applications should not exist as applications at all. He extends the same
logic speculatively to hardware, imagining neural networks as the host process with CPUs as
coprocessors, while saying the path there will be piecemeal.

The framing also carries past code. Karpathy argues that classical programs worked over structured
data, and that the newly automatable thing is information processing that was not previously
programmable at all — his example being an agent that incrementally compiles messy documents into a
persistent Markdown knowledge base of summaries, entity pages, concept pages, contradictions and
cross-links. His recommended question is therefore not only which existing workflow AI can speed
up, but which information transformation was impossible before and is now natural.

## When It Applies

The paradigm's trade is stated plainly by its author: it buys adaptiveness at the cost of
precision, so it suits work where the environment varies and an exact specification would be
brittle, and it assumes a model capable enough to act and debug in the loop. It is one person's
framing rather than an industry-agreed term, and this account of it comes from a talk write-up
whose prose was produced by a model from the event transcript and then checked by him.

## Related Terms

[[DefinedTerm/context-engineering]], [[DefinedTerm/jagged-intelligence]], [[DefinedTerm/prompt-engineering]], [[DefinedTerm/agentic-engineering]]
