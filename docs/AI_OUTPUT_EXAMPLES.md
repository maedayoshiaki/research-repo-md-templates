# AI_OUTPUT_EXAMPLES.md — AI Response Examples

AI コーディングエージェントに期待する回答形式の例。
目的は、AI に丸投げせず、人間が設計判断・中核実装・学習確認に参加できるようにすること。
ただし、人間の介入度は `AGENTS.md` の Repository Human Involvement Profile に従う。

## Principles

- 非自明な作業では、実装前に短い方針を出す。
- 設計判断がある場合は、2〜5 案を出し、人間が選ぶ余地を残す。
- `Human Coding Slots` はすべての作業で必須ではない。
- 学習価値が高い作業では、Repository Profile に応じて `Human Coding Slots` を提案する。
- AI は、実装・レビュー・テスト案・リファクタ案を支援する。
- 学習対象の中核部分は、`L2` 以上では AI が勝手に完成実装しない。
- 完了報告では、AI が書いた箇所、人間が書いた箇所、未確認箇所を分けて書く。
- コーディングエージェントが subagent を使える場合は、調査・レビュー・テスト失敗の切り分けに使ってよい。ただし Profile と人間レビューを迂回しない。

## Profile-Based Response Rules

| Profile | AI の基本応答 | Human Coding Slots | 完了報告で強調すること |
|---|---|---|---|
| `L0 Speed First` | すぐ実装方針と完成実装に進んでよい | 原則省略 | 変更点、実行方法、検証結果 |
| `L1 Review Gate` | 完成実装を出してよいが、主要 diff を説明する | 任意 | 人間が読むべき diff、設計意図 |
| `L2 Selective Human Slots` | 重要部分だけ Slot 化し、周辺は実装してよい | 1〜3 個 | Slot、AI 実装部分、理解確認 |
| `L3 Learning First` | 中核実装はヒント・疑似コード・レビュー中心 | 2〜4 個 | 人間が実装した中核、学習事項 |
| `L4 Human Driver` | 完成コードを先に出さず、問題分解とレビュー中心 | 中核処理を小さく分割 | 人間主導の実装、再実装できる範囲 |

## When to Suggest Human Coding Slots

AI は次のような場合に、Repository Profile に応じて `Human Coding Slots` を提案する。

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
- `L0` / `L1` で速度やレビューを優先する作業

---

## Example 1: 作業開始時の回答（L2）

```md
## Task understanding
{{この作業で達成すること}}

## Repository profile
- Profile: `L2 Selective Human Slots`
- Mode: `Pair Programming`
- Override: none

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

## Example 2: L0 Speed First の回答

```md
## Summary
Profile は `L0 Speed First` なので、Human Coding Slots は省略します。
AI 側で実装、簡易テスト、実行方法の整理まで進めます。

## Proposed changes
- {{変更点1}}
- {{変更点2}}

## Human review points
- {{研究前提・数式・評価指標など、人間確認が必要な点}}
- {{出力が期待と合っているか}}

## Verification
- {{実行コマンド}}
- {{確認結果}}
```

---

## Example 3: L4 Human Driver の回答

```md
## Task breakdown
Profile は `L4 Human Driver` なので、完成実装は先に出しません。
まず中核処理を小さい Human Coding Slots に分けます。

## Human Coding Slots

| Slot | 人間が書く部分 | AI が出してよい支援 | 完了条件 |
|---|---|---|---|
| H1 | {{関数の責務}} | 入出力仕様、疑似コード、テスト観点 | 人間実装後にレビュー |
| H2 | {{境界条件処理}} | よくあるミス、失敗ケース | 小さいテスト通過 |
| H3 | {{テスト本体}} | ケース案、期待値の考え方 | 主要ケースを人間が追加 |

## Hints for H1
- 入力: {{...}}
- 出力: {{...}}
- 境界条件: {{...}}
- 疑似コード:
  1. {{...}}
  2. {{...}}

人間が実装した後、レビューと改善案を返します。
```

---

## Example 4: 設計案を出す回答

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

## Example 5: Subagent を使う場合

```md
## Subagent use

このタスクでは subagent を使えるため、次を分担します。
Profile は `{{L1 / L2 / L3}}` なので、subagent は調査・レビュー補助に限定します。

| Agent | 役割 | 出力 | Main agent の確認 |
|---|---|---|---|
| search subagent | 既存 API の利用箇所を探す | 候補ファイル一覧 | 実際の採用箇所を確認 |
| test subagent | 失敗ログを読む | 原因候補 | 修正方針は main agent が統合 |
| docs subagent | Markdown 整合性を見る | 更新漏れ候補 | PR 説明に反映 |

Subagent の出力は未確認情報として扱い、最終判断は main agent が人間に提示します。
```

---

## Example 6: 実装中の回答

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

## Example 7: 完了報告

```md
## Summary
{{何を変更したか}}

## Repository profile
- Profile: `{{L0 / L1 / L2 / L3 / L4}}`
- Mode: `{{Collaboration Mode}}`
- Override: {{none / stricter / looser}}

## Changed files

| File | Change | Authoring |
|---|---|---|
| `{{file1}}` | {{変更内容}} | Human-written / AI-assisted / AI-generated |
| `{{file2}}` | {{変更内容}} | AI-generated, human review required |

## Human Coding Slots

| Slot | 結果 | 確認方法 |
|---|---|---|
| H1 | {{人間が実装した内容。該当なしなら none}} | {{test / review / small input}} |

## Subagent use
- Used: Yes / No
- If yes: {{何に使い、main agent が何を確認したか}}

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

## Example 8: PR 本文の出力

```md
## Summary
{{この PR の概要}}

## Motivation
{{なぜ必要か}}

## Changes
- {{変更点1}}
- {{変更点2}}

## Human Involvement Profile
- Repository Profile: `{{L0 / L1 / L2 / L3 / L4}}`
- This PR Mode: `{{mode}}`
- Profile Override: `{{none / stricter / looser}}`

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
