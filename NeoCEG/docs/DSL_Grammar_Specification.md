# NeoCEG DSL Grammar Specification v1.0

**Status**: Finalized (2026-02-08)
**Language**: English (primary) / 日本語 (説明)

---

## Overview / 概要

This document defines the formal grammar for the NeoCEG DSL (Domain-Specific Language) used to describe cause-effect graphs.

本ドキュメントは、NeoCEG DSL（原因結果グラフ記述言語）の正式文法を定義します。

### Key Features / 主要特徴

- **Human-readable syntax** / 人間可読な構文
- **Unicode support for node labels** (Japanese, etc.) / ノードラベルのUnicode対応（日本語等）
- **English-only keywords** / キーワードは英語のみ
- **Optional layout information** / レイアウト情報はオプション

---

## EBNF Grammar / EBNF文法

```ebnf
(* NeoCEG DSL Grammar v1.0 *)

(* ============================================================================= *)
(* Top-level structure / 最上位構造 *)
(* ============================================================================= *)

program         = { statement } ;

statement       = comment
                | node_definition
                | constraint_stmt
                | layout_stmt ;

comment         = "#" text newline ;

(* ============================================================================= *)
(* Node definitions / ノード定義 *)
(* ============================================================================= *)

(* Cause node: identifier : "label" [unobservable] *)
(* Effect/Intermediate node: identifier := expression *)
node_definition = identifier ( cause_def | effect_def ) ;

cause_def       = ":" string [ observable_flag ] ;
effect_def      = ":=" expression ;

observable_flag = "[unobservable]" | "[observable]" ;  (* [observable] accepted for backward compatibility *)

(* ============================================================================= *)
(* Logical expressions / 論理式 *)
(* ============================================================================= *)

expression      = or_expr ;

or_expr         = and_expr { "OR" and_expr } ;

and_expr        = unary_expr { "AND" unary_expr } ;

unary_expr      = [ "NOT" ] primary_expr ;

primary_expr    = identifier
                | "(" expression ")" ;

(* ============================================================================= *)
(* Constraints / 制約 *)
(* ============================================================================= *)

constraint_stmt = symmetric_constraint
                | directional_constraint ;

(* Symmetric constraints: ONE, EXCL, INCL *)
symmetric_constraint = ( "ONE" | "EXCL" | "INCL" )
                       "(" member_list ")" ;

(* Directional constraints: REQ, MASK *)
(* REQ: NOT on source or targets, but not both simultaneously *)
(* MASK: NOT on trigger only, targets always positive *)
req_constraint  = "REQ" "(" constraint_member "->" member_list ")" ;
mask_constraint = "MASK" "(" constraint_member "->" identifier_list ")" ;
directional_constraint = req_constraint | mask_constraint ;

identifier_list = identifier { "," identifier } ;

member_list     = constraint_member { "," constraint_member } ;

constraint_member = [ "NOT" ] identifier ;

(* ============================================================================= *)
(* Layout section (optional) / レイアウトセクション（オプション） *)
(* ============================================================================= *)

layout_stmt     = "@layout" "{" { layout_entry } "}" ;

layout_entry    = identifier ":" "(" number "," number [ "," number ] ")" ;
                  (* x, y, optional width / x座標, y座標, 省略可能な幅 *)

(* ============================================================================= *)
(* Lexical elements / 字句要素 *)
(* ============================================================================= *)

identifier      = ( letter | unicode_letter ) { letter | digit | "_" | unicode_letter } ;

string          = '"' { string_char | escape_sequence } '"' ;

string_char     = (* any character except " and \ *) ;

escape_sequence = "\" ( "n" | '"' | "\" ) ;

number          = [ "-" ] digit { digit } ;

letter          = "a" - "z" | "A" - "Z" ;

digit           = "0" - "9" ;

unicode_letter  = (* Unicode letters: Hiragana, Katakana, Kanji, etc. *)
                  (* Ranges: U+3040-U+309F, U+30A0-U+30FF, U+4E00-U+9FFF *) ;

text            = (* any character until end of line *) ;

newline         = "\n" | "\r\n" ;
```

---

## Semantic Rules / 意味規則

