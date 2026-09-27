---
title: "Conductor（Gemini CLI 拡張機能）"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コードレビュー, コーディングツール, 仕様駆動開発]
translated_from: ".wikicommit/entity/en/SoftwareApplication/conductor-gemini-cli-extension.md"
source_commit: "9b65710f8033cfb0f6c3388db1436c4e823817a3"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Google が提供するターミナル向けの仕様駆動開発ツール。プロジェクトのコンテキストを一時的なチャットログではなく、永続的でバージョン管理された Markdown ファイルに保持する。Gemini CLI の拡張機能として始まり、2026 年 2 月に実装後の自動レビューを追加し、2026 年 7 月には Antigravity CLI など他のエージェントツールからも利用できるプラグインとなった。"
  applicationCategory: "コーディングエージェントの拡張機能およびプラグイン"
  featureList: "コンテキスト駆動の計画、対話を通じたコンテキスト・仕様・計画の生成、コード品質・計画への準拠・ガイドラインの遵守・テストスイートの検証・基本的なセキュリティスキャンを対象とする実装後の自動レビュー、プラグインとしての複数エージェントツール間での可搬性"
  author: "[[Organization/google]]"
---

Conductor は Gemini CLI の拡張機能であり、2026 年 2 月のアップデートに先立つ前年 12 月に Google が発表した。その掲げる目的は、コンテキスト駆動の開発をターミナルにもたらすことである。中心的な設計上の選択は、プロジェクトに関する認識をどこに置くかにある。それを一時的なチャットログに蓄積させるのではなく、永続的でバージョン管理された Markdown ファイルへと移す。ソースが名前を挙げているのは `plan.md` と `spec.md` の 2 つである。Google は、これによって開発者が構築の前に計画を立てられるようになるとしている。

2026 年 2 月に発表された Automated Review 機能により、この拡張機能は計画と実行に加えて検証までを担うようになった。コーディングエージェントがタスクを完了すると、Conductor はコード品質と、開発者が定義したガイドラインへの準拠状況についての実装後レポートを生成できる。

2026 年 7 月、Google は Conductor が Gemini CLI の拡張機能から Conductor Plugin へと進化すると発表した。Conductor Plugin は、スキル、ルール、MCP サーバー、フックをまとめて同梱できるパッケージである（[[BlogPosting/evolving-spec-driven-development-conductor-now-supports-antigravity]]）。これによる帰結として挙げられているのは、厳密なコマンドの順序に従うのではなく対話的に操作できるようになったこと、そして Gemini CLI に縛られなくなったことである。

拡張機能は GitHub リポジトリから、直接または `gemini extensions install https://github.com/gemini-cli-extensions/conductor` によってインストールする。プラグインは `agy plugins install https://github.com/gemini-cli-extensions/conductor` によって Antigravity CLI にインストールする。

## 機能

計画の面では、プロジェクトのコンテキストはバージョン管理された Markdown ファイルに保持され、ワークフローはそれに基づいて進む。プラグインとしての Conductor は、開発者と対話的にやりとりし、機能について話し合う過程でコンテキスト、仕様、計画を生成しつつ、永続的な成果物として `spec.md` と `plan.md` を引き続き生成すると説明されている。Google によれば、プロジェクトのコンテキストをいつ更新するか、計画内の完了したタスクにいつチェックを付けるかは Conductor 自身が判断する。プラグインは、従来の Conductor のコマンドや既存の計画・仕様と後方互換性があるとされている。

Automated Review の面はより詳しく説明されており、1 つの実装後レポートを構成する 5 つのチェックからなる。

- **コードレビュー** — 新たに生成されたファイルに対する静的解析とロジック解析を深く行う。構文の枠を超えて、非同期ブロックにおける競合状態、潜在的なヌルポインタのリスク、実行時例外につながりうるロジックエラーといった複雑な問題を指摘する。
- **計画への準拠** — 新しいコードを `plan.md` と `spec.md` に照らしてチェックし、ロードマップのすべてのフェーズに対応していること、コーディング中に中核的な要件が抜け落ちていないことを確認する。
- **ガイドラインの遵守** — 新たな変更がプロジェクトのスタイルガイドと、計画フェーズで生成されたカスタムガイドラインファイルに従っていることを検証する。
- **テストスイートの検証** — 手動での実行に頼るのではなく、レビューワークフローの一部として関連する単体テストと統合テストを実行し、その結果とカバレッジデータをレポートに組み込む。
- **基本的なセキュリティレビュー** — コードがマージされる前に重大な脆弱性をスキャンし、ハードコードされた API キー、個人を特定できる情報の潜在的な漏洩、アプリケーションをインジェクション攻撃にさらしうる安全でない入力処理といった高リスクの問題を指摘する。

指摘事項は High、Medium、Low の 3 段階で評価され、正確なファイルパスが付記される。また、それらに対処するためのトラックを Conductor 内で開始できる。これらの挙動のいずれについてもバージョン番号は示されておらず、機能の内容は計測結果ではなく Google 自身による説明である。

## 採用とエコシステム

Conductor は独立したツールとしてではなく [[SoftwareApplication/gemini-cli]] の拡張機能として始まったため、このアシスタントのターミナルベースの作業スタイルを受け継いでいる。プラグインとしては、タスクに適したどのツールからでも利用できるものとして紹介されており、Google が例として挙げているのは [[SoftwareApplication/antigravity-cli]] と Claude である。プロジェクトの基礎となるドキュメント、共有された設定、進行中の開発トラックが永続化されるため、あるツールで始めた作業を別のツールで続けることができる。`plan.md` / `spec.md` という慣習は、より広い [[DefinedTerm/spec-driven-development]] の実践の中に位置づけられる。また、Conductor が追加するレビューステップは、レビュアー自身の判断だけに頼るのではなく、それらと同じ仕様ファイルに照らして実行される [[DefinedTerm/agentic-code-review]] の一例である。

Google はこの仕組みを、エージェント型開発を監督下に置き続けるためのものと位置づけている。AI が労働を担い、開発者は自動検証に支えられながら高レベルのアーキテクチャ上の監督を担う、というものである。この発表は [[BlogPosting/conductor-update-introducing-automated-reviews]] で報じられている。
