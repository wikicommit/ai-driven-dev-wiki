---
title: "Sandbox Runtime"
type: "schema:SoftwareApplication"
lang: ja
tags: [サンドボックス化, セキュリティ]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/sandbox-runtime.md"
source_commit: "02f7d23719e4ec300fc997d58e966c19037dfd22"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "リサーチプレビューとして公開された Anthropic のオープンソースのサンドボックスランタイム。OS レベルのプリミティブを使って、プロセスがアクセスできるディレクトリとネットワークホストを制限する。Claude Code は bash ツールのサンドボックス化にこれを使っている。"
  applicationCategory: "サンドボックスランタイム"
  operatingSystem: "Linux, macOS"
  author: "[[Organization/anthropic]]"
---

Sandbox Runtime は、[[Organization/anthropic]] が [[BlogPosting/beyond-permission-prompts]] で紹介した、エージェントやその他のプロセスのためのサンドボックスである。コンテナを起動・管理するオーバーヘッドなしに、エージェントがアクセスできるディレクトリとネットワークホストをユーザーが厳密に定義できる。ベータ版としてリサーチプレビューの形で公開されており、オープンソースのリサーチプレビューとしても入手できる。

[[SoftwareApplication/claude-code]] は bash ツールのサンドボックス化にこれを使っており、Claude はユーザーが設定した制限の範囲内で、パーミッションプロンプトなしにコマンドを実行できる。このランタイムは、任意のプロセス、エージェント、MCP サーバーのサンドボックス化にも使うことができる。

## 機能

このランタイムは、Linux の bubblewrap と macOS の seatbelt を基盤として、オペレーティングシステムのレベルで制限を強制する。制限は、ランタイムが起動するプロセスだけでなく、そのプロセスが生成するあらゆるスクリプト、プログラム、サブプロセスにも適用される。Claude Code の bash ツール向けに設定された状態では、2 つの境界を強制する。

- **ファイルシステムの分離** — 現在の作業ディレクトリへの読み取りと書き込みのアクセスを許可し、その外側にあるファイルの変更はすべてブロックする。
- **ネットワークの分離** — インターネットへのアクセスを、サンドボックスの外部で動作するプロキシサーバーに接続された Unix ドメインソケット経由に限定する。プロキシは、プロセスが接続できるドメインを制限し、新たに要求されたドメインについてはユーザーの確認を処理する。また、送信トラフィックに任意のルールを強制するようカスタマイズすることもできる。

どちらの境界も設定可能であり、特定のファイルパスやドメインを許可または禁止できる。サンドボックス化されたコマンドがサンドボックス外のものにアクセスしようとすると、ユーザーには即座に通知され、それを許可するかどうかを選択できる。Claude Code では `/sandbox` コマンドで起動する。

## 採用とエコシステム

Anthropic は、社内での利用において、このように Claude Code をサンドボックス化したことでパーミッションプロンプトが 84% 減少したと報告している。Anthropic は他のチームがより安全なエージェントを構築できるようにこのランタイムをオープンソース化し、他の開発者にも自らのエージェントへの採用を検討するよう勧めている。このランタイムは、この wiki の他のページで論じられている OS レベルの形態の [[DefinedTerm/sandboxing]] を支える具体的な実装である。
