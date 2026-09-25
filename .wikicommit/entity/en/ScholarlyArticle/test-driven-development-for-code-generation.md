---
title: "Test-Driven Development for Code Generation"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-generation, test-driven-development, execution-feedback]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2402.13521'
    hash: sha256:472dd21e000f1fab72f8d9c9f7bcf1e89cac69d6fc3f4a33f7023718663ee78a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An empirical study from the University of Waterloo of whether test-driven development can be incorporated into LLM code generation, finding with GPT-4 Turbo and Llama 3 that supplying human-written tests alongside the problem statement, and running a remediation loop on failing tests, solves more problems on MBPP, HumanEval and a set of 1,100 CodeChef problems."
  author: ["Noble Saji Mathews", "Meiyappan Nagappan"]
  keywords: ["code generation", "LLM", "TDD", "testing", "software engineering"]
---

The paper asks whether test-driven development (TDD), in which developers write tests before functional code, can be incorporated into AI-assisted code generation. Its hypothesis is that giving an LLM tests in addition to the problem statement improves the generated code, and that tests written up front let developers verify generated code against predefined expectations. The authors stress that it deliberately does not ask when or how AI should write tests: the tests supplied are human-written, and their contribution is the empirical study rather than the framework used to run it.

That framework, TGen, takes a problem statement and a set of supplied tests. A coder agent generates code; a verifier runs it with PyTest against the available tests; and, on failure, a remediation agent reads the failures and suggests fixes that the coder agent applies in the next iteration, for at most five iterations or until the same tests fail three times. Each problem is first attempted from the statement alone, then with all public tests supplied, then with the remediation loop, and the evaluation uses GPT-4 Turbo (v1106) with results validated using Llama 3 70B Instruct. Benchmarks are the EvalPlus versions of MBPP (399 problems) and HumanEval (164), whose extra tests are never shown to the model and serve as private tests, and a curated set of 1,100 CodeChef problems, 100 from each of 11 difficulty levels, for whole-file generation.

## Key Points

- With GPT-4 Turbo, supplying tests solved an additional 12.0% of MBPP and 8.5% of HumanEval problems, and the remediation loop a further 2.8% and 3%.
- After validation with EvalPlus's private tests, supplying tests improved correctness by 12.78% on MBPP and 9.15% on HumanEval, and remediation by a further 5.26% and 5.49%.
- On the 1,100 CodeChef problems, performance was markedly lower and fell sharply as difficulty rose; tests and remediation together still improved correctness by 7.27% when solutions were judged by CodeChef's private tests.
- With Llama 3, which solved fewer problems unaided, the improvement from tests and remediation after private-test validation was larger: 38.6% on MBPP and 21.95% on HumanEval, almost double what GPT-4 gained.
- Adding more tests generally increased correctness, but in some cases additional tests caused previously solved problems to fail, which the authors suggest may be the [[DefinedTerm/lost-in-the-middle]] problem.
- Manual inspection suggested tests helped most with function signature mismatches, mathematical formulas, precise string manipulation, complex data structures and edge cases, while persistent failures involved misunderstood core logic, specific data structures, input/output formats and performance limits.
- Remediation advice tended to become repetitive after three to four iterations, and no problem that used all five remediation attempts was solved.

## Notes

The authors acknowledge that MBPP and HumanEval do not capture the full complexity of real-world programming, that their difficulty-graded CodeChef set may not represent software engineering tasks, that treating test runs as ground truth may not hold for non-deterministic problems (which they excluded), and that LLM output remains somewhat unpredictable despite a fixed seed and temperature 0. They conclude by advocating widespread adoption of test-driven methodologies with LLMs for code generation, and note that the supplied tests' quality determines how well solutions capture implicit requirements.
