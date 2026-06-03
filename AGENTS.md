# AGENTS.md — AI Agent Guide

AI コーディングエージェント（Claude Code / Codex 等）向けの作業ルール。
人間向けの概要は `README.md`、Git ルールは `CONTRIBUTING.md` を参照する。

## Purpose

このテンプレートは、研究・実装・学習・Git 操作を小さく再開しやすく保つためのもの。
説明は短くし、必要な要点と例を残す。

## Read first

作業前に、必要な範囲だけ読む。

1. `README.md` — プロジェクト概要と Markdown の役割
2. `STATUS.md` — 現在の状態
3. `PLANS.md` — これから行う作業
4. `MEMORY.md` — 確定した前提・決定・落とし穴
5. 関連する `docs/*` — 理論、実験、設計、用語

すべての Markdown を毎回読む必要はない。

## Core rules

- 変更は小さく、レビューしやすくする。
- 複数ファイルにまたがる変更では、先に短い方針を示す。
- 既存の命名、構成、文体を尊重する。
- 賢い実装より、読みやすい実装を優先する。
- 挙動、理論、使い方、設計が変わったら関連 Markdown を更新する。
- API キー、認証情報、個人情報、未公開データを Markdown やコードに書かない。

## Human review required

次の変更は、人間の確認なしに確定しない。

- 数式、理論、研究上の前提
- 実験プロトコル、評価指標、データ形式
- アーキテクチャ、公開 API、ディレクトリ構成
- 新規依存ライブラリの追加
- 破壊的変更
- `MEMORY.md` に書かれた重要な前提の変更
- Git ルールや Markdown の役割分担の変更

## Collaboration modes

タスク開始時に、必要なら `PLANS.md` で協働モードを選ぶ。

| Mode | 人間の役割 | AI の役割 | 適する作業 |
|------|------------|-----------|------------|
| `Human Driver` | 設計・実装の主担当 | ヒント、レビュー、テスト案 | 学びたい文法、PyTorch 基本、研究アルゴリズム |
| `Pair Programming` | 方針決定と主要実装 | 小さい実装案、レビュー、代替案 | 通常の研究コード開発 |
| `AI Draft → Human Rewrite` | 読解、修正、採否判断 | たたき台作成 | 定型処理、CLI、設定、ログ、テスト雛形 |
| `AI Delegate` | 仕様と検証の確認 | 実装の大部分 | GPU 高速化、CI、互換性対応、退屈なリファクタ |

迷ったら `Pair Programming` を選ぶ。
学習したい箇所は `Human Driver` に寄せる。

## Design alternatives

非自明な設計判断では、AI は実装前に代替案を出す。

- 原則として 2〜5 案を提示する。
- 重い設計、構造変更、デザインパターン採用では最大 5 案まで出す。
- 軽い判断では 2〜3 案でよい。
- 各案には、概要、長所、短所、学習価値を 1〜3 行で添える。
- 最終決定は人間が行い、採用理由を `PLANS.md`、`MEMORY.md`、または ADR に残す。

## Planning

軽微な修正なら `PLANS.md` は不要。
次の場合は、着手前に `PLANS.md` に短い計画を書く。

- 複数ファイルにまたがる
- 新機能を追加する
- 大きめのリファクタを行う
- 数式やアルゴリズムを実装する
- 実験条件を変更する
- 人間が学びたい実装概念を含む

計画は長くしない。目的、協働モード、手順、確認方法が分かればよい。

## Coding and learning

このリポジトリでは、実装とコーディング学習を同時に扱う。

- 非自明なコードには、選択理由を 1〜3 文で添える。
- コメントは「何をしているか」ではなく「なぜそうするか」を書く。
- 学習に有用な概念が出たら、`docs/LEARNING.md` に短く残す。
- `docs/LEARNING.md` には、長い引用ではなく、自分の言葉で要点と小さなコード例を書く。
- AI が生成した主要コードは、人間が入出力、責務、変更方法を説明できる状態にする。

### Learning-first areas

次の領域では、AI はいきなり完成実装を出さない。
まず設計、最小例、ヒント、テスト方針を提示し、人間が書く余地を残す。

- PyTorch の `Dataset`, `DataLoader`, `nn.Module`, training loop
- Python の基本設計、型、例外、ファイル I/O
- 研究アルゴリズムの中核処理
- データ構造の選定
- 評価指標、loss、前処理の設計
- デザインパターンの採否判断

AI が出してよいもの：

- 最小例
- 疑似コード
- テスト案
- レビューコメント
- 代替設計案
- バグの原因説明

AI が避けるもの：

- いきなり全実装を完成させる
- 人間が理解していない抽象化を導入する
- 「一般的にはこう」として設計を確定する

例：

````md
### 2026-05-31: pathlib

`Path` を使うと、OS に依存しにくいパス操作ができる。

```python
from pathlib import Path

file_path = Path("data") / "input.csv"
```
````

## Markdown update rules

- `STATUS.md` は現在の状態を書く。
- `PLANS.md` は未来の作業を書く。
- `MEMORY.md` は今後も参照する確定情報を書く。
- `docs/LEARNING.md` は学習した実装概念を書く。
- `docs/THEORY.md` は数式、理論、アルゴリズムを書く。
- `docs/EXPERIMENTS.md` は実験条件、結果、考察を書く。
- `docs/ARCHITECTURE.md` はモジュール構成と依存関係を書く。

迷ったら、`README.md` の Documentation Map に従う。

## Git workflow

Git の詳細ルールは `CONTRIBUTING.md` に集約する。

基本手順：

1. `main` から作業ブランチを作る。
2. 小さく変更する。
3. 必要な検証を行う。
4. 関連 Markdown を更新する。
5. 小さく焦点を絞ったコミットを作る。
6. PR を開く。

## Verification

完了報告前に、可能な範囲で確認する。

```bash
{{make format}}
{{make lint}}
{{make typecheck}}
{{make test}}
```

ドキュメントのみの変更では、上記を省略してよい。
その場合は、PR に「docs only」と書く。

## Done criteria

作業完了の条件：

- 変更の目的が達成されている
- 変更範囲が小さく保たれている
- 必要な検証を行っている
- 関連 Markdown を更新している
- AI / 人間の担当範囲が分かる
- 残課題があれば `STATUS.md` または PR に書いている

## Project structure example

```text
.
├── AGENTS.md            # AI 向け作業ルール
├── CLAUDE.md            # Claude Code 用。AGENTS.md を参照
├── README.md            # 人間向け入口
├── CONTRIBUTING.md      # Git、ブランチ、コミット、PR のルール
├── PLANS.md             # これから行う作業計画
├── STATUS.md            # 現在の状態
├── MEMORY.md            # 確定した前提・決定・落とし穴
├── docs/
│   ├── LEARNING.md      # コーディング学習ログ
│   ├── ARCHITECTURE.md  # 実装構成・依存関係
│   ├── THEORY.md        # 数式・理論
│   ├── GLOSSARY.md      # 用語集
│   ├── EXPERIMENTS.md   # 実験ログ
│   └── adr/             # 重要な設計判断
├── src/{{package}}/
├── experiments/
└── tests/
```
