---
description: "NeoCombi — a combinatorial test design tool. Author factors, levels, and PICT-compatible constraints; generate pairwise sets or full decision tables. Free, open-source PWA."
---

# NeoCombi Documentation / NeoCombi ドキュメント

**NeoCombi** is a combinatorial test design tool. You describe a problem space as
**factors** and their **levels**, rule out impossible combinations with
**constraints** written in a PICT-compatible DSL (a subset of PICT), and generate test cases two ways:
a compact **pairwise / N-wise** set (via Microsoft PICT) or a full **decision
table** (every combination, with the forbidden ones marked). Authoring, the
forbidden view, the coverage matrix, and decision-table generation all run in
your browser.

**NeoCombi** は組み合わせテスト設計ツールです。問題空間を**因子**と**水準**で表し、
あり得ない組み合わせを **PICT 互換の DSL** による**制約**で除外し、テストケースを2通りで
生成します ── コンパクトな**ペアワイズ / N-wise**（Microsoft PICT 経由）と、全組み合わせの
**デシジョンテーブル**（禁止行は印付き）。オーサリング・禁則ビュー・総当たり表・
デシジョンテーブル生成はブラウザ内で動きます。

[Try the demo / デモを試す](https://neo-combi.vercel.app/){ .md-button .md-button--primary }
[User Manual](User_Manual.md){ .md-button }
[Deployment Guide](Deployment_Guide.md){ .md-button }

## The app at a glance / 画面の全体像

![The NeoCombi screen with the shopping-site sample: the Coverage matrix cross-tabulates every factor pair (covered 138 / missed 0 / forbidden 26 — 100% pair coverage), with the factor & level editor below. / NeoCombi の画面（サンプル：ショッピングサイト）。全因子ペアを総当たりする総当たり表（covered 138／missed 0／forbidden 26＝ペア被覆 100%）と、下段の因子・水準エディタ。](assets/Screenshot_Coverage.png)

## A DSL you can use directly / そのまま使える DSL

NeoCombi's constraint DSL is a **strict subset of Microsoft PICT's** language,
published as a versioned [EBNF grammar (v1.0)](DSL_Grammar_Specification.md). Two
benefits follow:

- **It runs directly in PICT.** Whatever you write in NeoCombi is valid PICT
  input — paste it into the `pict` command-line tool and it works unchanged, and
  Microsoft's PICT documentation applies as-is.
- **It is easy to generate with an AI.** Hand the grammar (EBNF) together with
  your test problem to an AI assistant and ask it to write the DSL — bridging the
  gap between specifications and test design — then review and refine it in
  NeoCombi.

NeoCombi の制約 DSL は **Microsoft PICT 言語の厳密なサブセット**で、版番号付きの
[EBNF 文法（v1.0）](DSL_Grammar_Specification.md)として公開しています。利点は2つ：

- **そのまま PICT に直接入力できる。** ここで書いたものは PICT 入力として有効で、
  `pict` コマンドにそのまま貼って動きます。Microsoft の PICT ドキュメントもそのまま参照可。
- **AI で生成しやすい。** EBNF とテスト対象の説明を AI に渡して DSL を生成させ、仕様と
  テスト設計を橋渡しし、NeoCombi で確認・修正できます。

## Two generation strategies / 2つの生成方略

| | **Pairwise** / ペアワイズ | **Decision table** / デシジョンテーブル |
|---|---|---|
| Produces / 生成物 | a small set covering every pair / 全ペアを覆う小さな集合 | **every** combination / **全組み合わせ** |
| Forbidden rows / 禁止行 | excluded / 含まない | kept and marked `X` / 残して `X` 印 |
| Runs / 実行 | via a PICT service / PICT サービス経由 | in your browser / ブラウザ内 |
| Best for / 向く場面 | many factors / 因子が多い | few factors, exhaustive / 少因子・網羅 |

![The Forbidden view (shopping-site sample) sliced as 決済方法 × 支払回数: red X cells mark impossible pairs, and the decision table below keeps those rows and flags them in a FORBIDDEN column. / 禁則ビュー（ショッピングサイト例、決済方法 × 支払回数 のスライス）。赤い X が不可能なペア。下段のデシジョンテーブルは禁止行を残し FORBIDDEN 列で明示。](assets/Screenshot_Forbidden.png)

## Open a sample / サンプルを開く

Samples load via a `?file=<url>` parameter. Each content example is available in
both English and Japanese / 各例題は英語版・日本語版の両方があります:

- **Shopping site / ショッピング** — a mask level (`_MASK_`) + several constraints —
  [EN](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/shopping-en.ncombi) ·
  [JA](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/shopping.ncombi)
- **Multifunction printer / 複合機（とじしろ）** — binding-margin geometry: valid gutters depend on orientation × duplex —
  [EN](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/mfp-en.ncombi) ·
  [JA](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/mfp.ncombi)
- **Copier N-up & zoom / 複合機（N-up・倍率）** — when a hidden control needs a `_MASK_` level, and when a locked field is just a fixed value —
  [EN](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/mfp-zoom-en.ncombi) ·
  [JA](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/mfp-zoom.ncombi)
- **Admission fee / 入館料** — a decision table: inputs determine the fee, enforced by constraints (the fee is an expected-result factor) —
  [EN](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/admission-fee-en.ncombi) ·
  [JA](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/admission-fee.ncombi)
- **Browsers / ブラウザ** — small pairwise model —
  [EN](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/browsers.ncombi) ·
  [JA](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/browsers-ja.ncombi)
- **Scale fixtures** (synthetic, language-neutral / 言語非依存) —
  [50 factors](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/large-50.ncombi) ·
  [100 factors](https://neo-combi.vercel.app/?file=https://sho1884.github.io/public-files/NeoCombi/Samples/large-100.ncombi)

## Sibling tools / 姉妹ツール

NeoCombi has a sibling test-design tool,
[NeoCEG](https://github.com/sho1884/NeoCEG) (cause-effect graphs). Both are
deterministic converters with no embedded AI.
