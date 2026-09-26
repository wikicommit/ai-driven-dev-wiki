---
title: "ドゥームループ"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントの失敗モード, ハーネスエンジニアリング, エージェント型コーディング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/doom-loop.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コーディングエージェントの失敗モードの 1 つ。ある計画に取りかかったエージェントが、立ち止まってそれを考え直す代わりに、同じ壊れたアプローチに小さな変更を加え続ける。"
---

ドゥームループとは、コーディングエージェントがある計画に落ち着いた後、それを考え直すのではなく、同じ壊れたアプローチに
小さな変更を繰り返し加える失敗モードである。LangChain は [[BlogPosting/improving-deep-agents-with-harness-engineering]] で、
これをエージェントがいったん計画を決めると視野が狭くなることに帰しており、一部のトレースでは同じアプローチが 10 回以上
再試行されているのを見たと報告している。

## 用法

LangChain はこの用語を [[DefinedTerm/harness-engineering]] の文脈で用いており、その対応はモデルの変更ではなくハーネスの
仕組みである。LangChain の対策はループ検出のミドルウェア（[[DefinedTerm/agent-middleware]] を参照）で、ツール呼び出しの
フックを通じてファイルごとの編集回数を数え、同じファイルへの編集が一定回数に達すると、エージェントにアプローチを考え直すよう
促すコンテキストを追加する。チームは、これがエージェントの立て直しに役立つことはあるが、モデルが自分は正しいと信じていれば
依然として同じ道を進み続けることがあると報告している。LangChain はこのガードレールを、現在認識されているモデルの問題に
合わせて設計されたヒューリスティックであり、モデルが改善するにつれて不要になる可能性が高いものとして示している。より広い
教訓としては、ハーネスの設計者が短期的に検出して修正すべき悪いパターンの 1 つとして、やみくもな再試行を挙げている。

## 関連用語

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/agent-middleware]]
- [[DefinedTerm/verification-loop]]
