---
title: "Agent Security Bench（ASB）"
type: "schema:Dataset"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/Dataset/agent-security-bench.md"
source_commit: "fed0100a95b9cbca3a6a11c43d68e28bc873bdea"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "LLM ベースのエージェントに対する攻撃と防御を評価するためのベンチマークフレームワーク。10 のシナリオ（e コマース、自動運転、金融など）、10 のエージェント、400 を超えるツール、27 種類の攻撃・防御手法、7 つの評価指標にまたがり、Agent Security Bench の論文で導入された。"
  creator: ["Hanrong Zhang", "Jingyuan Huang", "Kai Mei", "Yifei Yao", "Zhenting Wang", "Chenlu Zhan", "Hongwei Wang", "Yongfeng Zhang"]
  url: "https://github.com/agiresearch/ASB"
---

Agent Security Bench（ASB）は、[[ScholarlyArticle/agent-security-bench]] で導入されたベンチマークフレームワークであり、e コマース、自動運転、金融といった現実的なシナリオにおいて、LLM ベースのエージェントに対する攻撃と防御を定式化し、ベンチマークし、評価するために設計されている。

## 内容

ASB は、10 のシナリオ、それらのシナリオを対象とする 10 のエージェント、400 を超えるツール、27 種類の攻撃・防御手法、7 つの評価指標にまたがる。エージェントの動作のさまざまな段階を狙う攻撃を定式化している。ユーザープロンプトを直接操作する直接プロンプトインジェクション（DPI）攻撃、ツールの応答に悪意ある指示を埋め込む間接プロンプトインジェクション（IPI）攻撃、敵対的なキーと値のペアによって検索拡張生成のメモリデータベースを汚染するメモリポイズニング攻撃、エージェントの隠されたシステムプロンプトを狙う Plan-of-Thought（PoT）バックドア攻撃、そしてこれらを組み合わせた複合攻撃である。評価指標には攻撃成功率（ASR）と拒否率（RR）が含まれ、それぞれ攻撃や防御がどれほど効果的か、そしてエージェントが安全でない要求をどれほどうまく認識して拒否できるかを測るために用いられる。

## 出自

ASB は浙江大学とラトガース大学の研究者によって作成され、そのコードは github.com/agiresearch/ASB で公開されている。

## 利用

[[ScholarlyArticle/agent-security-bench]] は ASB を用いて、10 種類のプロンプトインジェクション攻撃、1 つのメモリポイズニング攻撃、PoT バックドア攻撃、4 種類の複合攻撃、およびそれらに対応する 11 の防御を 13 の LLM バックボーンにわたってベンチマークし、それぞれについて攻撃成功率、拒否率、およびそれらを組み合わせた Net Resilient Performance 指標を報告している。