### Node Roles / ノードの役割

Node roles are **derived from graph structure**, not explicitly specified:

ノードの役割はグラフ構造から**自動判定**され、明示的に指定しません：

| Role / 役割 | Definition / 定義 | DSL Syntax / DSL構文 |
|------------|------------------|---------------------|
| **Cause** / 原因 | No incoming edges (in-degree = 0) / 入力辺なし | `name: "label"` |
| **Effect** / 結果 | No outgoing edges (out-degree = 0) / 出力辺なし | `name := expression` |
| **Intermediate** / 中間 | Has both incoming and outgoing edges / 入出力辺あり | `name := expression` |

### Keywords / キーワード

All keywords are **case-insensitive** but conventionally written in **UPPERCASE**.

キーワードは**大文字小文字を区別しない**が、慣例的に**大文字**で記述します。

| Keyword / キーワード | Purpose / 用途 |
|---------------------|---------------|
| `AND` | Logical conjunction / 論理積 |
| `OR` | Logical disjunction / 論理和 |
| `NOT` | Logical negation / 否定 |
| `ONE` | Exactly-one constraint / 排他的選択制約 |
| `EXCL` | Exclusive constraint / 排他制約 |
| `INCL` | Inclusive constraint / 包含制約 |
| `REQ` | Requires constraint / 要求制約 |
| `MASK` | Masking constraint / マスク制約 |

### Operator Precedence / 演算子優先順位

| Priority / 優先度 | Operator / 演算子 | Associativity / 結合性 |
|------------------|------------------|----------------------|
| 1 (highest) | `NOT` | Right / 右結合 |
| 2 | `AND` | Left / 左結合 |
| 3 (lowest) | `OR` | Left / 左結合 |

### Observable Flag / 観測可能フラグ

- Default: **ON** for all nodes (all nodes are observable by default)
- デフォルト: すべてのノードで**ON**（デフォルトで観測可能）
- `[unobservable]` marks a node as non-observable / `[unobservable]` で非観測可能を指定
- `[observable]` is accepted for backward compatibility (equivalent to default) / `[observable]` は後方互換のため受け入れる（デフォルトと同等）
- Can be toggled in the UI or specified in DSL / UIでトグル可能、またはDSLで指定可能

---

## Example / 使用例

### Basic Example / 基本例

```
# Login feature test design
# ログイン機能のテスト設計

# Causes (inputs)
valid_user_id: "Valid user ID entered"
password_match: "Password matches"
sso_enabled: "SSO is enabled"

# Intermediate nodes
auth_success := valid_user_id AND password_match
sso_auth := sso_enabled AND valid_user_id

# Effects (outputs)
login_result := auth_success OR sso_auth
error_display := NOT auth_success AND NOT sso_auth

# Constraints
ONE(auth_success, sso_auth)
REQ(sso_auth -> sso_enabled)
```

### With Layout / レイアウト付き

```
# Same as above...

# Layout coordinates (optional, width is optional third value)
@layout {
  valid_user_id: (100, 100)
  password_match: (100, 200)
  sso_enabled: (100, 300)
  auth_success: (300, 150, 200)
  sso_auth: (300, 300)
  login_result: (500, 200)
  error_display: (500, 300, 250)
}
```

### Japanese Labels / 日本語ラベル

```
# 日本語ノード名の例

# 原因（入力）
ユーザーID正常: "有効なユーザーIDが入力された"
パスワード一致: "パスワードが一致する"

# 結果（出力）
認証成功 := ユーザーID正常 AND パスワード一致
エラー表示 := NOT 認証成功

# 制約
EXCL(認証成功, エラー表示)
```

---

## Constraints Semantics / 制約の意味

### ONE - Exactly One / 排他的選択制約

Exactly **one** of the members must be true.
メンバーのうち**ちょうど1つ**が真でなければならない。

```
ONE(A, B, C)
```

### EXCL - Exclusive / 排他制約

**At most one** of the members can be true (zero is allowed).
メンバーのうち**最大1つ**が真（0個も可）。

```
EXCL(A, B, C)
```

### INCL - Inclusive / 包含制約

