---
title: "Kimi CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, CLI]
translated_from: ".wikicommit/entity/en/SoftwareApplication/kimi-cli.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Moonshot AI によるターミナル向けの Python 製 AI エージェント。コードの読み取りと編集、シェルコマンドの実行、Web ページの検索と取得によって、ソフトウェア開発タスクとターミナル操作を支援していた。リポジトリはアーカイブされ、ツールは Kimi Code CLI に置き換えられている。"
  applicationCategory: "ターミナル型コーディングエージェント"
  author: "Moonshot AI"
---

Kimi CLI は、ソフトウェア開発タスクとターミナル操作の遂行を支援するためにターミナル上で動作する AI エージェントであり、Moonshot AI が Apache License 2.0 の下で公開した。README によれば、コードの読み取りと編集、シェルコマンドの実行、Web ページの検索と取得を行え、実行中に自律的に行動を計画・調整できる。

リポジトリはアーカイブされ、読み取り専用になっている。README は、Python 製の Kimi CLI が、同じチームによる次世代のターミナル AI エージェントとされる Kimi Code CLI に置き換えられたこと、今後はリリース、バグ修正、セキュリティアップデートが行われないこと、既存のインストールはサポート対象外となり動作しなくなることを述べている。Kimi Code CLI は初回起動時に Kimi CLI のデータを検出し、その設定、MCP サーバー、入力履歴、セッションの移行を提案するが、ログイン認証情報、MCP の認可、Kimi CLI のプラグインは移行されない。同じリポジトリから公開されていた他のパッケージ、すなわち kosong、pykaos、kimi-sdk、そして新しいツールではなく kimi-cli のレガシーなエイリアスである kimi-code という名前の PyPI パッケージも、あわせてアーカイブされた。

## 機能

以下の機能は、アーカイブされたリポジトリが参照用に残している元の README に記述されたものである。

Kimi CLI は、コーディングエージェントであると同時にシェルでもあると自らを位置づけている。Ctrl-X を押すとシェルコマンドモードに切り替わり、ツールを離れずにシェルコマンドを直接実行できるが、`cd` のようなシェルの組み込みコマンドはまだサポートされていなかった。Zsh プラグインはその逆方向に働き、Zsh セッションから同じキーでエージェントモードに切り替えられる。このエージェントは Kimi Code VS Code 拡張機能を通じて Visual Studio Code と統合され、また Agent Client Protocol に標準で対応しているため、ACP 互換のエディタや IDE（README の例では Zed と JetBrains IDE）であれば、`kimi acp` でエージェントサーバーとして起動し、IDE のエージェントパネルで Kimi CLI のスレッドを実行できる。

[[DefinedTerm/model-context-protocol]] のツールにも対応している。`kimi mcp` サブコマンド群は、streamable HTTP（任意で OAuth による認可付き）または stdio 経由でサーバーを追加し、一覧表示、削除、認可を行える。あるいは、一般的な MCP 設定形式の設定ファイルを `--mcp-config-file` で渡して、1 回の実行に限ってサーバーに接続することもできる。
