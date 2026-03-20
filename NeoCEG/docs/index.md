---
description: "NeoCEG — a Cause-Effect Graph test design tool (ISO/IEC/IEEE 29119-4). Draw logic as a graph, auto-generate decision tables and coverage tables. Free, open-source PWA."
---

# NeoCEG Documentation / NeoCEG ドキュメント

**NeoCEG** is a test design tool based on the Cause-Effect Graphing technique, a method specified in ISO/IEC/IEEE 29119-4:2021.
Simply draw logical and constraint relationships as a graph, and NeoCEG automatically generates an optimized decision table and a coverage table for efficient test coverage review.

Graph modifications are easily made through the GUI, and changes are instantly reflected across the cause-effect graph, logical expression language, decision table, and coverage table — all updated reactively.
Beyond test design, it is effective for organizing, verifying, and reviewing logical and constraint relationships throughout all phases of development.

The logical expression language grammar is published as an [EBNF specification](DSL_Grammar_Specification.md). By providing this grammar to an AI assistant, you can ask it to generate cause-effect graphs from natural language requirements — bridging the gap between specifications and test design.

**NeoCEG** は原因結果グラフ技法（ISO/IEC/IEEE 29119-4:2021 に規定）に基づくテスト設計ツールです。
論理関係と制約関係をグラフとして描くだけで、最適化されたデシジョンテーブルとテストの網羅性を効率的に確認できるカバレッジ表を自動生成します。

グラフの修正はGUI上で簡単に行うことができ、その変更は瞬時に原因結果グラフ、論理式によるテキスト表現、デシジョンテーブル、カバレッジ表に反映されます（リアクティブ動作）。
テスト設計に限らず、開発のあらゆるフェーズで論理関係や制約関係の整理や確認、レビューに効果を発揮します。

論理式言語の文法は [EBNF仕様](DSL_Grammar_Specification.md) として公開されています。この文法をAIアシスタントに渡すことで、自然言語の要求仕様から原因結果グラフを生成させることができ、仕様とテスト設計の橋渡しが可能になります。

## Why Cause-Effect Graphing? / なぜ原因結果グラフ法か？

The Cause-Effect Graphing technique is known to reduce the number of test cases by an order of magnitude compared to exhaustive combinatorial decision tables. Fewer tests mean faster preparation, more efficient execution, and easier maintenance — but there is another significant advantage.

Because the technique eliminates infeasible test cases — combinations that cannot occur due to constraint relationships — the resulting test suite consists entirely of executable tests. This makes it exceptionally well-suited for embedding in DevOps workflows and CI/CD pipelines, where every test must be runnable without manual intervention or judgment calls about which cases to skip.

Furthermore, the generated decision table can be directly fed into data-driven testing frameworks, making it straightforward to automate the entire test execution process.

原因結果グラフ技法は、すべての組み合わせを列挙するデシジョンテーブルと比較して、テストケース数をオーダーレベルで削減することが知られています。テスト数の削減は、準備の効率化、実行時間の短縮、保守性の向上をもたらしますが、大きな利点はほかにもあります。

この技法は、制約関係により実行不可能なテストケース（あり得ない組み合わせ）を排除するため、生成されるテストスイートはすべて実行可能なテストで構成されます。これにより、手動での判断や実行不要なケースの選別が不要となり、DevOps ワークフローや CI/CD パイプラインへの組み込みに非常に適しています。

さらに、生成されたデシジョンテーブルをデータ駆動テストフレームワークに直接投入することで、テスト実行全体の自動化を容易に進めることができます。

## How This Tool Was Built, and How to Use It with Confidence / 本ツールの成り立ちと、安心して使うために

This project was developed through AI-assisted development using Claude Code (Anthropic), employing a specification-driven methodology: the human author conceived the requirements, designed the architecture, directed the development process, and exercised final judgment on verification and validity. The AI generated all source code and documentation under continuous human direction.

The fact that code was written by an AI does not, in itself, make the output less trustworthy — just as code written by a human is not inherently reliable without verification. What matters is the ability to verify the results. NeoCEG provides a Coverage Table — a feature not required by any standard — that enables users to efficiently review which logical conditions have been covered, which tests were adopted, and why. This transparency applies equally regardless of whether the implementation was produced by an AI or a human engineer.

This software is provided free of charge under the MIT License, which includes an explicit disclaimer of warranty. Users are encouraged to make full use of the Coverage Table for review and validation before incorporating generated results into their test designs.

本プロジェクトは、Claude Code（Anthropic）を用いたAI支援開発によって構築されました。仕様駆動開発の手法を採用し、著者が要求仕様の策定、アーキテクチャの設計、開発プロセスの指揮、および検証・妥当性確認における最終判断を行っています。ソースコードおよびドキュメントの全行は、著者の継続的な指示のもとAIが生成しました。

AIがコードを書いたという事実は、それ自体で成果物の信頼性を損なうものではありません——人間が書いたコードであっても、検証なしに信頼できるわけではないのと同じです。重要なのは、結果を検証できるかどうかです。NeoCEG は国際規格等が要求していないカバレッジ表を出力します。カバレッジ表により、どの論理条件がカバーされたか、どのテストが採用されたか、そしてその理由を効率的にレビューできます。この透明性は、実装がAIによるものであっても人間のエンジニアによるものであっても、等しく有効です。

本ソフトウェアは MIT ライセンスのもと無償で提供されており、同ライセンスに明記された免責条項が適用されます。生成結果をテスト設計に組み込む前に、カバレッジ表を十分に活用してレビュー・妥当性確認を行うことを推奨します。

## Acknowledgments / 謝辞

NeoCEG is not a port of any existing software, but a ground-up reimplementation. Nevertheless, it could not exist without the pioneering work that came before it.

This project owes a profound debt to **X-CEG**, developed by Dr. Koichi Akiyama (秋山浩一), and to **CEGTest**, developed by Masaki Kase (加瀬正樹). Their tools brought the Cause-Effect Graphing technique — long confined to textbook descriptions — into practical, usable form, and demonstrated that rigorous test design methods could be made accessible to working engineers. NeoCEG stands on the foundation they built.

The author wishes to express deep respect and gratitude to both Mr. Akiyama and Mr. Kase for their years of dedication and the results they have achieved.

Special thanks are due to Dr. Koichi Akiyama, who tested NeoCEG from an early stage of its development and provided valuable evaluation and feedback.

NeoCEG は既存ソフトウェアの移植ではなく、一から再実装したものです。しかしながら、先行するツールなくしては存在し得ないものです。

本プロジェクトは、秋山浩一氏が開発された **X-CEG**、および加瀬正樹氏が開発された **CEGTest** に多大な恩恵を受けています。両氏のツールは、長らく教科書上の記述にとどまっていた原因結果グラフ技法を実用的かつ使いやすい形に具現化し、厳密なテスト設計手法が現場のエンジニアにとって身近なものとなり得ることを示しました。NeoCEG は両氏が築かれた基盤の上に立っています。

秋山浩一氏と加瀬正樹氏の両名の長年の取り組みとその成果に、改めて深い敬意と感謝を表します。

とりわけ秋山浩一氏には、NeoCEG の開発初期から試用いただき、大変有益な評価やご意見を賜りました。深く感謝いたします。

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
