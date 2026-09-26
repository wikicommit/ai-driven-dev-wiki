---
title: "Agent Payments Protocol（AP2）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["AP2"]
tags: [エージェント, エージェントプロトコル, エージェンティックコマース, ガードレール]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-payments-protocol.md"
source_commit: "83a69e2424e621789facae2288c4aa54d75ba9ed"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントが行う購入を承認するためのプロトコル。否認できない意図の証明を与え、承認済みの販売者や支出上限といった設定可能なガードレールを強制する型付きのマンデートを用い、意図から署名済みマンデートを経て領収書に至る監査証跡を生成する。"
---

Agent Payments Protocol（AP2）は、AI エージェントがユーザーに代わって行う支払いを承認するためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] はこれを、否認できない意図の証明を与え、すべての取引に設定可能なガードレールを強制する型付きのマンデートを追加するものと説明している。これにより、エージェントの購入には、どのような上限が設定されたか、どの販売者が承認されていたか、承認がいつ失効するか、そして誰が各支払いを承認したかの記録が伴うことになる。

## 用法

このガイドが AP2 を持ち出すのは、エージェントがすでに注文を出せるようになり、残る問いが「誰がその支出を承認したのか」になった段階である。その流れには 3 つの型付きオブジェクトがある。所有者が設定する `IntentMandate` は、許可された販売者、返金可能かどうかといった条件、カートの確認を必要とするかどうか、自動承認の支出上限、そして有効期限を指定する。次にエージェントは、特定のカートと金額に結び付いた `PaymentMandate` を生成する。注文が上限を超える場合、そのマンデートはマネージャーが明示的に承認するまで未署名のままとなる。`PaymentReceipt` が監査証跡を締めくくる。ガイドはこの連鎖を、何が意図され、承認され、支払われたかを記録するものとまとめている。

AP2 は [[DefinedTerm/universal-commerce-protocol]] と組み合わせて機能するよう設計されている。ガイドの言葉では、UCP は何を誰から注文するかを扱い、AP2 は誰がその購入を承認したかを扱って監査証跡を提供する。AP2 は UCP の拡張として組み込まれ、チェックアウトの流れに承認の暗号学的な証明を加える。ガイドの例ではマネージャーの署名をシミュレートしており、実際の AP2 ではセキュアなデバイス上での JWT または生体認証による署名を用いると注記している。

その投稿の時点で AP2 は v0.1 であり、その型は [[SoftwareApplication/agent-development-kit]] のコアに組み込まれるのではなく、別パッケージとして提供されていた。

## 関連用語

- [[DefinedTerm/universal-commerce-protocol]] — AP2 が拡張するコマースプロトコル
- [[DefinedTerm/guardrails]] — AP2 のマンデートは、プロトコルレベルでの支出のガードレールの一形態である
- [[DefinedTerm/human-in-the-loop]] — 設定された上限を超える注文は、人間による明示的な承認を待つ
