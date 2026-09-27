---
title: "AgentScript"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントツーリング, 仕様駆動開発, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/agentscript.md"
source_commit: "4b83a0390f0437f8f63f9399a1db3e12e1ace784"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM に JavaScript に似たプランコードの断片を出力させる手法。出力は抽象構文木にパースされ、ランタイムによってステップごとに実行される。情報源によれば、これによってプランが明示的で、レビュー可能で、一時停止可能で、シリアライズ可能になる。"
  applicationCategory: "エージェントのプランニング"
  featureList: "JavaScript に似たプランコードとしての LLM 出力、抽象構文木へのパース、ランタイムによるステップごとの実行、明示的でレビュー可能・一時停止可能・シリアライズ可能なプラン"
---

AgentScript は、モデルのプランそのものがプログラムであるという、エージェントのプランニングの手法である。LLM に何をするつもりかを記述させてから行動させるのではなく、JavaScript に似た**プランコード**の断片を出力させる。その出力は抽象構文木にパースされ、ランタイムがそれをステップごとに実行する。

情報源が導き出している帰結は、この構成によって得られるものである。すなわち、プランが明示的で、レビュー可能で、一時停止可能で、シリアライズ可能になり、それによってエージェントの解釈可能性と制御可能性が高まるという。情報源はこれを、AI IDE、CLI ツールキット、研究フレームワークと並ぶ [[DefinedTerm/spec-driven-development]] の代表的な実装の 1 つに挙げ、仕様駆動のエージェントの*振る舞い*のための設計と呼んでいる。

## 機能

ここで扱っている唯一の情報源は、仕組みを概略としてしか説明していない。すなわち、LLM がプランコードを出力 → AST にパース → ランタイムがステップごとに実行、という流れである。言語の構文、ツールとの結び付けのモデル、一時停止したプランをどう再開するか、誰が公開しているかについては説明していない。

## 関連用語

- [[DefinedTerm/spec-driven-development]] — 情報源がこれをその実装の 1 つに挙げている実践
- [[DefinedTerm/checkpoint-and-resume]] — 関連する考え方。情報源はここでのプランが一時停止可能でシリアライズ可能だと述べているが、この用語とは結び付けていない
- [[DefinedTerm/human-in-the-loop]] — 関連する考え方。情報源は重要なステップでの人間による確認を、この設計の説明の中ではなく、仕様駆動開発全般の文脈で扱っている
