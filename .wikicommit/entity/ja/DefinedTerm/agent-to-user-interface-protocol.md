---
title: "Agent-to-User Interface Protocol（A2UI）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["A2UI"]
tags: [エージェント, エージェントプロトコル, 生成 UI]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-to-user-interface-protocol.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントが、安全なコンポーネントプリミティブの固定カタログから宣言的な JSON 形式でユーザーインターフェースを組み立てられるようにするプロトコル。コンポーネント構造とデータを別々に送り、クライアント側のレンダラーがそれをネイティブ UI に変換する。"
---

Agent-to-User Interface Protocol（A2UI）は、AI エージェントがその結果をプレーンテキストとしてではなくインターフェースとして
提示できるようにするためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] の説明によれば、
エージェントは固定されたカタログから新しいレイアウトを動的に組み立てる。その際に用いるのは、行、列、テキストフィールドなど
18 種類の安全なコンポーネントプリミティブからなる宣言的な JSON 形式であり、クライアント側のレンダラーが Lit、Flutter、
Angular といったフレームワークを使ってその JSON をネイティブ UI に変換する。

## 用法

同ガイドが動機づけとして挙げるのは、在庫ダッシュボード、注文フォーム、仕入先の比較を表示する必要のあるエージェントであり、
これらはいずれも本来ならそれぞれ専用に手作りしたフロントエンドコンポーネントを必要とする。A2UI は UI の構造とデータを
分離する。エージェントはまずレンダリング用のサーフェスを作成し、次にコンポーネントツリーを、入れ子にするのではなく ID で
互いを参照し合うコンポーネントのフラットなリストとして送り、その後に別個のデータペイロードを送る。コンポーネントは
そのペイロード内の値にパスで束縛されるため、コンポーネントを再送せずにデータだけを更新できる。同ガイドの例では、同じ
エージェントに 3 つのプロンプトを与えると、同じプリミティブから在庫チェックリスト、注文フォーム、仕入先の比較が
生成され、追加のフロントエンドコードは一切必要ない。

開発中は、[[SoftwareApplication/agent-development-kit]] の Web インターフェース（`adk web`）が A2UI コンポーネントを
ネイティブにレンダリングできるため、独自のレンダラーを書かずにエージェントの UI 出力をテストできる。

同ガイドは A2UI を [[DefinedTerm/agent-user-interaction-protocol]] と区別している。A2UI は何をレンダリングするかを定義し、
AG-UI はエージェントのイベントをどのようにフロントエンドへストリーミングするかを定義する。

## 関連用語

- [[DefinedTerm/agent-user-interaction-protocol]] — 同ガイドが A2UI と組み合わせるストリーミング層
- [[DefinedTerm/model-context-protocol]] と [[DefinedTerm/agent2agent-protocol]] — 同ガイドが同じエージェントの
  ツール側とエージェント側に位置づけるプロトコル
