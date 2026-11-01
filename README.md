# 『Pokémon Champions』大会分析論文（LuaLaTeX／2段組み）

本文は[こちら](main.pdf)

## ディレクトリ構成

このフォルダをそのまま **VS Code の「フォルダーを開く」** で開いてください。`main.tex` が論文本文、`.vscode/settings.json` がビルド設定です。

## 初回セットアップ（Windows 11）

1. **TeX Live** をインストールします。公式の Windows 用インストーラー: https://tug.org/texlive/windows.html 。日本語組版が必要なため、`LuaLaTeX`、`latexmk`、`luatexja`、`ltjsclasses` を含む構成（TeX Live の標準的なフルインストールが確実）にします。
2. VS Code に **LaTeX Workshop** 拡張機能（`James-Yu.latex-workshop`）をインストールします。フォルダーを開くと推奨拡張機能として表示されます。
3. VS Code を再起動し、ターミナルで `lualatex --version` と `latexmk -v` を実行してコマンドが見つかることを確認します。
4. `main.tex` を開き、保存（`Ctrl + S`）します。成功すると **`build/main.pdf`** が作成されます。PDF は LaTeX Workshop のビューアで表示できます。自動ビルドが動かない場合は VS Code のコマンドパレットで `LaTeX Workshop: Build LaTeX project` を選択します。

## 編集箇所

- **著者・所属**: `main.tex` 冒頭の `\PaperAuthor` と `\PaperAffiliation` を変更します。
- **本文**: `\section{...}`、`\subsection{...}` の下を編集します。段落冒頭は、`\parindent=\zw` により全角1文字分の自動字下げが設定されています。ソースには手動の全角スペースを入れず、LaTeXが自動的に全角1文字分を字下げします。
- **パーティ画像**: `figures/party.png` というファイル名で画像を置くと、自動で図1に挿入されます。ファイルがない場合でも、画像用の枠が表示され、PDFをコンパイルできます。
- **2段組み**: `\twocolumn[...]` で表題と要旨を幅いっぱいに配置した後、本文を2段組みにしています。段間は `\columnsep=8mm` です。

## ターミナルからのビルド（必要な場合）

```powershell
latexmk -lualatex -interaction=nonstopmode -file-line-error -outdir=build main.tex
```

- `build/main.pdf`: 出力される論文PDF
- `build/`: LaTeX の補助ファイルもここにまとまります。

節・図表・参考文献の番号は補助ファイルを使って解決するため、LaTeXを1回だけ実行すると `??` や `[?]` が残る場合があります。本プロジェクトでは、冒頭の `% !TeX program = lualatex` による単発実行よりワークスペースのレシピを優先し、`latexmk` が必要な回数だけ再実行する設定にしています。通常の確認には `build/main.pdf` を開いてください。

※拡張機能は編集・表示・ビルド操作を担当し、実際のコンパイルは TeX Live の `latexmk` → `lualatex` が行います。VS Code の拡張機能のみではビルドできません。
