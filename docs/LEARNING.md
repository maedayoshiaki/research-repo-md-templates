# LEARNING.md — Coding Learning Log

コーディング中に学んだことを短く残すファイル。
調べ物の全文保存ではなく、理解した要点、実際に使った小さな例、復習項目だけを書く。

## Purpose

AI に任せきりにせず、人間が理解した設計・文法・ライブラリ・パターンを短く残す。
長い講義ノートではなく、次に同じ実装を読む・直すための学習ログにする。

## Rules

- 調べた内容をそのまま貼らない。
- 自分の言葉で 1〜3 行に要約する。
- 実際に使った小さなコード例を残す。
- 理解が曖昧なものは `Review later` に入れる。
- プロジェクト固有の確定事項は `MEMORY.md` に書く。
- AI 生成コードを採用した場合も、人間が入出力・責務・変更方法を説明できるようにする。

## Learning-first Areas

次は、できるだけ人間が主導して書く。
AI はヒント、最小例、レビュー、テスト案を出す。

- PyTorch の基本構成: `Dataset`, `DataLoader`, `nn.Module`, training loop
- Python の基本設計: 型、例外、ファイル I/O、関数分割
- 研究アルゴリズムの中核処理
- データ構造、loss、評価指標、前処理の設計
- デザインパターンの採否判断

AI に任せやすいもの：

- GPU 高速化の詳細
- CI、format、lint、型チェックの設定
- 定型的なテスト雛形
- ログ、CLI、設定ファイルの下書き
- 互換性対応、単純なリファクタ

## PyTorch Roadmap

PyTorch を使うプロジェクトでは、必要に応じて進捗を残す。

- [ ] Tensor の `shape` / `dtype` / `device`
- [ ] `Dataset` / `DataLoader`
- [ ] `nn.Module` と `forward`
- [ ] loss と metric の違い
- [ ] `autograd`
- [ ] optimizer / scheduler
- [ ] train / eval loop
- [ ] checkpoint 保存と復元
- [ ] GPU / mixed precision
- [ ] profiling / bottleneck analysis

## Learned

### {{YYYY-MM-DD}}: {{学んだ概念}}

{{何を理解したかを 1〜3 行で書く。}}

```{{language}}
{{small_code_example}}
```

- Used in: `{{src/...}}`
- Related: `{{issue / PR / docs/...}}`

Explain-back:

- 入出力: {{...}}
- どこで使うか: {{...}}
- よくあるミス: {{...}}
- 次に自分で書けそうな範囲: {{...}}

## Review later

- {{復習したい概念}}
