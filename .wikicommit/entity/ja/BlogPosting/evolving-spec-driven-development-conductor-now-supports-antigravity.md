---
title: "仕様駆動開発の進化：Conductor が Antigravity に対応"
type: "schema:BlogPosting"
lang: ja
tags: [仕様駆動開発, コーディングツール, エージェントツーリング]
review_status: pending
translated_from: ".wikicommit/entity/en/BlogPosting/evolving-spec-driven-development-conductor-now-supports-antigravity.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "ターミナル向けの仕様駆動開発ツールである Conductor が、Gemini CLI 拡張機能ではなくプラグインになるという Google の発表。これにより Conductor は対話的に操作でき、Antigravity CLI など他のエージェントツールからも使えるようになる。"
  author: ["Mahima Shanware", "Sherzat Aitbayev", "Jay Kornder"]
  datePublished: "2026-07-16"
  publisher: "[[Organization/google]]"
---

この記事は、[[SoftwareApplication/conductor-gemini-cli-extension]] の次の段階を発表するものである。Conductor は、プロジェクトの把握を一時的なチャットログから、永続的でバージョン管理された Markdown ファイルへと移すことで、[[DefinedTerm/spec-driven-development]] をターミナルにもたらすために Google が前年に導入したものである。Conductor は Gemini CLI 拡張機能から Conductor Plugin へと変わる。記事の説明によれば、プラグインとはスキル、ルール、MCP サーバー、フックをまとめて含めることのできるパッケージである。

記事によれば、ここから 2 つの変化が生じる。Conductor は厳密なコマンドの順序を要求しなくなり、対話的に動作して、開発者が機能について議論するのに合わせてコンテキスト、仕様、計画を生成する。また Gemini CLI に縛られなくなるため、[[SoftwareApplication/antigravity-cli]] や他のツールから使えるようになる。記事はこの両方を、仕様駆動開発の手続き的な厳密さを保ちながら、そこから摩擦を取り除くものとして提示している。

## 要点

- 永続的な Markdown の成果物は残る。`spec.md` と `plan.md` は引き続き生成されるが、それらの作成と反復はアシスタントとチャットしているように感じられることが意図されている。
- Conductor は、プロジェクトのコンテキストをいつ更新するか、計画の中の完了したタスクにいつチェックを付けるかを自ら判断し、開発者がアーキテクチャに集中している間、バックグラウンドでプロジェクトの状態を管理するものとして説明されている。
- プラグインとしての Conductor は、ツールをまたいで持ち運べるものとして提示されている。プロジェクトのアーキテクチャ、ガイドライン、目標に関する基礎文書が、共有の設定や進行中の開発トラックとともに永続化されるため、あるツールで始めた作業を別のツールで続けることができる。
- 旧来の Conductor のコマンド、および既存の計画と仕様との後方互換性があるとされている。
- 記事は、このプラグインを使えるツールとして Antigravity CLI と Claude を挙げている。
- Google は、[[Dataset/terminal-bench]] のタスクのうち最も複雑なサブセットにおいて、Conductor Plugin が仕様駆動開発を用いないユーザーよりも高い成功率を達成したと主張している。記事はこの比較について、数値もタスク数も手法も示していない。
- インストールはプラグインの GitHub リポジトリから行うか、`agy plugins install https://github.com/gemini-cli-extensions/conductor` で Antigravity CLI に導入する。実践的な Codelab も提供されている。

## 背景

この記事は Google が自社ツールの変更を告知するものであり、その性能に関する主張は裏付けとなるデータなしに述べられている。記事は Conductor の使命を、AI による開発を「安全で、予測可能で、アーキテクチャ的に健全」なものにする手助けとして改めて示し、リポジトリをプロジェクトの唯一の信頼できる情報源として扱っている。プラグインが変えるのは、その情報源がどこにあるかではなく、開発者がそれとどう関わるかだとされる。
