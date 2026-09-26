---
title: "Agent Payments Protocol（AP2）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["AP2"]
tags: [エージェント, エージェントプロトコル, エージェンティックコマース, ガードレール]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-payments-protocol.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントによる購入を承認するためのプロトコル。型付きのマンデート（mandate）を用いて、否認できない意図の証明を提供するとともに、承認済みの加盟店や支出上限といった設定可能なガードレールを強制し、意図から署名済みマンデートを経て領収書に至るまでの監査証跡を生成する。"
---

Agent Payments Protocol（AP2）は、AI エージェントがユーザーに代わって行う支払いを承認するためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] は、AP2 が型付きのマンデート（mandate）を加えるものだと説明している。このマンデートは否認できない意図の証明を提供し、すべての取引に設定可能なガードレールを強制する。これにより、エージェントの購入には、どのような上限が設定されていたか、どの加盟店が承認されていたか、承認がいつ失効するか、そして各支払いを誰が承認したかの記録が伴うことになる。

## 用法

このガイドが AP2 を持ち出すのは、エージェントがすでに注文を出す能力を得ており、残る問いが「その支出を誰が承認したのか」になった時点である。そのフローには 3 つの型付きオブジェクトがある。所有者が設定する `IntentMandate` は、許可された加盟店、返金可能性などの条件、カートの確認が必要かどうか、自動承認の支出上限、そして有効期限を指定する。次にエージェントが、特定のカートと金額に紐づいた `PaymentMandate` を生成する。注文が上限を超える場合、マネージャーが明示的に承認するまでそのマンデートは署名されないままとなる。最後に `PaymentReceipt` が監査証跡を締めくくる。ガイドはこの連鎖を、何が意図され、何が承認され、何が支払われたかを記録するものとまとめている。

AP2 は [[DefinedTerm/universal-commerce-protocol]] と組み合わせて動作するよう設計されている。ガイドの言葉によれば、UCP は何をどこから注文するかを扱い、AP2 は誰が購入を承認したかを扱って監査証跡を提供する。AP2 は UCP に拡張として組み込まれ、チェックアウトフローに承認の暗号学的証明を加える。ガイドの例ではマネージャーの署名をシミュレートしており、実際の AP2 ではセキュアなデバイス上での JWT または生体認証による署名を用いると注記している。

この投稿の時点で AP2 は v0.1 であり、その型は [[SoftwareApplication/agent-development-kit]] のコアに組み込まれるのではなく、別パッケージとして提供されていた。

## 関連用語

- [[DefinedTerm/universal-commerce-protocol]] — AP2 が拡張するコマースプロトコル
- [[DefinedTerm/guardrails]] — AP2 のマンデートは、支出に関するガードレールをプロトコルレベルで実現したものである
- [[DefinedTerm/human-in-the-loop]] — 設定された上限を超える注文は、人間による明示的な承認を待つ
