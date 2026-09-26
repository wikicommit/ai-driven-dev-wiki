---
title: "Universal Commerce Protocol（UCP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["UCP"]
tags: [エージェント, エージェントプロトコル, エージェンティックコマース]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/universal-commerce-protocol.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントのための購買ライフサイクルを、強く型付けされたリクエストとレスポンスのスキーマを持つモジュール式のケイパビリティとして標準化するプロトコル。スキーマは REST、MCP、A2A、ブラウザ組み込み型のプロトコルの間で一貫しており、エージェントは一つのパターンで異なるマーチャントに注文できる。"
---

Universal Commerce Protocol（UCP）は、マーチャントごとに個別の連携を用意するのではなく、一つのパターンで AI エージェントに買い物をさせるためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] の説明によれば、UCP は購買ライフサイクルをモジュール式のケイパビリティとして標準化しており、それらは強く型付けされたリクエストとレスポンスのスキーマとして表現され、下位のトランスポートが REST、[[DefinedTerm/model-context-protocol]]、[[DefinedTerm/agent2agent-protocol]]、あるいはブラウザベースのフロー向けの Embedded Protocols（EP）のいずれであっても一貫している。

## 用法

このガイドの捉え方では、UCP が扱う問題は、サプライヤーごとにチェックアウト API が異なるため、5 つの卸売業者から仕入れるエージェントは本来 5 種類のチェックアウト連携を必要とする、という点にある。UCP を使うと、エージェントはよく知られた URL（`/.well-known/ucp`）で公開されているプロファイルからマーチャントのケイパビリティを発見する。これは A2A が Agent Card に用いているのと同じ発見パターンである。そのうえで、明細行と支払い情報を含む型付きのチェックアウトリクエストを組み立て、チェックアウトセッションを作成し、それを完了させる。ガイドの例では、各リクエストに識別用のヘッダーを付けて送っており、その中には呼び出し元エージェントのケイパビリティプロファイルを指すヘッダーや、操作ごとに新しく発行される冪等性キーが含まれる。

UCP は標準的な REST API もサポートしているため、プロジェクトが既に使っている HTTP クライアントであれば何でも動作し、独自の SDK は必要ないとガイドは述べている。また、UCP と A2A を組み合わせてエンドツーエンドの購買ワークフローを実現するサンプルのショッピングアシスタントも紹介している。

UCP が扱うのは、何を誰から注文するかである。購入の承認、つまり誰がそれを承認し、どの範囲内で承認したのかは [[DefinedTerm/agent-payments-protocol]] の役割であり、ガイドはこれを UCP に拡張として組み込まれるものとして説明している。

## 関連用語

- [[DefinedTerm/agent-payments-protocol]] — UCP のチェックアウトフローに支払いの承認と監査証跡を追加する
- [[DefinedTerm/agent2agent-protocol]] — UCP が再利用している、よく知られた URL による発見パターンの出どころ
- [[DefinedTerm/model-context-protocol]] — UCP が利用できるトランスポートの一つ
