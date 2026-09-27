---
title: "CodeActAgent"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, オープンソース]
translated_from: ".wikicommit/entity/en/SoftwareApplication/codeactagent.md"
source_commit: "c30b98db983bd016bce35703f3ae928b84c5f04c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Llama2 と Mistral からファインチューニングされた、実行可能な Python コードを出力することで行動するオープンソースの LLM エージェント。Python インタプリタと統合されており、既存のライブラリを使って高度なタスクを実行し、自律的にセルフデバッグするよう調整されている。"
  applicationCategory: "LLM コーディングエージェント"
  featureList: "実行可能な Python コードを出力することで行動する。Python インタプリタと統合されている。既存のライブラリを使ってモデルの学習などの高度なタスクを実行する。自律的にセルフデバッグする。自然言語でユーザーと協働する"
---

CodeActAgent は、[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] の著者らが
[[DefinedTerm/codeact]] を実践に移すために構築したオープンソースの LLM エージェントである。CodeAct が
アプローチ（エージェントの行動を、実行可能な Python コードという統一された行動空間に集約すること）であるのに対し、
CodeActAgent は、そのように動作するよう著者らが Llama2 と Mistral を出発点としてファインチューニングしたモデルである。

論文はこれを自らの分析から導かれたものとして位置づけている。広く使われている JSON ベースおよびテキストベースの
行動形式に対して CodeAct が示したと報告される性能こそが、解釈可能なコードを実行することで環境と相互作用し、
自然言語でユーザーと協働するオープンソースの LLM エージェントを著者らが構築する動機となった。

## 機能

CodeActAgent は Python インタプリタと統合されており、それによってコードによる行動が出力されるだけでなく実際に
実行される。論文は、既存のライブラリを使って高度なタスク（例として挙げられているのはモデルの学習）を実行するよう
独自に調整されており、自律的にセルフデバッグできるものとして説明している。行動することに加えて、自然言語で
ユーザーと協働する。

## 採用とエコシステム

このエージェントは、同じ著者らが収集した、CodeAct を用いた 7k 件のマルチターンのインタラクションからなる
データセットである [[Dataset/codeactinstruct]] でファインチューニングされた。著者らは、このデータを既存のデータと
組み合わせて使うことで、モデルの汎用的な能力を損なうことなく、エージェント指向のタスクにおけるモデルの性能を
向上させられると報告している。コード、データ、モデル、デモは <https://github.com/xingyaoww/code-act> で
公開されているとされる。
