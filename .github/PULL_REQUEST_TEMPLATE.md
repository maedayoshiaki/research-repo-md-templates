<!-- PR テンプレート。GitHub が PR 作成時に自動で読み込みます。 -->

## Summary（概要）
{{この PR で何を変えたか（1〜3 文）}}

## Motivation（動機）
{{なぜ必要か。関連 issue: #}}

## Changes（変更点）
- {{...}}
- {{...}}

## Collaboration（AI / 人間の分担）
- **Mode:** `Human Driver` / `Pair Programming` / `AI Draft → Human Rewrite` / `AI Delegate`

| Area | Human / AI / Pair | Reason |
|---|---|---|
| 設計 | {{...}} | {{...}} |
| 実装 | {{...}} | {{...}} |
| テスト | {{...}} | {{...}} |
| 高速化・定型処理 | {{...}} | {{...}} |

## Human Coding Slots（人間が書いた箇所）

学習目的の変更では、人間が実際に書いた・書き直した部分を記録する。
学習目的でない場合は「該当なし」と書く。

| File / Function | 人間が書いた内容 | AI の支援内容 | 学んだこと |
|---|---|---|---|
| {{src/...}} | {{...}} | {{ヒント / 疑似コード / レビュー / テスト案}} | {{...}} |

## Design Review（設計判断）
- [ ] 非自明な設計判断はない
- [ ] 非自明な設計判断がある → `PLANS.md` / `docs/ARCHITECTURE.md` / ADR に記録した
- [ ] 必要な場合、2〜5 案を比較した

採用案と理由：{{...}}

## Learning（学習確認）
- [ ] 学習目的の変更ではない
- [ ] 人間が主要な関数の入出力を説明できる
- [ ] 人間が主要な設計判断を説明できる
- [ ] 人間が一部を自分で実装または書き直した
- [ ] `Human Coding Slots` に人間が書いた箇所を記録した
- [ ] 必要なら `docs/LEARNING.md` を更新した

## Explain-back Summary

人間が説明できること：

- [ ] 主な入出力
- [ ] 主要な責務
- [ ] なぜこの設計にしたか
- [ ] どこを変更すれば拡張できるか
- [ ] どのテストで正しさを確認したか

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
