# LaTeX Template

九州産業大学理工学部下川研用の汎用LaTeXテンプレートです。研究ノート、レポート、実験記録など様々な用途に活用できる軽量で使いやすいテンプレートです。

## 🚀 主な機能

- **シンプルな構造**: jsarticleベースで軽量・高速
- **汎用性**: 研究ノート、レポート、実験記録に最適
- **自動PDF生成**: プルリクエスト時にPDFプレビューを自動作成
- **日本語完全対応**: uplatex + 日本語フォントで最適化
- **即座の利用**: 複雑な設定不要で即座に文書作成開始

## 📁 ファイル構成

```
├── main.tex           # メイン文書（jsarticle形式）
└── .github/workflows/ # 自動ビルド設定
```

## 🔧 使用方法

### 自動セットアップ（推奨）
[thesis-management-tools](https://github.com/smkwlab/thesis-management-tools)の自動セットアップスクリプトを使用：

#### 下川研学生向け
```bash
DOC_TYPE=latex /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/smkwlab/thesis-management-tools/main/create-repo/setup.sh)"
```

#### それ以外の皆さん向け
```bash
INDIVIDUAL_MODE=true DOC_TYPE=latex /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/smkwlab/thesis-management-tools/main/create-repo/setup.sh)"
```

**自動セットアップの特徴**:

**下川研学生向け**:
- 学籍番号・文書名の対話的入力
- リポジトリ名: `学籍番号-文書名` (例: `smkwlab/k21rs001-research-note`)

**それ以外の皆さん向け**:
- リポジトリ名: `文書名` (例: `my-paper`, `experiment-log`)

**共通機能**:
- リポジトリの自動作成と LaTeX環境の追加

### 手動セットアップ
1. このテンプレートから新しいリポジトリを作成
2. 下記手順で文書作成を開始

### 文書作成と編集

### 1. 文書編集
\`main.tex\` を編集して文書を作成：
- **直接編集**: mainブランチで直接編集可能
- **構造**: section/subsection でシンプルに整理
- **数式・図表**: 基本LaTeX機能をすぐに利用

### 2. PDF生成
- **自動生成**: プッシュ時に自動でPDFが生成
- **確認方法**: GitHub Actionsタブで状況確認
- **ダウンロード**: Artifactsから生成PDFを取得

### 3. ローカルビルド（オプション）
\`\`\`bash
# 日本語LaTeXでコンパイル
uplatex main.tex
dvipdfmx main.dvi

# または一括処理（設定済みの場合）
latexmk main.tex
\`\`\`

#### 基本的な文書構造
`main.tex` を編集して文書を作成：

```latex
\section{章タイトル}
本文の内容...

\subsection{節タイトル}
詳細な説明...

\subsubsection{項タイトル}  % 必要に応じて
さらに詳細な内容...
```

#### よく使用する要素

**数式**:
```latex
% インライン数式
テキスト中の数式: $E = mc^2$

% 独立した数式
\begin{equation}
(x - a)^2 + (y - b)^2 = r^2
\label{eq:circle}
\end{equation}

% 式番号なし
\begin{equation*}
\sum_{i=1}^{n} x_i = 0
\end{equation*}
```

**箇条書きと番号付きリスト**:
```latex
% 箇条書き
\begin{itemize}
\item 項目1
\item 項目2
  \begin{itemize}
  \item サブ項目
  \end{itemize}
\end{itemize}

% 番号付きリスト
\begin{enumerate}
\item 手順1
\item 手順2
\end{enumerate}
```

**図表の挿入**:
```latex
% 図の挿入
\begin{figure}[htbp]
\centering
\includegraphics[width=0.8\textwidth]{図ファイル名.pdf}
\caption{図のキャプション}
\label{fig:example}
\end{figure}

% 表の作成
\begin{table}[htbp]
\centering
\caption{表のキャプション}
\label{tab:example}
\begin{tabular}{|l|c|r|}
\hline
左寄せ & 中央 & 右寄せ \\
\hline
データ1 & データ2 & データ3 \\
\hline
\end{tabular}
\end{table}
```

### PDF生成とワークフロー

#### ローカルでのビルド
VS Code でファイル保存時に下記の latexmk が実行される
開発環境での確認用：

```bash
# latexmk使用（推奨）
latexmk main.tex


# uplatex使用（なんらかの理由で個別に実行したい場合）
uplatex main.tex
dvipdfmx main.dvi

## クリーンアップ
rm -f *.aux *.log *.dvi *.toc
```

#### 自動PDF生成
GitHub Actionsにより以下のタイミングで自動的にPDFが生成される。

**プルリクエスト時（プレビュー）**:
1. ブランチを作成して変更をコミット
2. プルリクエストを作成
3. 自動的にPDFが生成され、ActionsのArtifactsからダウンロード可能
4. レビュー・修正のサイクルが効率化

**mainブランチへのプッシュ時**:
- 自動的にPDFをビルドして検証
- エラーがある場合はActionsログで確認可能

**タグ作成時（正式リリース）**:
```bash
git tag v1.0.0
git push origin v1.0.0
```
- 自動的にGitHubリリースが作成
- 完成版PDFがリリースに添付
- バージョン管理された文書の保管


## 📋 適用シーンと選択指針

### このテンプレートが最適な用途
- **研究ノート**: 日々の研究記録やアイデア整理
- **実験記録**: 実験手順、結果、考察の詳細記録
- **技術レポート**: 調査・分析結果のまとめ
- **学習ノート**: 勉強内容の体系的な整理
- **個人文書**: 備忘録、プロトタイプ文書

### 利用モードの比較

| 項目 | 下川研学生向け | それ以外の皆さん向け（INDIVIDUAL_MODE） |
|------|-----------|------------------------------|
| **対象ユーザー** | 学生 | 教員・研究者・一般ユーザー |
| **学籍番号** | 必須 | 不要 |
| **リポジトリ名** | `k21rs001-research-note` | `research-note` |
| **作成先** | smkwlab組織 | 個人アカウント |
| **管理体制** | 組織管理下 | 個人管理 |
| **使用例** | 学生の課題・研究 | 教員の研究文書・個人プロジェクト |

## ⚙️ 環境詳細

### LaTeX エンジン
- **TeXLive 2025**: 最新の日本語LaTeX環境
- **uplatex**: Unicode対応の日本語文書処理エンジン
- **jsarticle**: 軽量で汎用的な日本語文書クラス

### 品質管理
- **textlint**: 日本語文章の自動校正
- **自動構文チェック**: LaTeX構文エラーの検出

### 自動化機能
- **依存関係更新**: TeXLive環境の自動更新チェック
- **PDF生成**: プッシュ時の自動ビルド
- **アーティファクト管理**: プレビュー版と正式版の自動管理

## 🔧 カスタマイズ

### 追加ファイルのビルド
`.github/workflows/latex-build.yml` の `files` パラメータを編集：

```yaml
files: main, custom1, custom2
```

デフォルトでは `main.tex` のみビルドされます。

### LaTeX オプション調整
同ファイル内の `latex_options` を調整：

```yaml
latex_options: -pdf -halt-on-error
```

## 🆘 トラブルシューティング

### コンパイルエラー
1. GitHub Actionsのログを確認
2. ローカル環境での構文チェック
3. 文字エンコーディング（UTF-8）の確認

### PDF生成されない
1. `.tex` ファイル名が `files` パラメータと一致しているか確認
2. ファイルの構文エラーがないか確認
3. GitHub Actionsの実行権限を確認

### 日本語文書の問題
1. 文字エンコーディングがUTF-8であることを確認
2. 必要なパッケージ（`\usepackage{...}`）の記述確認

## 📚 関連リンク

- [LaTeX環境構築ガイド](https://github.com/smkwlab/latex-environment)
- [論文執筆テンプレート](https://github.com/smkwlab/sotsuron-template)
- [下川研究室](https://shimokawa-lab.kyusan-u.ac.jp/)

## 📄 ライセンス

このテンプレートは研究・教育目的での利用を想定しています。
