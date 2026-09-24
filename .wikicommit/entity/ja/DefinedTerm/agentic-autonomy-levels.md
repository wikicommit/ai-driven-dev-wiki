---
title: "エージェント自律性レベル"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-autonomy-levels.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "AI コーディングエージェントの自律性を分類する 6 段階の体系。単一のはしごではなく、エージェンシー（単一のエージェントがどこまで進むか）とオーケストレーション（いくつのエージェントが動き、誰がそれらを調整するか）という 2 つの別々の軸から構成される。"
---

エージェント自律性レベル（Agentic Autonomy Levels）は、AI コーディングエージェント（あるいはエージェントの一群）がどの程度自律的に動作するかを分類するための 6 段階の体系であり、別々に測られる 2 つの軸から構成される。1 つはエージェンシー、すなわち人間の判断が必要になるまでに単一のエージェントがどこまで進むことを許されるかであり、もう 1 つはオーケストレーション、すなわちいくつのエージェントが動き、誰がそれらを調整するかである。この体系ではオーケストレーションはスケールの上端近くになって初めて区別の要因となるため、2 つの軸は合わせて 1 つの上昇として読まれる。

## 用法

6 つのレベルは次のとおりである。**Level 0（Assist）** — エージェントはアクションを提案し、そのすべてについて人間が判断する。**Level 1（Supervised action）** — エージェントは編集やコマンドの実行を行うが、影響の大きいことの前には確認を求める。**Level 2（Scoped task delegation）** — 明確な目標と完了の定義を持つ範囲の限定されたタスクが引き渡され、テストの合格などの証拠によって検証される。**Level 3（Goal-driven autonomy）** — エージェントは、測定可能で自動化可能な停止条件によって定義された目標に到達するために必要なことは何でも行う。**Level 4（Parallel delegation）** — 複数のエージェントがタスクの互いに隔離された部分を並列に処理する。そして **Level 5（Managed-by-exception orchestration）** — マネージャーエージェントが定められたポリシーに照らしてワーカーエージェントを割り当て、その出力を検証し、例外だけを人間にエスカレーションする。

この体系は、Steve Yegge による以前の単一軸の自律性のはしご（「Welcome to Gas Town」より）に対する 2 軸の代替案として提示されている。その根拠は、単一の数値では個々のエージェントの信頼レベルと、多数のエージェントを同時に調整する組織の技能とを別々に表現できない、というものである。

## 関連用語

[[BlogPosting/agentic-autonomy-levels]]
