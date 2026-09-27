---
title: "Agent-to-User Interface Protocol（A2UI）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["A2UI"]
tags: [エージェント, エージェントプロトコル, 生成 UI]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-to-user-interface-protocol.md"
source_commit: "20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントが、安全なコンポーネントプリミティブからなる固定のカタログを使い、宣言的な JSON 形式でユーザーインターフェースを組み立てられるようにするプロトコル。コンポーネントの構造とデータは別々に送られ、クライアント側のレンダラーがそれをネイティブ UI に変換する。"
---

Agent-to-User Interface Protocol（A2UI）は、AI エージェントが結果を単なるテキストではなくインターフェースとして提示できるようにするためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] の説明によれば、エージェントは、行、列、テキストフィールドなど 18 種類の安全なコンポーネントプリミティブからなる宣言的な JSON 形式を用い、固定のカタログから新しいレイアウトを動的に組み立てる。そしてクライアント側のレンダラーが、Lit、Flutter、Angular などのフレームワークを使ってその JSON をネイティブ UI に変換する。

## 用法

このガイドが動機として挙げる事例は、在庫ダッシュボード、注文フォーム、サプライヤー比較を表示する必要のあるエージェントである。本来であれば、それぞれに専用のフロントエンドコンポーネントを手作りしなければならない。A2UI は UI の構造とデータを分離する。エージェントはまずレンダリング用のサーフェスを作成し、次にコンポーネントツリーを、入れ子にするのではなく ID で互いを参照するコンポーネントのフラットなリストとして送り、その後に別途データのペイロードを送る。コンポーネントはパスによってそのペイロード内の値にバインドされるため、コンポーネントを送り直すことなくデータを更新できる。ガイドの例では、同じエージェントに対する 3 つのプロンプトが、同じプリミティブから在庫チェックリスト、注文フォーム、サプライヤー比較を生成しており、追加のフロントエンドコードは一切必要ない。

開発中は、[[SoftwareApplication/agent-development-kit]] の Web インターフェース（`adk web`）が A2UI コンポーネントをネイティブにレンダリングできるため、独自のレンダラーを書かずにエージェントの UI 出力をテストできる。

ガイドは A2UI を [[DefinedTerm/agent-user-interaction-protocol]] と区別している。A2UI は何をレンダリングするかを定義し、AG-UI はエージェントのイベントをどのようにフロントエンドへストリーミングするかを定義する。

## 関連用語

- [[DefinedTerm/agent-user-interaction-protocol]] — ガイドが A2UI と組み合わせるストリーミングの層
- [[DefinedTerm/model-context-protocol]] と [[DefinedTerm/agent2agent-protocol]] — ガイドが同じエージェントのツール側とエージェント側に位置づけるプロトコル
