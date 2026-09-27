---
title: "DeepSeek Harness"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントツーリング, エージェントアーキテクチャ, オープンソース]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/deepseek-harness.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "DeepSeek AI によるオープンソースのエージェントハーネス。`dsh` として起動し、Cordis フレームワークを基盤とする「すべてがプラグイン」のアーキテクチャで構築され、ローカルの Web UI を通じて動作する。開発者プレビューとして公開されている。"
  applicationCategory: "エージェントハーネス"
  author: "DeepSeek AI"
---

DeepSeek Harness は `dsh` として起動するオープンソースの[[DefinedTerm/agent-harness]]で、
DeepSeek AI が開発し、MIT ライセンスのもとで公開している。キャッチフレーズの「Everything is a Plugin」は
そのアーキテクチャを表しており、このハーネスは Cordis フレームワークを基盤とする「すべてがプラグイン」の設計で構築されている。

## 機能

ハーネスは `npx @deepseek-ai/dsh web` で起動し、ローカルマシン上で Web UI を立ち上げて
（デフォルトでは `127.0.0.1:3080`）ブラウザで開く。SSH 経由の場合は、転送されたローカルアドレスを
SSH クライアントやエディタが管理するため、代わりにホストのアドレスを表示する。リポジトリのチェックアウトから
ビルドして実行することもでき、プロジェクトの開発ツールは Web アプリケーションとデスクトップアプリケーションの両方をカバーしている。
このプロジェクトは急速に改良が続けられている開発者プレビューであることが明示されており、README は
互換性を損なう変更が行われることを大文字で警告し、実行前に安全上の注意事項を読むよう利用者に求めている。

## 採用とエコシステム

拡張はプラグインを通じて行われるため、プロジェクトはプラグイン作者に対し、プラグインを見つけやすくするために
リポジトリへ `dsh-plugin` という GitHub トピックを付けるよう求めている。README はまた、リポジトリで作業する
コーディングエージェントに対して、その `AGENTS.md`（[[DefinedTerm/agents-md]]）に従うよう指示している。
