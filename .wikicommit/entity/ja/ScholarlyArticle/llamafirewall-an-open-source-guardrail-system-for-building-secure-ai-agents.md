---
title: "LlamaFirewall：安全な AI エージェントを構築するためのオープンソースのガードレールシステム"
type: "schema:ScholarlyArticle"
lang: ja
tags: [セキュリティ, プロンプトインジェクション, ガードレール, エージェント]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/llamafirewall-an-open-source-guardrail-system-for-building-secure-ai-agents.md"
source_commit: "90f235c19401779128f2c36166ba9e641fa1393d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "プロンプトインジェクション、エージェントのミスアラインメント、安全でないコードに対する LLM エージェントの最終防御層として意図された、オープンソースでセキュリティに特化したガードレールフレームワーク LlamaFirewall を紹介する Meta の論文。"
  author: ["Sahana Chennabasappa", "Cyrus Nikolaidis", "Daniel Song", "David Molnar", "Stephanie Ding", "Shengye Wan", "Spencer Whitman", "Lauren Deason", "Nicholas Doucette", "Abraham Montilla", "Alekhya Gampa", "Beto de Paola", "Dominik Gabi", "James Crnkovich", "Jean-Christophe Testud", "Kat He", "Rashnil Chaturvedi", "Wu Zhou", "Joshua Saxe"]
  datePublished: "2025-04-29"
  abstract: "LLM は、本番コードを編集し、ワークフローをオーケストレーションし、信頼できない入力に基づいてより重大な結果を伴うアクションを実行する自律エージェントへと進化しており、モデルのファインチューニングやチャットボット向けのガードレールでは十分に対処できないセキュリティリスクをもたらしている。著者らは、AI エージェントに関連するセキュリティリスクに対する最終防御層として設計された、オープンソースでセキュリティに特化したガードレールフレームワーク LlamaFirewall を紹介する。LlamaFirewall は 3 つのガードレールによってプロンプトインジェクション、エージェントのミスアラインメント、安全でないコードを緩和する。汎用的なジェイルブレイク検出器である PromptGuard 2、プロンプトインジェクションや目標のミスアラインメントがないかエージェントの推論を検査する思考連鎖（chain-of-thought）の監査器で、現時点では実験的な Agent Alignment Checks、そしてコーディングエージェントが安全でないコードや危険なコードを生成するのを防ぐことを目的としたオンライン静的解析エンジンである CodeShield である。また、正規表現または LLM プロンプトに基づくカスタマイズ可能なスキャナーも含まれる。LlamaFirewall は Meta の本番環境で使用されている。"
---

Meta によるこの論文は、LLM がコードを書き、ワークフローをオーケストレーションし、Web ページや
メールといった信頼できない入力に基づいて行動する自律エージェントへと変わりつつあるのに対し、
セキュリティ基盤はそれに追いついていないと論じる。既存の取り組みの多くはチャットボットの
コンテンツをモデレーションするものであり、モデル API に組み込まれたプロプライエタリな安全性
システムは可視性、監査可能性、カスタマイズ性が限られている。これらのリスクに対する決定論的な
解決策が存在しないことを踏まえ、著者らは、最終防御層として機能し、システムレベルかつユース
ケース固有のポリシーをサポートするリアルタイムのガードレールモニターが必要だと主張する。

その答えが [[SoftwareApplication/llamafirewall]] である。これは 3 つのガードレールをポリシー
エンジンに統合したオープンソースのフレームワークで、開発者はそこでパイプラインを構築し、
是正戦略を定義し、新しい検出器を組み込むことができる。PromptGuard 2 は直接的な
[[DefinedTerm/jailbreaking]] の試みを検出するためにファインチューニングされた
BERT 系の分類器である。AlignmentCheck は、LLM を用いてエージェントの思考連鎖とアクションを検査し、
[[DefinedTerm/indirect-prompt-injection]] によって目標が乗っ取られた
兆候がないかを調べる実験的な監査器である。CodeShield は、LLM が生成した安全でないコードを検出する
静的解析エンジンである。論文は 2 つのシナリオ、すなわち汚染された Web ページによって目標を
乗っ取られる旅行エージェントと、安全でない SQL パターンを取り込んでしまうコーディングエージェントを
順に取り上げ、各層が必要なときにだけ作動する様子を示している。

