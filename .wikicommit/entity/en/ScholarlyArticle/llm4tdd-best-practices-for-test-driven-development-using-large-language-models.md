---
title: "LLM4TDD: Best Practices for Test Driven Development Using Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [test-driven-development, code-generation, human-in-the-loop, prompting]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2312.04687'
    hash: sha256:8dd7261f465fe9cef73c017485d8354c2037091cfee1f5cf9b4a3a5e030b3056
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing LLM4TDD, a human-in-the-loop process in which a developer guides an LLM to generate code by presenting unit tests one at a time in a test-driven development cycle, with an empirical study using ChatGPT on 70 LeetCode problems and a set of best practices drawn from it."
  author: ["Sanyogita Piya", "Allison Sullivan"]
  datePublished: "2023-12-07"
  keywords: ["LLM4TDD", "test-driven development", "program synthesis", "ChatGPT"]
---

The paper explores LLM4TDD, a human-in-the-loop code generation process that modifies test-driven development to incorporate large language models. Its premise is that test code is conceptually easier to write than implementation code: a test only has to set up a state, run the method and compare actual with expected output, whereas an implementation must capture the logic that satisfies the specification. In LLM4TDD the developer writes a unit test, the LLM generates code so that the test passes, and the developer then supplies the next test and the cycle repeats. The authors argue that this keeps a degree of developer ownership over the implementation and, because the developer watches the code change incrementally in response to each test, may avoid the trust problem that black-box program synthesis faces.

In the workflow, the developer selects a problem and a test suite, sets up a code execution environment, and gives the LLM a prompt containing the first test and instructions to follow TDD principles. Generated code is run against the tests collected so far; if one fails, an inner loop sends the LLM a prompt reporting the failing test, and if the LLM keeps repeating the same code, escalating hint prompts follow — first pointing out that the code has not changed, then suggesting data structures to use. The process ends when every test in the suite passes. The authors evaluate it with ChatGPT, Visual Studio Code and 70 LeetCode problems in Python (25 easy, 24 medium, 21 hard), checking the final code against LeetCode's own test suite as ground truth.

## Key Points

- LLM4TDD produced code that passed LeetCode's test suite for 62 of 70 problems (88.5%); of the eight failures, three passed the authors' manual tests but not LeetCode's and five got stuck repeating code.
- The average ratio of tests to prompts was 5:8 rather than the ideal 1:1, for two reasons the authors observed: on 27 problems (38.6%) ChatGPT kept suggesting the same faulty code with only small changes, and on 23 (32.9%) a change that made the new test pass broke a previously passing test.
- ChatGPT made assumptions from a descriptive function name even when the test contradicted them, so the authors recommend sanitizing function names to a generic form while keeping descriptive test names.
- Tests whose input-output pairs could fit several different functions led ChatGPT to wrong assumptions; the authors recommend clear, unambiguous tests and single out integer-based problems as especially prone to accidentally ambiguous tests.
- Manually written test suites based on input space partitioning needed fewer prompts than suites generated automatically with the Pynguin tool, which on average required 2× as many prompts, rising to 2.5× on hard problems.
- Describing tests in plain text instead of test code needed on average 2.0× as many prompts, and consolidating tests into one meta-test with multiple asserts needed 1.5× as many while not stopping earlier tests from breaking; the authors recommend neither.
- Problems returning booleans needed the fewest prompts and those taking string inputs needed fewer than those taking integers.

## Notes

The study uses a single LLM (ChatGPT) and function-level LeetCode problems, and the authors name other LLMs such as Codex and other languages such as Java as future work. They also report that ChatGPT's repeated failing code bore only minor resemblance to incorrect solutions posted online, and that its performance did not appear to depend on whether a problem predated its training cutoff. The dataset of problems, test suites and prompts is published by the authors.
