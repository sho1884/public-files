# NeoCEG Documentation / NeoCEG ドキュメント

**NeoCEG** is a modern reimplementation of CEGTest, a Cause-Effect Graph test design tool.
Built with React Flow for graph editing and TypeScript for type safety.

**NeoCEG** は CEGTest の現代的な再実装であり、原因結果グラフによるテスト設計ツールです。
グラフ編集に React Flow、型安全性に TypeScript を採用しています。

## Quick Links / リンク

- **[User Manual / ユーザーマニュアル](User_Manual.md)** - How to use NeoCEG / NeoCEG の使い方

## Try It / 試してみる

- **Application / アプリケーション**: [neo-ceg.vercel.app](https://neo-ceg.vercel.app/)
- **Source Code / ソースコード**: [github.com/sho1884/NeoCEG](https://github.com/sho1884/NeoCEG)

### Samples / サンプル

Click a link to open the sample directly in NeoCEG. / リンクをクリックすると NeoCEG でサンプルが開きます。

**Basic Logic / 基本ロジック:**

- [AND](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/AND.nceg) - AND gate
- [OR](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/OR.nceg) - OR gate
- [AND (4 inputs)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/AND4.nceg) - 4-input AND
- [OR (4 inputs)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/OR4.nceg) - 4-input OR
- [AND/OR Logic](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/AND_OR_Logic.nceg) - Combined AND/OR
- [AND/OR Program](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/AND_OR_Program.nceg) - Program logic example

**Constraints / 制約:**

- [ONE constraint (definition)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/One-constraint-definition.nceg)
- [ONE constraint (enforced)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/One-constraint-enforced.nceg)
- [AND4 + EXCL](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/AND4_EXCL.nceg)
- [OR4 + EXCL](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/OR4_EXCL.nceg)
- [REQ constraint (A->B, A->C)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Req-constraint-AB_AC.nceg)
- [REQ constraint (A->B, B->C)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Req-constraint-AB_BC.nceg)
- [REQ implication as rule (definition)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Req-implication_as_rule-definition.nceg)
- [REQ implication as rule (enforced)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Req-implication_as_rule-enforced.nceg)
- [REQ negative implication (enforced)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Req-negative_implication-enforced.nceg)
- [MASK constraint (A->B, A->C)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Mask-constraint-AB_AC.nceg)
- [MASK constraint (A->B, C->B)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Mask-constraint-AB_CB.nceg)
- [MASK constraint (enforced)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Mask-constraint-enforced.nceg)
- [MASK negative implication (enforced)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Mask-negative_implication-enforced.nceg)
- [REQ vs MASK comparison (Req)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/reciprocal_comparison-Req_constraint.nceg)
- [REQ vs MASK comparison (Mask)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/reciprocal_comparison-Mask_constraint.nceg)

**Real-world Examples / 実践例:**

- [Admission Fee / 入場料金 (JA)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Admissionfee_jp.nceg)
- [Admission Fee (EN)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Admissionfee_en.nceg)
- [Printer Print Options / プリンタ印刷設定 (JA)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/OneMask-printer_print_options_jp.nceg)
- [Printer Print Options (EN)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/OneMask-printer_print_options_en.nceg)
- [Copy/Paste Operation / コピー＆ペースト操作 (JA)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/ReqMask-copy_paste_operation_jp.nceg)
- [Copy/Paste Operation (EN)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/ReqMask-copy_paste_operation_en.nceg)
- [Windows Folder Option / Windowsフォルダオプション (JA)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Windows-Folder-Option.nceg)
- [Windows Folder Option (EN)](https://neo-ceg.vercel.app/?file=https://sho1884.github.io/public-files/NeoCEG/Samples/Windows-Folder-Option_en.nceg)

## Reference / 参考文献

- Myers, G.J., Badgett, T., Sandler, C. [*The Art of Software Testing*, 3rd Edition](https://www.oreilly.com/library/view/the-art-of/9781118133156/toc.html), Chapter 4
- [ISO/IEC/IEEE 29119-4:2021](https://www.iso.org/standard/79430.html) "Software and systems engineering — Software testing — Part 4: Test techniques"
- 秋山浩一 [『ソフトウェアテスト技法ドリル【第2版】』](https://www.juse-p.co.jp/products/view/934) 日科技連出版社 — Software Test Technique Drill, 2nd Edition
- 加瀬正樹 [CEGTest](http://softest.cocolog-nifty.com/blog/cegtest.html) — The original CEG test design tool
- sho1884 [ブールグラフでロジックを整理してデシジョンテーブルと条件式を自動生成する](https://note.com/sho1884/n/n4afa22873334) (note) — Organizing Logic with Boolean Graphs to Auto-Generate Decision Tables and Conditional Expressions
- sho1884 [ロジックとアーキテクチャの境界を設計する（その１）](https://note.com/sho1884/n/n372d4dbf49dc) (note) — Designing the Boundary Between Logic and Architecture (Part 1)
- sho1884 [原因結果グラフ法がテストを減らすときの「考え方」](https://qiita.com/sho1884/items/f2b3a887546e87bb734a) (Qiita) — The Concept Behind How Cause-Effect Graphing Reduces Tests
- sho1884 [原因結果グラフ法と MC/DC カバレッジ](https://qiita.com/sho1884/items/d8b34102e9eb47643866) (Qiita) — Cause-Effect Graphing and MC/DC Coverage
- sho1884 [原因結果グラフ法における制約関係のチートシート](https://qiita.com/sho1884/items/32f8d4d6454e48f1c33c) (Qiita) — Cheat Sheet for Constraints in Cause-Effect Graph Method
- sho1884 [原因結果グラフ法における制約関係解説（Require制約編）](https://qiita.com/sho1884/items/fc37f3953f4aeb061e60) (Qiita) — Constraint Relationships in CEG: Require Constraint
- sho1884 [原因結果グラフ法における制約関係解説（Mask制約編）](https://qiita.com/sho1884/items/f1b3668b2b134dddad4a) (Qiita) — Constraint Relationships in CEG: Mask Constraint
