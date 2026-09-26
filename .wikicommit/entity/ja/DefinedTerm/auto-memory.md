---
title: "Auto Memory"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントメモリ, コンテキストエンジニアリング, Anthropic]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/auto-memory.md"
source_commit: "10e9746c9bd7c8cfc2db7e41ba9601f191b8bb0f"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Claude Code の仕組みの一つで、Claude が自分自身のためのメモ——ユーザーについて、訂正や確認済みのやり方、進行中のプロジェクト上の決定、外部の情報の在りか——をリポジトリごとのメモリディレクトリに書き込み、その MEMORY.md 索引が毎セッションの開始時に読み込まれる。"
---

Auto Memory（自動メモリ）は、ユーザーが何も書かなくても Claude がセッションをまたいで知識を蓄積できるように
[[SoftwareApplication/claude-code]] が備える仕組みである。Claude は作業しながら、ユーザーの訂正や好みに基づいて自分の
ためのメモをプロジェクトのメモリディレクトリに保存し、それらのメモの索引が毎回の会話の開始時に読み込まれる。
Anthropic のドキュメントはこれを、[[DefinedTerm/claude-md]] と並ぶ 2 つの相補的なメモリシステムの一つとして提示して
いる。CLAUDE.md ファイルはユーザーが書き、指示やルールを保持する。一方 Auto Memory は Claude が書き、学びやパターンを
保持する。どちらも強制される設定ではなく、コンテキストとして扱われる。

## 用法

ドキュメントは 4 種類のメモを挙げており、それぞれのメモリファイルのフロントマターに `type` フィールドとして記録される。
`user`（ユーザーの役割、専門性、作業上の好み）、`feedback`（ユーザーが与える訂正と、ユーザーが確認したやり方）、
`project`（コードや git の履歴からは導けない進行中の作業、締め切り、決定）、`reference`（イシュートラッカーや
ダッシュボードなど、プロジェクト外の情報の在りか）である。Claude は、アーキテクチャ、ファイルパス、デバッグでの修正
など、コードベースから導けるものや、CLAUDE.md ファイルにすでに書かれているものは記録しない。また毎セッション何かを
保存するわけではなく、その情報が将来の会話で役立つかどうかで判断する。

各プロジェクトには `~/.claude/projects/<project>/memory/` に専用のディレクトリが割り当てられる。`<project>` のパスは
git リポジトリから導かれるため、1 つのリポジトリのすべてのワークツリーとサブディレクトリが単一のメモリディレクトリを
共有する。このディレクトリは `autoMemoryDirectory` 設定で別の場所に移すことができる。ディレクトリには、1 メモリにつき
1 行の `MEMORY.md` 索引と、メモリごとに 1 つのトピックファイルが置かれる。セッション開始時に読み込まれるのは
`MEMORY.md` の先頭 200 行または 25KB のいずれか先に達したほうまでであり、どちらかの上限に近づくと Claude Code は
Claude に索引を短くするよう促す。上限を超えた内容は次回の読み込みで切り捨てられるからである。トピックファイルは起動時
には読み込まれず、Claude の通常のファイル操作ツールで必要に応じて読まれる。Auto Memory はマシンローカルであり——
複数のマシンやクラウド環境の間では共有されない——、そのファイルは古いセッションのトランスクリプトを削除する保持期間の
一掃処理の対象から外されている。既定で有効であり、`/memory` コマンドや `autoMemoryEnabled` 設定で切り替えられ、環境
変数で無効化することもできる。ファイルはユーザーが読み、編集し、削除できるプレーンな Markdown である。

同じ仕組みは、Claude Code が実装する [[DefinedTerm/sub-agent-architecture]] にも及ぶ。メインの会話の Auto Memory は
サブエージェントには読み込まれない（親の会話を引き継ぐフォークは例外である）が、サブエージェントには `memory`
フィールドを通じて独自の永続的なメモリを持たせることができ、それは別のディレクトリに保管される。ユーザーが、特定の
パッケージマネージャーを常に使うといったことを覚えておくよう Claude に頼むと、Claude はそれを Auto Memory に保存すると
ドキュメントは述べている。代わりに CLAUDE.md に追加させるには、明示的にそう頼むか、ファイルを編集する必要がある。

## 関連用語

- [[DefinedTerm/claude-md]] —— 対をなす、ユーザーが書く側の仕組み
- [[DefinedTerm/memory-bank]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
