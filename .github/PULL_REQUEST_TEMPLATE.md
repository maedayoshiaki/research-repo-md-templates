<!-- PR テンプレート。GitHub が PR 作成時に自動で読み込みます。 -->

## Summary（概要）
{{この PR で何を変えたか（1〜3 文）}}

## Motivation（動機）
{{なぜ必要か。関連 issue: #}}

## Changes（変更点）
- {{...}}
- {{...}}

## Human Involvement Profile

- **Repository Profile:** `L0 Speed First` / `L1 Review Gate` / `L2 Selective Human Slots` / `L3 Learning First` / `L4 Human Driver`
- **This PR Mode:** `Human Driver` / `Pair Programming` / `AI Draft → Human Rewrite` / `AI Delegate`
- **Profile Override:** `none` / `stricter` / `looser`
- **Override Reason:** {{必要なら理由}}

Profile compliance:

- [ ] この PR は Repository Profile に従っている
- [ ] Profile より人間の介入度を上げた
- [ ] Profile より人間の介入度を下げた
- [ ] 下げた理由を PR に書いた

## Collaboration（AI / 人間の分担）

| Area | Human / AI / Pair | Reason |
|---|---|---|
| 設計 | {{...}} | {{...}} |
| 実装 | {{...}} | {{...}} |
| テスト | {{...}} | {{...}} |
| 高速化・定型処理 | {{...}} | {{...}} |
| Subagent 利用 | none / used | {{調査・レビュー・機械的修正など。使った場合は main agent が確認した内容を書く}} |

## Human Coding Slots（人間が書いた箇所）

Repository Profile に従って記録する。

- `L0`: 該当なしでよい
- `L1`: レビュー対象のみでもよい
- `L2`: 実装・書き直し・説明した Slot を記録する
- `L3`: 少なくとも 1 個の `Design Vertical Slice` を記録する
- `L4`: 中核実装の Slot を記録する

| File / Function | 人間が書いた内容 | AI の支援内容 | 学んだこと |
|---|---|---|---|
| {{src/...}} | {{...}} | {{ヒント / 疑似コード / レビュー / テスト案}} | {{...}} |

<details>
<summary><b>L3 Design Vertical Slice（設計縦断スライス）— L3 の PR のみ展開して記入</b></summary>


`L3 Learning First` でデザインパターンや抽象化を扱う場合に記録する。
人間が文脈のない穴埋めだけを担当しないように、抽象・代表具象・最小呼び出し・契約テストのつながりを確認する。

- [ ] L3 ではないため該当なし
- [ ] 人間が抽象インターフェース / 抽象クラス / Protocol を書いた
- [ ] 人間が代表的な具象クラスを少なくとも 1 つ書いた
- [ ] 人間が最小の呼び出し例を書いた、または既存呼び出し側を変更した
- [ ] 人間が契約テストを書いた、または契約を説明した
- [ ] AI は全体文脈、候補設計、疑似コード、レビュー、類似実装、統合作業を担当した

| Abstract / Interface | Representative Concrete | Minimal Usage | Contract Test | AI-held Context |
|---|---|---|---|---|
| {{Metric / Sampler / Repository など}} | {{PSNRMetric / RandomSampler など}} | {{どこから抽象経由で呼ぶか}} | {{置換可能性をどう確認するか}} | {{既存コード、統合先、類似実装、境界条件}} |

</details>

<details>
<summary><b>Implementation Style / Pattern Review — 非自明な設計判断がある PR のみ展開して記入</b></summary>


非自明な設計判断がある場合は、検討した実装スタイルや設計パターンを書く。
候補は固定しない。GoF patterns、architecture patterns、enterprise application patterns、research-code patterns、functional / procedural / object-oriented styles などから、タスクに合うものを選ぶ。

| 案 | 実装スタイル / パターン | 参照元・分類 | 採用 / 不採用 | 理由 |
|---|---|---|---|---|
| A | {{...}} | {{...}} | {{...}} | {{...}} |
| B | {{...}} | {{...}} | {{...}} | {{...}} |
| C | {{必要なら}} | {{...}} | {{...}} | {{...}} |

過剰設計でない理由、またはより単純な実装で十分だった理由：{{...}}

</details>

## Design Review（設計判断）
- [ ] 非自明な設計判断はない
- [ ] 非自明な設計判断がある → `PLANS.md` / `docs/ARCHITECTURE.md` / ADR に記録した
- [ ] 必要な場合、2〜5 案を比較した

採用案と理由：{{...}}

## Learning（学習確認）
- [ ] 学習目的の変更ではない
- [ ] Profile 上、人間による実装は不要
- [ ] 人間はレビューのみ行った
- [ ] 人間が主要な関数の入出力を説明できる
- [ ] 人間が主要な設計判断を説明できる
- [ ] 人間が一部を自分で実装または書き直した
- [ ] `Human Coding Slots` に人間が書いた箇所を記録した
- [ ] `L3` の場合、抽象・代表具象・呼び出し側・契約テストのつながりを説明できる
- [ ] 必要なら `docs/LEARNING.md` を更新した

## Explain-back Summary

人間が説明できること：

- [ ] 主な入出力
- [ ] 主要な責務
- [ ] なぜこの設計にしたか
- [ ] どこを変更すれば拡張できるか
- [ ] どのテストで正しさを確認したか
- [ ] 抽象と具象の関係
- [ ] 新しい具象実装を追加する手順

## Test Plan（テスト計画）
- [ ] {{追加/更新したテスト}}
- [ ] 検証スタック通過（format / lint / typecheck / test）
- [ ] （研究）seed 固定で再現を確認
- [ ] docs only（コード変更なし）

## Theory（数式・理論の変更）
- [ ] 数式に変更はない
- [ ] 数式を変更した → `docs/THEORY.md` を更新し、**人間レビュー済み**／式↔コード対応を記載

## Docs & State（ドキュメント更新）
- [ ] `STATUS.md` を更新
- [ ] 確定事項を `MEMORY.md` へ反映（必要なら）
- [ ] 設計判断がある場合、複数案と選定理由を記載（`PLANS.md` / `docs/ARCHITECTURE.md` / ADR）

## Compatibility（互換性）
- [ ] 破壊的変更なし
- [ ] 破壊的変更あり → 人間確認済み（AGENTS.md）。内容: {{...}}