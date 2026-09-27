---
title: "SpecRover"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, コードレビュー, 検証]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/specrover.md"
source_commit: "0905902793f108bf59d40f17ccaecab6d323e38b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AutoCodeRover を基盤に構築された、プログラムの自律的な改善のための LLM エージェント。コード検索の過程で意図された振る舞いの仕様を推論し、判断の理由を説明するレビュアーエージェントで候補パッチを吟味することによって、GitHub のイシューを解決する。"
  applicationCategory: "イシューの自動解決とプログラム修復のための LLM エージェント"
  featureList: "再現エージェント、意図された振る舞いを表す関数要約を伴うコンテキスト取得、パッチ作成エージェント、パッチと再現テストを判定するレビュアーエージェント、リトライを伴う回帰テストのチェック、理由を明示する選択エージェント、エビデンスの出力（バグのある箇所とその意図された振る舞い、再現テスト、承認または選択の理由）"
---

SpecRover は、GitHub のイシューに記述されたバグ修正や機能追加といったソフトウェアのイシューを、まずコードが何をすべきかを推論することによって解決する LLM エージェントである。これを導入した論文
[[ScholarlyArticle/specrover-code-intent-extraction-via-llms]] は、SpecRover を
[[SoftwareApplication/autocoderover]] の後継と位置づけている。SpecRover は AutoCodeRover のコードベース上に実装されてそのコンテキスト取得 API を再利用しており、そこに関数要約の抽出、パッチのレビュー、パッチの選択を加えている。
著者らは、そのソースコードと実験のアーティファクトが Zenodo で公開されていると述べており、また SpecRover を AutoCodeRover-v2 と同一のものとしている。AutoCodeRover-v2 は、ワンクリックでのイシュー解決を提供する GitHub ボットとしてもパッケージ化されている。

## 機能

イシューの記述とコードベースが与えられると、SpecRover は一連の LLM エージェントを実行する。再現エージェントは、報告された不具合を再現するテストを書く。コンテキスト取得エージェントは構造を考慮した API を通じてコードベースを検索し、取得した関数ごとに、イシューの要件を満たすためにその関数がどのように振る舞うべきかを自然言語で短く要約する。そして最後にバグのある箇所を決定する。続いてパッチ作成エージェントが、対応する関数要約を手がかりに、それらの箇所のコードを修正する。

レビュアーエージェントは、元のプログラムとパッチを適用したプログラムの両方で再現テストを実行し、その結果、イシュー、テストを踏まえて、パッチとテストがそれぞれ正しいかどうかを説明付きで個別に判定する。却下されたパッチやテストは、このフィードバックを用いて修正される。承認されたパッチはプロジェクトの回帰テストスイートに照らしてチェックされ、回帰が現れた場合はあらかじめ定められた回数までワークフローがリトライされる。どの候補も通過しなかった場合は、選択エージェントがイシューの記述をもとに 1 つを選び、その理由を述べる。SpecRover は最終的なパッチとともに、バグのある箇所とその意図された振る舞い、再現テスト、そしてパッチが承認または選択された理由を出力する。著者らは、これをコミットメッセージとして使ったり、将来の回帰を追跡するためにコードとともに保存したりできると示唆している。

## 採用とエコシステム

SpecRover はバックエンドとして複数の LLM をサポートしている。論文の実験では Claude 3.5 Sonnet を主要なモデルとして使い、Claude API がエラーを返した場合に限り、そのタスクについて GPT-4o に切り替えている。Python リポジトリの GitHub イシュー向けに設計されたものではあるが、論文では DARPA の AI Cyber Challenge で扱われた Linux カーネルの C 言語のセキュリティ脆弱性に対して、脆弱性レポートを出発点に SpecRover を適用してみせている。SpecRover は、[[DefinedTerm/software-issue-resolution]] と
[[DefinedTerm/automated-program-repair]] のためのエージェントの系譜に属する。