**At least one** of the members must be true.
メンバーのうち**少なくとも1つ**が真でなければならない。

```
INCL(A, B, C)
```

### REQ - Requires / 要求制約

If **source** is satisfied, then **all targets** must satisfy their conditions.
**source**が成立するなら、**すべてのtarget**がその条件を満たさなければならない。

NOT is allowed on the **source side or target side, but not both simultaneously**.
NOTは**ソース側またはターゲット側のいずれか一方のみ**許可。両側同時のNOTは禁止。

> **Why both-sides-NOT is prohibited / 両側NOTを禁止する理由**:
> `REQ(NOT A -> NOT B)` appears to mean "if A=F then B=F", but the double negation makes the intent ambiguous and error-prone.
> This is explicitly prohibited to prevent misunderstanding.
> `REQ(NOT A -> NOT B)` は「A=Fならば B=F」という意味に見えるが、二重否定は意図が曖昧でエラーを招きやすい。
> 誤解防止のため明示的に禁止する。

- `REQ(A -> B, C)` — If A=T then B=T and C=T
- `REQ(NOT A -> B)` — If A=F then B=T
- `REQ(A -> NOT B)` — If A=T then B=F

```
REQ(A -> B, C)        # If A=T then B and C must be T
REQ(NOT A -> B)       # If A=F then B must be T
REQ(A -> NOT B)       # If A=T then B must be F
```

### MASK - Masking / マスク制約

If **trigger** is true, then **all targets** become don't-care (M).
**trigger**が真なら、**すべてのtarget**がdon't-care（M）になる。

> **Note / 注**: NOT is allowed on trigger (left of `->`) only. NOT is prohibited on targets (right of `->`).
> NOTはトリガー（`->`の左側）のみ許可。ターゲット（`->`の右側）のNOTは禁止。
>
> **Why target NOT is prohibited / ターゲットNOTを禁止する理由**:
> The M (Don't Care) value is symmetric under negation — NOT M = M.
> Therefore, `MASK(A -> NOT B)` would have the same effect as `MASK(A -> B)`, making target NOT meaningless.
> M値は否定に対して対称（NOT M = M）であるため、`MASK(A -> NOT B)` は `MASK(A -> B)` と同じ効果になり、ターゲットNOTは無意味。
>
> **REQ vs MASK asymmetry in NOT handling / REQとMASKのNOT処理の非対称性**:
> This contrasts with REQ, where target NOT IS meaningful because REQ sets T/F values:
> これはREQと対照的で、REQはT/F値を設定するためターゲットNOTは意味がある：
> - `REQ(A -> B)`: A=T → B=**T**
> - `REQ(A -> NOT B)`: A=T → B=**F** (different result / 異なる結果)
> - `MASK(A -> B)`: A=T → B=**M**
> - `MASK(A -> NOT B)`: A=T → B=**M** (same result — NOT M = M / 同じ結果)

```
MASK(A -> B, C)       # If A=T then B=M and C=M
MASK(NOT A -> B, C)   # If A=F then B=M and C=M
```

---

## Compatibility / 互換性

### Not Compatible with CEGTest 1.6 CSV / CEGTest 1.6 CSVとの非互換性

This DSL format is **NOT compatible** with CEGTest 1.6's CSV format.

このDSL形式はCEGTest 1.6のCSV形式と**互換性がありません**。

**Design Decision**: Prioritize human-readability and AI tool integration over legacy compatibility.

**設計判断**: レガシー互換性よりも人間可読性とAIツール連携を優先。

---

## Document History / ドキュメント履歴

| Date / 日付 | Version / バージョン | Changes / 変更内容 |
|------------|---------------------|------------------|
| 2026-02-08 | 1.0 | Initial finalized version / 初版確定版 |
| 2026-03-01 | 1.1 | Invert observable flag: `[unobservable]` replaces `[observable]` (backward compat kept) / observable反転：`[unobservable]`に変更（`[observable]`は後方互換維持） |
| 2026-03-04 | 1.2 | Add optional width to layout entry: `(x, y, width)` — backward compatible / レイアウトエントリに省略可能な幅を追加：`(x, y, width)` — 後方互換 |
