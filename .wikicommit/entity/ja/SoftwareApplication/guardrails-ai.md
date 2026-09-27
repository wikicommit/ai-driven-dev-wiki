---
title: "Guardrails AI"
type: "schema:SoftwareApplication"
lang: ja
tags: [ガードレール, LLM, 検証]
translated_from: ".wikicommit/entity/en/SoftwareApplication/guardrails-ai.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "LLM の呼び出しを、再利用可能なバリデーターで構成した Input Guard と Output Guard で包む Python フレームワーク。LLM の出力を、宣言した構造化された形に強制することもできる。"
  applicationCategory: "LLM ガードレールフレームワーク"
  featureList: "バリデーターから構成する Input/Output Guard、Guardrails Hub のバリデーターコレクション、Pydantic ベースの構造化出力生成、REST API を備え Flask で提供されるスタンドアロンの Guardrails Server"
---

Guardrails AI は、同プロジェクトが「信頼性の高い AI アプリケーション」と呼ぶものを構築するための Python
フレームワークであり、その README は目的を一つではなく二つの機能として述べている。一つ目は、アプリケーション内で
**Input Guard と Output Guard** を実行することである。これは、モデルに入力されるものとモデルから出力される
ものについて、特定の種類のリスクを検出・定量化・緩和する仕組みである。二つ目は **LLM から構造化データを生成
すること** であり、モデルの出力を、アプリケーションが事前に宣言した形に制約する。

PyPI から `guardrails-ai` としてインストールでき、ライセンスは Apache-2.0 である。より広い概念である
[[DefinedTerm/guardrails]] の具体的な実装の一つにあたる。

## 機能

**バリデーター** は測定の単位であり、特定の一種類のリスクに対する事前構築済みのチェックである。バリデーターは
`Guard` に組み合わされ、Guard が LLM の入力と出力をインターセプトする。README の実例では、正規表現マッチから
Guard を構築する例と、競合他社チェックと有害な言語のチェックを組み合わせて Guard を構築する例が示されており、
それぞれに例外の送出などの `on_fail` アクションが設定されている。**Guardrails Hub** はそれらのバリデーターの
出どころとなるコレクションで、guardrailsai.com/hub で文書化されている。また `guardrails` CLI がプロジェクトを
設定し、ガードの構成を作成する。

構造化出力については、求める形を記述した Pydantic の `BaseModel` から Guard を構築し
（`Guard.for_pydantic(output_class=..., prompt=...)`）、フレームワークはモデルに応じて二つの経路のいずれかで
その形を得る。LLM が関数呼び出しをサポートしていればそれを使い、そうでなければプロンプト最適化、すなわち期待する
出力スキーマをプロンプトに追記し、モデル自身が構造化データを生成できるようにする方法を用いる。

Guardrails はライブラリとしてではなく **スタンドアロンのサービス** として動かすこともできる。`guardrails start`
は REST API の背後で Flask を使ってこれを提供し、プロジェクトはこれを Guardrails を活用したアプリケーションの開発と
デプロイを簡素化するものとして紹介している。

## 採用とエコシステム

リポジトリ内にあるプロジェクト自身のニュース項目には、このプロジェクトに関する古い資料を読む人にとって注目すべき
二つの変更が記録されている。2025 年 2 月には **Guardrails Index** を公開した。プロジェクトはこれを、一般的な
六つのカテゴリーにわたる 24 のガードレールの性能とレイテンシを比較する、この種のものとして初のベンチマークと説明
している。2026 年 7 月には、バリデーターを `pip` で直接インストールする標準の PyPI パッケージへ移行すること
（README の例はすでにその形式、つまりハブの URL ではなく `pip install guardrails-ai-regex-match` を使っている）、
そしてホスト型のリモート推論を終了し、2026 年 8 月 25 日に提供を打ち切る予定であることを発表した。

## 関連

[[DefinedTerm/guardrails]]、[[SoftwareApplication/nemo-guardrails]]