評価には、非公開のジェイルブレイクベンチマーク、公開ベンチマークである [[Dataset/agentdojo]]、
そして Meta のエージェント型シミュレーションフレームワーク内で構築された社内の目標乗っ取り
ベンチマークが用いられている。著者らはこのフレームワークの役割を、従来のセキュリティにおける
Snort、Zeek、Sigma になぞらえる。すなわち、ポリシーと検出器のための共有されたオープンな基盤である。

## 要点

- 論文はエージェントのセキュリティリスクを、直接的および間接的な汎用ジェイルブレイク型プロンプトインジェクション、安全でないコーディング慣行、プロンプトインジェクションを介して持ち込まれる悪意あるコードに分類し、それぞれを対応するスキャナーに対応づけている。
- PromptGuard 2 には、mDeBERTa-base をベースとする 8,600 万パラメータのモデルと、DeBERTa-xsmall をベースとする 2,200 万パラメータのモデルがある。PromptGuard 1 のより広範な目標乗っ取り検出という対象範囲は、過剰な偽陽性を引き起こしたため、明示的なジェイルブレイク手法に絞り込まれた。
- 著者らの分布外（out-of-distribution）ジェイルブレイクベンチマークにおいて、PromptGuard 2 86M は英語で偽陽性率 1% のとき再現率 97.5% に達した。PromptGuard 1 では 21.2% であった。
- 著者らは AlignmentCheck を、知る限りにおいて、インジェクション防御のために LLM の思考連鎖をリアルタイムで監査する初のオープンソースのガードレールだと説明している。
- 社内の目標乗っ取りベンチマークでは、Llama 4 Maverick や Llama 3.3 70B などの大規模モデルを用いた AlignmentCheck が、ファインチューニングなしで偽陽性率 4% 未満、再現率 80% 超を達成した。より小規模なモデルでは偽陽性率が高くなった。
- AgentDojo では、ベースラインの攻撃成功率 17.6% が、PromptGuard 2 86M 単独で 7.5%、AlignmentCheck 単独で 2.89%、両者の組み合わせで 1.75% に低下した。一方でタスクの有用性は 47.7% からそれぞれ 47.0%、43.1%、42.7% に低下した。
- 著者らは、AgentDojo が狭い種類の攻撃に焦点を当てているため、より多様な敵対的環境では PromptGuard 単独では不十分な可能性があると指摘している。
- CodeShield は 2 段階のスキャンを用いており、社内の本番デプロイでは入力の約 90% が高速な第 1 段階で判定される。CyberSecEval 3 で評価したところ、安全でないコードの特定において適合率 96%、再現率 79% に達した。

## 注記

著者らは、CodeShield が網羅的ではなく、微妙な脆弱性や文脈に依存する脆弱性を見逃す可能性があること、
AlignmentCheck には大規模で高性能なモデルが必要でレイテンシが増えること、そして AlignmentCheck
自体がガードレールモデルを狙ったインジェクションの標的になりうることを認めている。この最後の点に
ついては、生のツール出力ではなくエージェントの推論とアクションのみを渡すこと、そして入力を
PromptGuard で事前スキャンすることで緩和している。論文は CodeShield が対応する言語数を、序論では
8、評価の節では 7 と記載している。今後の課題としては、マルチモーダルエージェント、モデル蒸留による
レイテンシの低減、悪意あるコードの実行や安全でないツール利用などのより広範な脅威への対応、そして
より現実的なエージェントベンチマークが挙げられている。論文は LlamaFirewall を、
[[SoftwareApplication/nemo-guardrails]]、[[SoftwareApplication/guardrails-ai]]、Invariant Labs の
フレームワークといった他のガードレールフレームワークと比較し、[[DefinedTerm/guardrails]]
というより広い実践の中で、[[DefinedTerm/prompt-injection]] に対する
防御として位置づけている。
