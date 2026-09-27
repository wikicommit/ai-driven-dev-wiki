---
title: "ast-grep"
type: "schema:SoftwareApplication"
lang: ja
tags: [コードレビュー, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/ast-grep.md"
source_commit: "62375f91cd50b55903e4c7e317338dbf1f45f8fe"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "コードのパターンを大規模にマッチングするための AST ベースのツール。tree-sitter のパーサーを基盤に Rust で書かれており、正規表現に似たシンプルなクエリ言語を用いる。CodeRabbit は AST パターンに基づくレビュー指示のためにこれを利用している。"
  applicationCategory: "AST ベースのコードパターンマッチング兼リンティングツール"
---

ast-grep は、Phodal による AI 支援コードレビューの章の中で、そのルール設定のドキュメントへのリンクとともに、「コードを大規模に管理するための新しい AST ベースのツール」として紹介されている。Rust で書かれており、tree-sitter のパーサーを使って多くの主要なプログラミング言語の抽象構文木を生成し、正規表現をモデルにしたシンプルなクエリ言語で開発者がコードのパターンをマッチングできるようにする。

## 機能

そのルール設定は 3 種類の条件を組み合わせる。アトミックルールはパターン、tree-sitter のノード種別、または正規表現でマッチングする。リレーショナルルールは、他のコードに対する相対的な位置（inside、has、follows、precedes）によってマッチを制約する。コンポジットルールは all、any、not で他のルールを組み合わせる。例には matches キーも示されている。

章では、コーディング規約を強制するだけでなく、ast-grep がコードの意図 ― ネットワーク呼び出し、エラー処理のパターン、リソース管理、並行処理のパターンの検出 ― を浮かび上がらせることができると説明している。

## 採用とエコシステム

[[SoftwareApplication/coderabbit]] は、AST パターンに基づくレビュー指示をサポートするために内部で ast-grep を利用している。章に示された設定例では、必須のセキュリティルールを有効にし、カスタムルールのディレクトリとルールパッケージを指定している。章は CodeRabbit の記事を要約する形で、この組み合わせを AI ネイティブな汎用リンターとして提示している。ast-grep が抽出したパターンとコンテキストが LLM に渡されることでより正確な修正提案が生成され、一方で決定論的なマッチングが、生成 AI 単独で生じるノイズとばらつきを減らすというものである。
