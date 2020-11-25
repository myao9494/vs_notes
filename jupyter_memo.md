---
tags:
  - 01_チートシート
  - python
---

# 2020-11-21 jupyter_memo

## jupyter notebookのCSS、matplotlibのデフォルトファイルの設定

https://github.com/myao9494/jupyter_style_myao　の通り設定する

### extention のバーを表示したい場合

CSSの以下をコメントアウトすると、extentionのツールバーが表示される
　※操作する際はコマンドパレットで必要十分なので消してある

```css
div#maintoolbar {
  display: none !important;
}
```

## ショートカット

| ショートカットキー    | 説明                    |
|--------------|-----------------------|
| Ctrl-Shift-P | コマンドパレットを開く           |
| Shift-M      | セルのマージ(選択してないなら下のセルと) |
| L            | 行番号の表示・非表示            |
| Shift-L      | 全てのセルの行番号の表示・非表示      |
| O            | セルの出力結果の表示・非表示        |
| Shift-O      | 出力結果スクロール・非スクロール      |
| H            | キーボードショートカット表示        |
| Shift-Space  | 上にスクロール               |
| Space        | 下にスクロール               |

【編集モード】

| ショートカットキー      | 説明       |
|----------------|----------|
| Shift-Tab      | 関数の説明を出す |
| Ctrl-Left      | 一単語前に移動  |
| Ctrl-Right     | 一単語後に移動  |
| Ctrl-Backspace | 前の単語を削除  |
| Ctrl-Delete    | 後の単語を削除  |

## jupyter マジックコマンド

- %who : 宣言されている変数一覧の表示
- %whos : 宣言されている変数一覧の詳細表示(型と値)
- obj? : Object の型と値の表示
- %quickref : サポートされる Magic Command の一覧の表示
- %matplotlib inline : jupyter 内に表示させる