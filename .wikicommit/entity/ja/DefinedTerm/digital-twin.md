---
title: "デジタルツイン"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェンティックコーディング, AI支援プログラミング, テスト]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/digital-twin.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Kevin Ryan が説明するエージェンティック開発の文脈における意味では、自律的なエージェントが開発対象にできる外部サービスの振る舞いのクローン——現実のように振る舞いながら実データには一切触れないシミュレート環境。連携する数十のサービスそれぞれについてこれを構築した StrongDM に帰されている。"
---

[[Book/spec-driven-development-ai-native-software-engineering]] で用いられる意味において、デジタルツインとは外部サービスの振る舞いのクローンである。実際のサービスのように振る舞いながら実データには一切触れないシミュレート環境であり、自律的なコーディングエージェントがそれを相手に安全に開発し、テストを受けられるようにする。[[Person/kevin-ryan]] はこの実践を [[Organization/strongdm]] に帰し、同社の [[DefinedTerm/dark-factory]] という営みを支える2つのアーキテクチャ上の工夫の一つとして説明している。

## 用法

その動機となる制約は単純である。StrongDM は数十の外部サービス——例として挙げられているのは Okta、Jira、Slack、Google Drive——と連携しており、開発中の自律的なエージェントに本番 API への認証済み呼び出しをさせるわけにはいかない。エージェントが触れられる範囲を制限するのではなく、同社はすべてのサービスについて振る舞いのクローンを構築した。Ryan はその結果を、速度を保ったままの安全な自律実行だと要約している。

彼は、シミュレート環境が外部評価と並んで、自著の示す方法論に直接関わるものであり、本書を通じて繰り返し登場すると述べている。なお「デジタルツイン」という語はソフトウェアエンジニアリングの外部により広い確立された意味を持つ。ここに記録した定義は情報源が説明するエージェンティック開発における狭い用法であり、情報源自身もこの語を一般的に定義していると主張してはいない。

## 関連用語

デジタルツインは Ryan が記録する StrongDM の2つの工夫の一つであり、もう一方が [[DefinedTerm/external-scenarios]] である。いずれも [[DefinedTerm/dark-factory]] を運営するための前提条件として提示されており、どちらも Ryan が AI ネイティブな実行——仕様を動くソフトウェアに変え、その結果を検証する機械仕掛け——と呼ぶものに属する。[[DefinedTerm/agent-execution-environment]] も参照。
