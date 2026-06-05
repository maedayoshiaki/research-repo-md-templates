# TEMPLATE_GUIDE — このドキュメント群の使い方

雛形そのものの取扱説明書。仕組みを理解したら**削除して構わない**。
各テンプレートの `{{...}}` `<!-- TODO -->` を自分のプロジェクトの値で埋めて使う。

---

## 1. 設計思想（なぜこの構成か）

生成 AI（Claude Code / Codex 等）に丸投げせず、**開発者が主導権を握りながら効率を上げる**ことを目的に設計している。
Markdown ファイルは増やしすぎず、役割を分けて短く保つ。

3 原則がある。

1. **Human-in-the-Loop（人間が主導）** — 設計判断・数式・破壊的変更は人間が最終決定する。AI は「実装・検証・別解提示」の伴走者であり、独断で確定しない。
2. **教育的であること** — AI は「なぜそうするか」を簡潔に説明する。学んだ実装概念は `docs/LEARNING.md` に短く残す。
3. **小さく保つこと** — 変更、コミット、PR、Markdown の説明を小さくし、後から再開しやすくする。

この原則は `AGENTS.md` に明文化され、AI が毎回読む契約になる。

---

## 2. 最初に選ぶ: Human Involvement Profile

このテンプレートを使い始めるとき、まず `AGENTS.md` の `Repository Human Involvement Profile` を 1 つ選ぶ。
これは「このリポジトリでは、人間がどの程度コードに関わるか」を決める上位方針である。

| Profile | 目的 | 人間の実装量 | AI への委任 |
|---|---|---:|---:|
| `L0 Speed First` | 最速で動かす | なし | 最大 |
| `L1 Review Gate` | AI 実装を人間が読む | 少 | 大 |
| `L2 Selective Human Slots` | 速度と学習の両立 | 中 | 中 |
| `L3 Learning First` | 学習重視 | 多 | 補助 |
| `L4 Human Driver` | 人間が主担当 | 最大 | 最小 |

おすすめ：

- 迷ったら `L2 Selective Human Slots`
- 研究補助スクリプトや短期検証は `L0` / `L1`
- 研究アルゴリズムや設計パターンを学びたい場合は `L3`
- コーディング訓練が主目的なら `L4`

選んだ後にやること：

1. `AGENTS.md` の `Selected Profile` を埋める。
2. 選ばなかった Profile の詳細説明を削除する。
3. `PLANS.md` の `Repository Profile` 欄に同じ Profile を書く。
4. 必要に応じて `docs/LEARNING.md` を残すか削除する。
5. PR テンプレートの Profile 欄を使って、PR ごとに準拠を確認する。

Profile はリポジトリの既定値であり、タスク単位で一時的に変えてよい。
ただし、人間の介入度を下げる場合は `PLANS.md` または PR に理由を書く。

---

## 3. ファイル一覧と役割

| ファイル | 役割（ひとことで） | 主な読者 | 更新頻度 |
|------|------|------|------|
| `AGENTS.md` | AI への作業ルール。Human Involvement Profile もここで選ぶ | AI（兼 人間） | 低〜中 |
| `CLAUDE.md` | `AGENTS.md` を参照（Claude Code 用の入口） | AI | 低 |
| `README.md` | 人間向けの入口。概要・クイックスタート・Markdown の役割表 | 人間 | 低 |
| `CONTRIBUTING.md` | Git、ブランチ、コミット、PR のルール | 人間 + AI | 低〜中 |
| `PLANS.md` | **これからやること**（タスクの設計図 / ExecPlan） | AI + 人間 | 高 |
| `STATUS.md` | **今この瞬間の状態**（ダッシュボード） | AI + 人間 | 高 |
| `MEMORY.md` | **確定した知識**（長期記憶・決定ログ・落とし穴） | AI + 人間 | 中 |
| `docs/LEARNING.md` | コーディング学習ログ。理解した概念と小さな例 | 人間 + AI | Profile による |
| `docs/ARCHITECTURE.md` | 設計思想。原則・アーキ様式・パターン集 | 人間 + AI | 低〜中 |
| `docs/THEORY.md` | 数学・理論。数式と導出（人間所有） | 人間（AI 補助） | 中 |
| `docs/GLOSSARY.md` | 用語集（和英・コード変数対応） | AI + 人間 | 低 |
| `docs/EXPERIMENTS.md` | 研究の実験ログ（再現性・結果・判断） | 人間 + AI | 高 |
| `docs/adr/` | 重い意思決定の正式記録（ADR） | 人間 | 低 |
| `DESIGN.md` | 見た目。UI を作る場合のみ | AI + 人間 | 低 |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR の定型フォーマット | 人間 | 低 |

