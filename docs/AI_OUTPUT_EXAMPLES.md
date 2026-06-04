# AI_OUTPUT_EXAMPLES.md — AI Response Examples

AI コーディングエージェントに期待する回答形式の例。
目的は、AI に丸投げせず、人間が設計判断・中核実装・学習確認に参加できるようにすること。

## Principles

- 非自明な作業では、実装前に短い方針を出す。
- 設計判断がある場合は、2〜5 案を出し、人間が選ぶ余地を残す。
- `Human Coding Slots` はすべての作業で必須ではない。
- 学習価値が高い作業では、`Human Coding Slots` を積極的に提案する。
- AI は、実装・レビュー・テスト案・リファクタ案を支援する。
- 学習対象の中核部分は、AI が勝手に完成実装しない。
- 完了報告では、AI が書いた箇所、人間が書いた箇所、未確認箇所を分けて書く。

## When to Suggest Human Coding Slots

AI は次のような場合に `Human Coding Slots` を提案する。

- 新しい言語機能、ライブラリ、API を学ぶとき
- 関数分割、クラス設計、責務分離を学ぶとき
- デザインパターンや実装スタイルを比較・採用するとき
- 研究アルゴリズム、loss、評価指標、前処理などの中核処理を書くとき
- 人間が今後も自力で修正・拡張できるようにしたい箇所があるとき

次のような場合は省略してよい。

- typo
- rename
- format / lint
- 設定の微修正
- 明らかに定型的な処理
- 学習目的でない docs only の軽微な変更

---

## Example 1: 作業開始時の回答

```md
## Task understanding
{{この作業で達成すること}}

## Current context
- {{既存構成・制約の理解}}
- {{関連する docs / issue / 既存コード}}

## Proposed approach
1. {{手順1}}
2. {{手順2}}
3. {{手順3}}

## Recommended Human Coding Slots

| Slot | 人間が書く部分 | 学習価値 | AI が出してよい支援 | 完了条件 |
|------|----------------|----------|----------------------|----------|
| H1 | `{{file}}` の `{{function}}` | {{学びたい概念}} | 仕様整理、疑似コード、レビュー、テスト案 | 人間が実装し、テスト通過 |
| H2 | `{{test_file}}` の主要ケース | テスト設計 | 境界条件の提案 | 人間が1ケース以上追加 |

## AI-assisted work

| Part | AI が担当してよいこと | 人間確認 |
|---|---|---|
| A1 | 定型的なリファクタ | 必要 |
| A2 | lint / format 修正 | 不要または軽い確認 |

## Confirmation needed
- {{人間に選んでほしい設計判断}}
```

---

## Example 2: 設計案を出す回答

```md
## Design alternatives

| 案 | 実装スタイル / パターン | 参照元・分類 | 概要 | 長所 | 短所 | 学習価値 |
|---|--------------------------|--------------|------|------|------|----------|
| A | Simple procedural | Basic style | {{...}} | {{...}} | {{...}} | 処理の流れを素直に理解できる |
| B | Strategy pattern | GoF / Behavioral | {{...}} | {{...}} | {{...}} | 手法差し替えの設計を学べる |
| C | Pipeline architecture | Architecture pattern | {{...}} | {{...}} | {{...}} | 前処理・変換・評価の分離を学べる |
| D | Repository pattern | Enterprise application pattern | {{必要なら}} | {{...}} | {{...}} | データアクセスの責務分離を学べる |
| E | Registry / plugin style | Research-code style | {{必要なら}} | {{...}} | {{...}} | metric / loss / method の追加を学べる |

## Recommendation
まずは案 {{A/B/C/D/E}} を推奨する。理由は {{理由}}。

## Simpler alternative check
- より単純な実装で十分か: {{Yes / No / Partial}}
- 過剰設計でない理由: {{...}}

## Human decision
人間が以下を決める。

- 採用する案: {{A/B/C/D/E}}
- 今回学びたい実装スタイル: {{...}}
- 今回はやらないこと: {{Non-Goals}}
```

---

## Example 3: 実装中の回答

```md
## Progress
- 完了: {{完了した作業}}
- 進行中: {{進行中の作業}}
- 未着手: {{未着手の作業}}

## Human Coding Slot status

| Slot | 状態 | コメント |
|---|---|---|
| H1 | Waiting for human | `{{function}}` は人間が実装する想定のため未変更 |
| H2 | Done | 人間実装後に AI がレビュー済み |

## Notes
- {{設計上の注意}}
- {{テスト時の注意}}
```

---

## Example 4: 完了報告

```md
## Summary
{{何を変更したか}}

## Changed files

| File | Change | Authoring |
|---|---|---|
| `{{file1}}` | {{変更内容}} | Human-written / AI-assisted / AI-generated |
| `{{file2}}` | {{変更内容}} | AI-generated, human review required |

## Human Coding Slots

| Slot | 結果 | 確認方法 |
|---|---|---|
| H1 | {{人間が実装した内容}} | {{test / review / small input}} |

## Verification
- [ ] format
- [ ] lint
- [ ] typecheck
- [ ] test
- [ ] docs only, so code checks skipped

## Remaining issues
- {{残課題}}
- {{人間レビューが必要な箇所}}
```

---

## Example 5: PR 本文の出力

```md
## Summary
{{この PR の概要}}

## Motivation
{{なぜ必要か}}

## Changes
- {{変更点1}}
- {{変更点2}}

## Human-written parts

| File | Section / Function | Reason |
|---|---|---|
| `{{file}}` | `{{function}}` | 学習目的・中核ロジックのため人間が実装 |

## AI-assisted parts

| File | Section / Function | Human Review |
|---|---|---|
| `{{file}}` | {{section}} | Required / Done / Not needed |

## Implementation style / pattern review

| 案 | 実装スタイル / パターン | 参照元・分類 | 採用 / 不採用 | 理由 |
|---|---|---|---|---|
| A | {{...}} | {{...}} | {{...}} | {{...}} |
| B | {{...}} | {{...}} | {{...}} | {{...}} |

## Test plan
- [ ] {{テスト1}}
- [ ] {{テスト2}}

## Learning
- Learned: {{学んだ概念}}
- Related: `docs/LEARNING.md`
- Code Reproduction: Yes / Partial / No
```

---

## Pattern Reference Policy

AI は、設計パターンや実装スタイルを固定リストから選ぶ必要はない。
ただし、できるだけよく知られた分類や名前を使い、分類も添える。

参照する分類の例：

- Basic styles: procedural, functional, object-oriented, data-oriented
- GoF design patterns: creational, structural, behavioral patterns
- Architectural patterns: Layered, Pipeline, MVC, Hexagonal Architecture, Clean Architecture
- Enterprise application patterns: Repository, Unit of Work, Service Layer, Data Mapper
- Research-code patterns: config-driven experiment, registry-based metric/loss selection, plugin-style method extension, script-first prototype

AI は、パターン名を使う場合、必ず次を確認する。

- 小さい実装に対して過剰設計ではないか
- より単純な実装では不十分か
- 将来の拡張で本当に有利か
- 人間がその抽象化を説明できるか
