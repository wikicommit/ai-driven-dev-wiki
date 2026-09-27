---
title: "NVIDIA"
type: "schema:Organization"
lang: ja
tags: [セキュリティ, AI ベンダー, エージェントツーリング]
translated_from: ".wikicommit/entity/en/Organization/nvidia.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "NVIDIA AI Red Team を擁する組織。同チームは AI システムやエージェント型システムを敵対的にテストし、発見した問題を影響を受けるベンダーに開示したうえで、その結果を LLM の振る舞いを評価・制約するためのツールとともに NVIDIA Technical Blog で公開している。また、NeMo Agent Toolkit をはじめ、AI エージェントの構築と最適化のためのオープンソースツールも公開している。"
  url: "https://developer.nvidia.com/"
---

NVIDIA がこの wiki に登場するのは主に AI セキュリティの取り組みを通じてであり、加えてオープンソースのエージェント向けツールの発行元としても登場する。その取り組みを担うのは NVIDIA AI Red Team であり、同チームは AI システムやエージェント型システムを敵対的にテストし、その結果を NVIDIA Technical Blog で公開している。

## 活動と製品

ここでまとめた成果から見える Red Team の実践は、実際にデプロイされているシステムに対して実際に機能する攻撃を構築し、影響を受けるベンダーに開示したうえで、開示のタイムラインとベンダーの対応とともに発見を公開する、というものである。ベンダーが変更を行わないと判断した場合もそのまま公開される。[[SoftwareApplication/openai-codex]] に対する [[DefinedTerm/indirect-agents-md-injection]] 攻撃の報告もこのパターンに沿っており、最初の報告から、この攻撃は依存関係が侵害されるシナリオを超えてリスクを実質的に高めるものではないというベンダーの結論に至るまでの経緯が記されている。

それ以前の開示も、[[SoftwareApplication/langchain]] に対して同じ形をとっていた。Red Team は同ライブラリのチェーンに 3 つの脆弱性を特定・検証しており、いずれも [[DefinedTerm/prompt-injection]] によって到達可能なものだった。これらは、影響を受けるコンポーネントがコアライブラリから削除された後に、メンテナーの承認を得て公開された。この記事には、NVIDIA が即時の緩和策が講じられなかったと説明する状況を受けて、自ら CVE を申請したことが記録されている。また、公開に踏み切った理由として、問題は深刻ではあるものの特定のチェーンに限定されていたこと、そしてその手法が当時すでに広く理解されていたことが述べられている。さらに記事は個別の発見を超えて一般化し、モデルの出力はすべて潜在的に悪意あるものとして扱うべきだと論じている。これは [[DefinedTerm/control-data-plane-confusion]] で展開されている立場である。

研究と並行して、NVIDIA は自社のセキュリティ上の推奨事項が参照するツールも公開している。既知のプロンプトインジェクションの弱点に対してモデルを評価する LLM 脆弱性スキャナーとして紹介されている garak と、LLM の入出力をフィルタリング・保護するための NeMo Guardrails である。この分野のトレーニング教材も公開しており、敵対的機械学習に関する自己ペース型のコースなどがあるほか、Black Hat で AI レッドチームのトレーニングを実施したこともある。同社の NeMo サービスも、先の記事の中で LLM アプリケーションとその統合を支援するサービスとして挙げられている。

セキュリティ以外では、NVIDIA は [[SoftwareApplication/nemo-agent-toolkit]] を公開している。これは Apache 2.0 ライセンスのオープンソースライブラリであり、既存のエージェントフレームワークと併用して、AI エージェントにプロファイリング、オブザーバビリティ、評価、最適化の機能を追加する。その README は、このツールキットを NVIDIA 自身のインフラと結びつけており、入門用の例で使われている NVIDIA NIM のモデルエンドポイントや、大規模環境でのエージェント性能向上を目的とした NVIDIA Dynamo との実験的な統合を挙げている。
