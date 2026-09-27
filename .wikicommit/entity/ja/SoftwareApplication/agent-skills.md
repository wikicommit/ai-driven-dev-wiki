---
title: "Agent Skills"
type: "schema:SoftwareApplication"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/SoftwareApplication/agent-skills.md"
source_commit: "908ab492691e9fcd622bfa73c6c2fd839716bea1"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "AI コーディングエージェント向けの、Markdown ベースの 20 個のスキルと 7 つのスラッシュコマンドからなる MIT ライセンスのオープンソースライブラリ。6 つの SDLC フェーズを軸に構成され、エージェントが普段は省略してしまうシニアエンジニアの実践（仕様、テスト、レビュー、スコープの規律）を強制することを目的としている。"
  applicationCategory: "AI コーディングエージェント向けスキルライブラリ"
  featureList: "/spec、/plan、/build、/test、/review、/ship、/code-simplify のスラッシュコマンド、反合理化テーブルと段階的開示を備えた 20 個の Markdown スキル"
  author: "Addy Osmani"
---

Agent Skills は、AI コーディングエージェント向けの、Markdown ベースの 20 個のスキルからなる MIT ライセンスのオープンソースライブラリで、作者によって GitHub で公開されており、スター数が 27,000 を超えたと報じられている。各スキルはリファレンスドキュメントではなく、チェックポイントと明確な終了基準を持つワークフローファイルである。その目的は、放っておけば完成したように見える差分への最短経路をたどってしまうエージェントに、シニアエンジニアの規律（仕様を書く、テストを先に書く、レビューしやすい大きさに変更を収める）を後から組み込むことにある。

## 機能

このライブラリは 20 個のスキルを、定義、計画、構築、検証、レビュー、出荷という 6 つの SDLC フェーズを軸に構成しており、それらは `/spec`、`/plan`、`/build`、`/test`、`/review`、`/ship`、`/code-simplify` の 7 つのスラッシュコマンドを通じて呼び出される。ルーターの役割を果たすスキル `using-agent-skills` が、20 個のスキルのうちどれを特定のタスクに適用するかを決めるため、小さなバグ修正では少数のスキルしか有効にならない一方で、複雑な機能では 11 個ほどのスキルが順番に有効になることもある。各スキルには、ワークフローを省略するためのよくある言い訳と、それに対して書かれた反論を対にした [[DefinedTerm/anti-rationalization-tables]] が組み込まれており、スキルは一度にすべて読み込まれるのではなく、段階的開示によって読み込まれる。

3 つの使い方が説明されている。Claude Code のプラグインとしてインストールする方法（`/plugin marketplace add addyosmani/agent-skills` の後に `/plugin install agent-skills@addy-agent-skills`）、プレーンな Markdown ファイルを他のツール独自のシステムプロンプトの仕組み（例: Cursor の `.cursor/rules/`、Gemini CLI、Codex、Aider、Windsurf、OpenCode）に置く方法、そして何もインストールせずに、スキルファイルそのものを実践の仕様として読む方法である。

## 採用状況とエコシステム

これらのスキルには、*Software Engineering at Google* や Google の公開されたエンジニアリング文化に由来する実践がふんだんに盛り込まれているとされる。たとえば、ハイラムの法則、テストピラミッドとビヨンセ・ルール、DRY より DAMP を優先するテスト、Critical/Nit/Optional/FYI の重大度ラベルを伴う 100 行程度のプルリクエストの規模、チェスタートンのフェンス、トランクベース開発、シフトレフトの CI/CD、そして非推奨化の判断においてコードを負債として扱うことなどである。このプロジェクトは、作者がより広く提唱する [[DefinedTerm/harness-engineering]] という枠組みの 1 つの層として位置づけられており、`AGENTS.md`、フック、ツールと並ぶものとされている。
