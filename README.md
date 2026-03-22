# ACT-TeX — Arcaea共通テスト 問題作成用TeXソース

本リポジトリは，音楽ゲーム「Arcaea」を題材としたファンメイド試験
**「Arcaea共通テスト（ACT）」** の問題を作成するための LaTeX ソースコードを公開するものです。

> **注意：本プロジェクトは非公式のファン企画です。**
> Arcaea および関連する知的財産はすべて **Lowiro Limited** や **各権利者** に帰属します。
>
> **テンプレートは2027年度試験より適用します。**

---

## 目次

- [ACT-TeX — Arcaea共通テスト 問題作成用TeXソース](#act-tex--arcaea共通テスト-問題作成用texソース)
  - [目次](#目次)
  - [プロジェクト概要](#プロジェクト概要)
  - [リポジトリ構成](#リポジトリ構成)
  - [セットアップ](#セットアップ)
    - [必要環境](#必要環境)
    - [emathのインストール](#emathのインストール)
    - [コンパイル方法](#コンパイル方法)
  - [ライセンス](#ライセンス)
    - [試験問題（生成されるPDF）](#試験問題生成されるpdf)
    - [TeXソースコード（`.tex` ファイル等）](#texソースコードtex-ファイル等)
  - [注意事項](#注意事項)
  - [クレジット](#クレジット)
  - [連絡先](#連絡先)

---

## プロジェクト概要

**Arcaea共通テスト（ACT）** は，大学入学共通テストを模した形式で出題されるファンメイドの模擬試験です。
Arcaea という作品をより深く楽しむための思考体験を目的として，高校レベルの論理・統計・数理等を活用した問題を出題します。

- **主催者：** tzug（個人）
- **性質：** 非公式・非営利のファン企画
- **試験形式：** 選択式中心，Arcaea領域 / 文科領域 / 理科領域 に分類
- **公式サイト：** [https://akino1729.github.io/ACT/public/index.html](https://akino1729.github.io/ACT/public/index.html)
  （問題閲覧・受験フォームはこちらのサイトで）

本リポジトリの目的は，試験問題作成に使用した **TeXソースコードの公開・共有** です。
問題を直接解く場合は上記サイトをご利用ください。

---

## リポジトリ構成

```
ACT-TeX/
├── pre_2026/         # Arcaea共通テスト本試験初回のための運用テスト
├── main_2026/        # 2026年度 本試験
│   ├── question/     # 問題冊子
│   └── answer/       # 解答・解説冊子
├── template/         # 2027年度以降の問題作成テンプレート
│   ├── ACTXXXX_main.tex
│   ├── ACTXXXX_instruction.tex
│   ├── preamble.tex
│   ├── question/
│   │   ├── arcaea/
│   │   ├── arts/
│   │   └── science/
│   └── answer/
├── preamble.tex      # テンプレート共通プリアンブル
├── README.md
└── LICENSE
```

各ディレクトリ内の `.tex` ファイルが試験問題のソースです。

---

## セットアップ

### 必要環境

- **TeX Live 2024 以降**（upLaTeX + dvipdfmx 環境）
- **emath パッケージ**（別途インストールが必要です。下記参照）

### emathのインストール

`template/` 以降のソース（2027年度試験）は **emath パッケージ** を使用しています。
emath は TeX Live の標準配布に含まれていないため，以下の手順で手動インストールしてください。

> `main_2026/` 以前のソースは emath を使用していないため，このインストールは不要です。

**Windows（TeX Live）の場合**

1. [奥村晴彦氏のサイト](https://emath.e-cat.jp/) から `emath.zip` をダウンロードする
2. ダウンロードした `emath.zip` を解凍する
3. 解凍して得られた `emath` フォルダを以下のパスに配置する

   ```
   C:\texlive\texmf-local\tex\latex\emath\
   ```

   （`texmf-local` フォルダが存在しない場合は作成してください）

4. TeX Live のファイルデータベースを更新するため，コマンドプロンプトで以下を実行する

   ```
   mktexlsr
   ```

5. 動作確認として，コマンドプロンプトで以下を実行し，エラーが出なければ完了

   ```
   kpsewhich emath.sty
   ```

**macOS / Linux の場合**

`C:\texlive\texmf-local\` の代わりに，以下のパスに `emath` フォルダを配置してください。

```bash
$(kpsewhich -var-value TEXMFLOCAL)/tex/latex/emath/
```

配置後，同様に `mktexlsr`（または `sudo mktexlsr`）を実行してください。

### コンパイル方法

`latexmk` を使用することを推奨します。各ディレクトリに `.latexmkrc` は含まれていないため，
以下のコマンドで直接指定してコンパイルしてください。

```bash
cd template/
latexmk -uplatex -pdfdvi ACTXXXX_main.tex
```

または `uplatex` + `dvipdfmx` を手動で実行：

```bash
uplatex ACTXXXX_main.tex
dvipdfmx ACTXXXX_main.dvi
```

---

## ライセンス

本リポジトリのコンテンツは，**種別によってライセンスが異なります。**
詳細は [LICENSE](./LICENSE) ファイルを参照してください。

### 試験問題（生成されるPDF）

**著作権は tzug が保持します。**

以下の条件のもとで，個人・商業利用を問わず自由に利用・共有・改変できます。

| 事項 | 詳細 |
|------|------|
| 利用・共有 | 自由（営利目的を含む） |
| 改変 | 自由（改変した旨の明記が必要） |
| 出典表記 | **必須**（例：「Arcaea共通テスト」より） |
| 著作者の詐称 | **禁止** |

イメージとしては **CC BY 4.0** に近い条件です。

### TeXソースコード（`.tex` ファイル等）

**CC0（パブリックドメイン相当）** として提供します。

著作権を放棄しており，出典表記なしで自由に利用・改変・再配布・商業利用できます（問題文を除く）。

---

## 注意事項

- 本プロジェクトは **非公式のファン企画** であり，Lowiro Limited とは無関係です。
- 「Arcaea」の名称・ロゴ・楽曲・アートワーク等の知的財産権はすべて **Lowiro Limited** と **各権利者** に帰属します。
- 本試験問題は Arcaea の公式コンテンツを題材・参照していますが，公式の試験・資格等とは一切関係ありません。
- 本プロジェクトのライセンスは，Arcaea に関する諸権利者の権利を侵害する利用を許諾するものではありません。

---

## クレジット

[公式ウェブサイト](https://akino1729.github.io/ACT/public/index.html) に記載しています。

---

## 連絡先

ご意見・お問い合わせは，tzug(@tzug_c)のDMからお願いします。

- 本GitHub: [Akino1729/ACT-TeX](https://github.com/Akino1729/ACT-TeX)
- ウェブサイト: [https://akino1729.github.io/ACT/public/index.html](https://akino1729.github.io/ACT/public/index.html)

---
Copyright (c) 2026 tzug. Some rights reserved.