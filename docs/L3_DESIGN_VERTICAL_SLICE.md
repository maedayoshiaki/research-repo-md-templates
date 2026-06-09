# L3_DESIGN_VERTICAL_SLICE.md — L3 の設計縦断スライス

`L3 Learning First` で、デザインパターンや抽象化を学ぶための運用ルール。
目的は、AI に主要文脈を持たせつつ、人間が抽象・具象・利用側・テストのつながりを実装として経験すること。

## Problem

L3 で「主要実装を人間が書く」とだけ決めると、次の問題が起きやすい。

- 人間が文脈のない穴埋めだけを担当する
- AI が抽象や呼び出し側を作り、人間が計算部分だけを書く
- Strategy / Adapter / Template Method などの設計意図を学びにくい
- 開発速度を落とすだけで、設計理解につながらない

そのため L3 では、単独の関数ではなく `Design Vertical Slice` を人間が担当する。

## Definition

`Design Vertical Slice` は、設計パターンの最小成立単位を縦に切り出したもの。

人間が書く中心部分：

1. 抽象インターフェース、抽象クラス、または Protocol
2. 代表的な具象クラス 1 つ
3. 最小の呼び出し例、または既存呼び出し側の変更
4. 契約テスト、または契約を確認する最小テスト
5. 採用した設計パターンの短い理由

AI が担当してよい部分：

- 既存コードの調査
- 全体文脈の整理
- 候補設計の比較
- 疑似コード
- 境界条件とテスト観点
- 人間が書いたコードのレビュー
- 類似する 2 個目以降の具象クラス
- Factory / Registry の周辺実装
- CLI、設定、ログ、ドキュメント更新

## Workflow

1. AI が変わりやすい部分と固定したい部分を分ける。
2. AI が設計案を 2〜5 個提示する。
3. 人間が採用する実装スタイルまたはデザインパターンを選ぶ。
4. AI が `Design Vertical Slice` を定義する。
5. 人間が抽象、代表具象、最小呼び出し、契約テストを書く。
6. AI がレビュー、補助実装、類似実装、統合作業を行う。
7. 人間が explain-back で設計意図を説明する。

## Slice Template

| Slice | 人間が書くもの | AI が支援するもの | 完了条件 |
|---|---|---|---|
| Interface Slice | 抽象インターフェース、責務、契約 | 既存呼び出し側、命名案、候補メソッド | 具象を差し替えられる |
| Concrete Slice | 代表的な具象クラス 1 つ | 疑似コード、境界条件、レビュー | 抽象経由で動く |
| Usage Slice | 最小の呼び出し例 | 統合先、Factory / Registry 案 | 呼び出し側が具象に依存しない |
| Contract Test Slice | 契約テスト | fixture、boilerplate、失敗例 | 新しい具象実装にも同じテストを適用できる |

## Example: Metric Strategy

評価指標を Strategy として実装する場合。

人間が書く：

- `Metric` インターフェース
- `PSNRMetric` の代表実装
- `evaluate(metric: Metric, ...)` の最小呼び出し例
- `Metric` 契約を確認するテスト
- Strategy を採用した理由

AI が書いてよい：

- `SSIMMetric` などの類似実装
- `MetricRegistry`
- 設定ファイルから Metric を生成する補助コード
- README / ARCHITECTURE / LEARNING の更新

良い L3：

```text
Human: Metric interface + PSNRMetric + evaluate(metric) + contract test
AI: context, alternatives, review, similar metrics, registry, docs
```

悪い L3：

```text
Human: PSNRMetric.compute() の中身だけ
AI: interface, registry, caller, tests, docs
```

悪い例では、人間が計算式だけを埋めるため、抽象と具象の関係を学びにくい。

## Example: Adapter

外部ライブラリやストレージを Adapter で隔離する場合。

人間が書く：

- `ArtifactStore` インターフェース
- `LocalArtifactStore` の代表実装
- 保存・読み込みを抽象経由で呼ぶ最小例
- 同じ契約を満たすことを確認するテスト

AI が書いてよい：

- `S3ArtifactStore` など 2 個目以降の実装
- エラー処理の補助
- 設定から store を選ぶ Factory
- ドキュメント更新

## Explain-back Checklist

L3 の PR 前に、人間は次を説明できる状態にする。

- 抽象は何を隠しているか
- 代表具象はその契約をどう満たしているか
- 呼び出し側はどの具体クラスにも依存していないか
- 新しい具象クラスを追加するとき、どこを変更するか
- 契約テストは何を保証しているか
- 今回の抽象化は過剰設計ではないか

## Anti-patterns

避ける。

- 人間が関数の中身だけを埋める
- AI が抽象、具象、呼び出し側、テストをすべて先に完成させる
- 人間が採用パターンを説明できない
- Factory / Registry を先に作り、差し替える実装が 1 個しかない
- 将来の拡張可能性だけを理由に抽象化する

迷ったら、まず素朴な実装と抽象化案を並べ、人間が選ぶ。