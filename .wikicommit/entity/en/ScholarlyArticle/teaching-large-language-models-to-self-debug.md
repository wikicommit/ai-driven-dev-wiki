---
title: "Teaching Large Language Models to Self-Debug"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-generation, self-correction, execution-feedback, prompting]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2304.05128'
    hash: sha256:b679f7e9a946d6ef8ce5e9ec080c15a2d3f0f8dc76964f44fa48fb26ce848012
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper proposing Self-Debugging, a few-shot prompting method that teaches a large language model to debug its own predicted code by executing it and explaining it in natural language, in the manner of rubber duck debugging, without any additional model training."
  author: ["Xinyun Chen", "Maxwell Lin", "Nathanael Schärli", "Denny Zhou"]
  keywords: ["self-debugging", "code generation", "few-shot prompting", "rubber duck debugging"]
---

The paper starts from the observation that, for complex programming tasks, generating a correct program in a single attempt is hard, and that earlier ways around this either rerank many sampled candidates or train a separate code-repair model. It proposes Self-Debugging, which instead teaches a pretrained large language model to debug its own predicted code through few-shot demonstrations alone, with no additional training.

One turn of Self-Debugging has three steps: **Generation**, where the model predicts candidate code; **Explanation**, where it processes that prediction in a semantically useful way, such as explaining the code line by line in natural language or writing an execution trace for a sample input; and **Feedback**, where a message about the code's correctness is produced, either by the model itself or externally from unit-test execution. Debugging stops when the feedback says the prediction is correct or a maximum number of turns is reached. The authors liken the explanation step to rubber duck debugging, where a programmer finds bugs by explaining code line by line, and argue that it lets the model identify its mistakes without human feedback on correctness or error messages.

The method is evaluated with code-davinci-002 (Codex), gpt-3.5-turbo, gpt-4 and StarCoder on three kinds of task: text-to-SQL on Spider, where no unit tests are available; C++-to-Python translation on TransCoder, where all unit tests are; and text-to-Python on MBPP, where only one of three unit tests is shown to the model.

## Key Points

- Self-Debugging uses a pretrained model without finetuning; debugging is taught entirely through few-shot prompting.
- The paper compares several feedback formats: simple feedback that only states whether the code is correct, unit-test feedback that includes execution results, code-explanation feedback, and execution-trace feedback in which the model itself traces execution line by line (the trace is model-generated, not taken from actually running the code).
- On Spider, where there are no unit tests, Self-Debugging with code explanation improves the baseline by 2–3% and improves accuracy on the hardest problems by 9%, while simple feedback alone does not notably help because the model struggles to tell correct from wrong SQL without explanation.
- On TransCoder and MBPP, where unit tests are available, Self-Debugging improves baseline accuracy by up to 12%, and models generally benefit from richer feedback, especially when execution information is present.
- It improves sample efficiency: on Spider, applying it to a single greedily decoded prediction matches the baseline that uses 16 samples, and in the paper's words it can match or outperform baseline models that generate more than 10× as many candidate programs.
- An ablation without unit-test execution finds that code execution plays an important role, though models can sometimes still improve using self-generated feedback alone; without execution, GPT-3.5 and GPT-4 tend to be overconfident in their initial predictions.
- On Spider, the initial SQL queries it fixes are usually close to correct, with small mistakes such as wrong WHERE conditions or a missing DISTINCT keyword; on TransCoder and MBPP, 60–70% of successful fixes address output mismatches where the initial code was already close.

## Notes

The authors present Self-Debugging as related in spirit to chain-of-thought prompting, since the line-by-line explanation supplies intermediate reasoning, and contrast it with prompting-with-feedback work such as [[DefinedTerm/reflexion]] by focusing on code generation and on feedback that does not need to state the error and its fix explicitly. As future work they hypothesize that better code-explanation ability leads to better debugging, and note that in their preliminary results model-generated messages about semantic errors added nothing on top of line-by-line explanation. The copy of the paper used here is its second arXiv version, dated 5 October 2023; the authors are affiliated with Google DeepMind and UC Berkeley.
