---
title: "カスタムスラッシュコマンド"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント設定, 仕様駆動開発, プロンプトエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/custom-slash-commands.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "よく使うプロンプトをコマンドとして保存し、プロジェクト単位で永続化・共有する AI エージェントツールの機能。仕様駆動開発において、AI への指示を共有資産にする方法として示されている。"
---

カスタムスラッシュコマンドとは、よく使うプロンプトを名前付きのコマンドとして保存し、プロジェクトのレベルで永続化・共有するための AI エージェントツールの機能である。[[DefinedTerm/spec-driven-development]] の文脈で、[[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] はこれを、AI への指示を資産化し、開発プロセスそのものを関数の集まりにするための仕組みとして説明している。

## 用法

この記事は、仕様駆動開発でこれを使う理由を 3 つ挙げている。第一に、プロンプトエンジニアリングを標準化する。チームのベストプラクティスを組み込んだコマンドは、出力の品質が開発者一人ひとりのプロンプトの腕前に左右されるのではなく、誰が実行しても同じ形式と品質を生み出す。第二に、コンテキストの注入を自動化する。コマンドは読み込むべき仕様ファイルを指定できるため、毎回手作業で選んで貼り付けなくても、適切な仕様がエージェントのコンテキストに届く。第三に、プロンプトをリポジトリ内のコードとしてバージョン管理下に置く（「Prompt as Code」）。そこでは、チームがプロンプトをレビューし、時間をかけて改善していける。

同じ記事は、コマンドの設計を [[DefinedTerm/context-engineering]] の主要なレバーとして扱い、そのための実践を提案している。各コマンドには単一の責務と単一の出力ファイルを持たせる、読み込むコンテキストは必要最小限にとどめる、コマンドを書く前に出力の構造とテンプレートを定義する、人間が書いたゴールデン出力に照らしてコマンドをテストする、コマンドのロジックはツール固有のディレクトリの外に置く、そして指示が長くなったり分岐したりするのはコマンドを分割すべき兆候として扱う、というものである。これらは一般的な慣行ではなく、あるテックリードが概念実証から得た知見である。

## 関連用語

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/context-confusion]]
- [[DefinedTerm/context-poisoning]]
