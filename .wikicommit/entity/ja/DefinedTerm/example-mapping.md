---
title: "Example Mapping"
type: "schema:DefinedTerm"
lang: ja
tags: [要件, 仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/example-mapping.md"
source_commit: "d5488c1df4d0cbce781137bbb410c0d112fd8758"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "振る舞い駆動開発で用いられるワークショップ形式で、ユーザーストーリーをめぐる会話を、ビジネスルール、例、反例、エッジケース、未解決の問いという構造化された振る舞いの知識に変える。"
---

Example Mapping は [[DefinedTerm/behavior-driven-development]] に結びついたワークショップ形式であり、
チームはユーザーストーリーを検討する際に、そのビジネスルールを、それを具体的に示す例・反例・エッジケース、
そしてなお未解決のまま残る問いとあわせて並べていく。これらはそれぞれ構造化された情報の一片となり、
期待される振る舞いについての曖昧さを段階的に減らしていく。

## 用法

[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]] は、AI エージェントの登場によって
このワークショップが新たな重要性を帯びると論じている。それはもはやチームの認識合わせに役立つだけでなく、
会話をエージェントが利用できる振る舞いの知識へと変えるものになる、というのである。この記事が描く流れでは、
Example Mapping の成果は Gherkin シナリオとして形式化され、それが [[DefinedTerm/spec-driven-development]] における
生きた仕様（リビングスペシフィケーション）へと供給される。同じ記事は、Example Mapping のセッションで挙がった
未解決の問いを、プロジェクトのコンテキストを保持するエージェントにリアルタイムで投げかけられるとも示唆している。
エージェントは既存のルールを呼び起こし、矛盾を検出し、影響を指摘し、調査の方向性を提案できる——ただし、
決定を下すのはあくまで参加者である。

## 適用される場面

- **条件。** ユーザーストーリーの振る舞いを、ビジネスの専門家とチームが同席したうえで、実装前に共同で
  明確化する必要がある場合に適用される。
- **前提。** ワークショップで得られたルールと例が、会話の中に置き去りにされるのではなく、その後に永続的な
  形——この記事の説明では Gherkin シナリオと仕様——へと引き継がれることを前提とする。
- **失敗モード。** この記事は、エージェントは明示されたものからしか推論しないと強調しており、ワークショップの
  成果から漏れたルール、例外、エッジケースは、エージェントの生成物における潜在的な誤りの源になる。
- **確立度。** この記事はこの実践について Cucumber のドキュメントにリンクしている。エージェント駆動の開発に
  おいてこのワークショップの重要性が増すという主張は、記事の著者が論じている立場である。

## 関連用語

- [[DefinedTerm/behavior-driven-development]]
- [[DefinedTerm/spec-driven-development]]
