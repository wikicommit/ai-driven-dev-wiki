---
title: "Agent Payments Protocol（AP2）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["AP2"]
tags: [エージェント, エージェントプロトコル, エージェンティックコマース, ガードレール]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-payments-protocol.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントによる購入を承認するためのプロトコル。否認不可能な意図の証明を与え、承認済みマーチャントや支出上限といった設定可能なガードレールを強制する型付きのマンデートを用い、意図から署名済みマンデートを経て領収書に至る監査証跡を生成する。"
---

Agent Payments Protocol（AP2）は、AI エージェントがユーザーに代わって行う支払いを承認するためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] はこれを、否認不可能な意図の証明を与え、あらゆる取引に設定可能なガードレールを強制する型付きのマンデートを追加するものと説明している。これにより、エージェントによる購入には、どのような上限が設定されていたか、どのマーチャントが承認されていたか、承認がいつ失効するか、そして各支払いを誰が承認したかの記録が伴う。

## 用法

このガイドが AP2 を持ち出すのは、エージェントがすでに注文を出せるようになり、残る問いが「その支出を誰が承認したのか」になった時点である。そのフローには 3 つの型付きオブジェクトがある。オーナーが設定する `IntentMandate` は、許可するマーチャント、返金可能かどうかといった条件、カートの確認を必須とするかどうか、自動承認の支出上限、そして有効期限を指定する。次にエージェントが、特定のカートと金額に結びついた `PaymentMandate` を生成する。注文が上限を超える場合、マネージャーが明示的に承認するまでそのマンデートは署名されないままとなる。`PaymentReceipt` が監査証跡を締めくくる。ガイドはこの連鎖を、何が意図され、何が承認され、何が支払われたかを記録するものと要約している。

AP2 は [[DefinedTerm/universal-commerce-protocol]] と連携するよう設計されている。ガイドの言葉では、UCP は何を誰から注文するかを扱い、AP2 は誰が購入を承認したかを扱って監査証跡を提供する。AP2 は UCP の拡張として組み込まれ、チェックアウトフローに承認の暗号学的な証明を追加する。ガイドの例ではマネージャーの署名をシミュレートしており、実際の AP2 ではセキュアなデバイス上での JWT または生体認証による署名を用いると注記している。

その投稿の時点で AP2 は v0.1 であり、その型は [[SoftwareApplication/agent-development-kit]] のコアに組み込まれるのではなく、別パッケージとして提供されていた。

## 関連用語

- [[DefinedTerm/universal-commerce-protocol]] — AP2 が拡張するコマースプロトコル
- [[DefinedTerm/guardrails]] — AP2 のマンデートは、支出に関するガードレールをプロトコルのレベルで実現したものである
- [[DefinedTerm/human-in-the-loop]] — 設定された上限を超える注文は、人間による明示的な承認を待つ