---

## 4. 最重要：「記憶の 3 点セット」PLANS / STATUS / MEMORY の違い

最も混同しやすいので、時間軸で整理する。

```text
   過去 ← ───────────── 現在 ───────────── → 未来
  MEMORY.md           STATUS.md            PLANS.md
 （確定した知識）     （今の状態）         （設計図）
   長期記憶            ダッシュボード         これからやること
```

- **PLANS.md = 未来**: これから着手する作業の計画。「ゴール・手順・検討した代替案」を書く。完了したら要点を MEMORY へ昇格し、消す/アーカイブ。
- **STATUS.md = 現在**: 今この瞬間に「何が進行中／次は何／何で詰まっているか」。揮発的でよい。毎セッションの最初に読み、最後に更新。
- **MEMORY.md = 過去（確定）**: もう動かない事実・決定・落とし穴。「次に同じことで迷わないため」の長期記憶。AI は**上書きせず追記**。

> 迷ったら：**「明日の自分が読んで嬉しいか？」**。手順なら PLANS、状況なら STATUS、教訓なら MEMORY。

---

## 5. 規模別の採用ガイド（最初から全部入れない）

**小さく始めて、必要になったら足す**のが鉄則。

### 小規模（個人・短期・プロトタイプ）— まずこれだけ

`AGENTS.md` + `STATUS.md` + `MEMORY.md` + `CLAUDE.md`

> これだけで「AI が毎回文脈を忘れる」問題の大半が解消する。
> `AGENTS.md` では Human Involvement Profile だけは先に選ぶ。

### 学習も重視する場合 — 追加

`docs/LEARNING.md`

> 実装中に学んだ概念を、要点と小さなコード例だけで残す。
> `L0` / `L1` では削除または任意運用でもよい。

### 中規模（チーム・継続開発・研究本体）— さらに追加

`PLANS.md`（タスクが複数ステップになったら）+ `CONTRIBUTING.md`（Git ルールを固定したいなら）+ `docs/ARCHITECTURE.md`（設計判断が必要になったら）+ `docs/THEORY.md`（数式を扱うなら）

### 大規模（長期・多人数・公開）— さらに追加

`docs/GLOSSARY.md`（用語ゆれ防止）+ `docs/adr/`（重い決定の正式記録）+ `docs/EXPERIMENTS.md`（実験の体系管理）+ `DESIGN.md`（UI があれば）+ `.github/PULL_REQUEST_TEMPLATE.md`（レビュー文化の定着）

---

## 6. 命名・言語の規約

- ファイル名は `AGENTS.md` / `README.md` に合わせて**大文字**（`STATUS.md` 等）。
- 見出しは英語でも日本語でもよいが、同じファイル内では揃える。
- ExecPlan の living section（`Progress` 等）など、AI が探す目印の見出しは**英語のまま固定**。

---

## 7. 1 セッションの運用ループ

1. **読む**: `AGENTS.md`（規約）→ `STATUS.md`（今）→ 関係する `PLANS.md` / `docs/*`
2. **Profile 確認**: `AGENTS.md` の Human Involvement Profile を確認する。
3. **計画**: 複数ステップなら `PLANS.md` に短く計画を書く。
4. **実装**: 選んだ方針で実装。非自明なコードは理由を短く残す。
5. **検証**: テスト・型・lint を通す。研究なら数値の再現性も確認。
6. **記録**: `STATUS.md` を更新。確定した決定・教訓は `MEMORY.md` へ昇格。学習事項は Profile に応じて `docs/LEARNING.md` へ。

---

## 8. LLM への渡し方のコツ

- Claude Code は `CLAUDE.md` を、多くのツールはルート直下の `AGENTS.md` を自動で読む。**契約は AGENTS.md に集約**し、詳細は各 doc へのリンクで委譲する。
- 大きいファイルを全部読ませない。「まず STATUS と該当 PLAN を読んで」と促し、必要時だけ `docs/THEORY.md` 等を開かせる。
- コーディングエージェントが subagent を使える場合は、調査・レビュー・テスト失敗の切り分けなどに使ってよい。
- ただし、subagent は Profile や人間レビューを迂回するために使わない。最終方針の統合と PR 説明は main agent が責任を持つ。
- AI に書かせた `MEMORY.md` / `THEORY.md` は**人間がレビューしてから確定**。未確認のものは `（未確認）` と明記。
