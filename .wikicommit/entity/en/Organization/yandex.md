---
title: "Yandex"
type: "schema:Organization"
lang: en
tags: [industry]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex/articles/841436/'
    hash: sha256:ed090e4e81e25e3fc5fbdddabb08371c8ae7509c5d4943bdcadbc1d5a5459eff
  - type: url
    url: 'https://habr.com/ru/companies/yandex_cloud_and_infra/articles/1084654/'
    hash: sha256:3a39bfbcaf9b1ab426e9dd699c371ca1c03d2891de020bf64c99fa2f2c088392
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A company based in Russia whose Yandex Infrastructure team builds the development platform used inside the company and, from it, AI coding products such as Yandex Code Assistant."
  foundingDate: "1997-09-23"
  url: "http://www.ya.ru/"
---

Yandex is a company based in Russia. In this wiki it appears as a builder of AI coding tools that were first used by its own developers: the accounts available here come from its own engineering blog, so they describe how the company presents its work rather than an outside assessment of it.

Its Yandex Infrastructure team builds the platform on which the company's developers work — described in a later post as developing the tools for creating and deploying applications and services inside Yandex and supporting the infrastructure most of its developers use — and an ML laboratory inside that team developed [[SoftwareApplication/yandex-code-assistant]], an inline code-suggestion assistant that was rolled out internally before being opened for free testing on the Yandex Cloud platform.

## History

The company profile accompanying its blog gives its founding date as 23 September 1997.

## Activities & Products

According to [[BlogPosting/how-we-taught-yandex-code-assistant-to-make-developers-happy]], the code assistant was evaluated with A/B testing, which that post calls customary at Yandex, and use of the assistant inside Yandex was never compulsory — developers who did not like it could simply remove the plugin.

The SourceCraft developer-tools team, whose history that later post places in Yandex Infrastructure, began its development work in January 2024 and has since built [[SoftwareApplication/vibecraft]], a platform for creating applications from a chat without writing code, aimed at people outside programming. As [[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]] describes it, VibeCraft runs on the company's own stack: code is kept in a SourceCraft repository, products are deployed to Yandex Cloud with data in serverless YDB, and generation uses an ensemble of Yandex's own models.
