---
tags:
  - 01_チートシート
---

# VScode のメモ {ignore=true}

【Table Of Contents】

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [VScode のメモ {ignore=true}](#vscode-のメモ-ignoretrue)
  - [ショートカット](#ショートカット)
  - [コマンド](#コマンド)
  - [VS code で正規表現を使って置換](#vs-code-で正規表現を使って置換)
  - [VScode で引数を渡してデバッグする](#vscode-で引数を渡してデバッグする)

<!-- /code_chunk_output -->

## ショートカット

| 説明                                    | ショートカットキー     |
| --------------------------------------- | ---------------------- |
| コマンドパレット                        | F1 または Ctrl+Shift+P |
| view の拡大/縮小                        | Ctrl + / Ctrl -        |
| エクスプローラを表示                    | Ctrl+Shift+E           |
| 関数の説明（パラメーター ヒント）を表示 | Ctrl+Shift+Space       |
| 入力候補                                | Ctrl+Space             |
| コード整形ツール(Fomatter)              | Shift + Alt + F        |
| bookmark                                | Alt+Ctrl+K             |
| Excel to Markdown table                 | Shift+Alt+V            |
| タブの選択                              | Ctrl + Tab             |
| マルチカーソル (1 件づつ選択)           | Ctrl + D               |
| マルチカーソル (1 件飛ばす）            | Ctrl + K -> Ctrl + D   |

## コマンド

| 説明                                 | コマンド                             |
| ------------------------------------ | ------------------------------------ |
| 目次（TOC ：table of contents)を追加 | Markdown Preview Enhanced Create TOC |

## VS code で正規表現を使って置換

print("任意の文字列")が print("任意の文字列これを足します")に変わります。便利！

- 検索文字列　 `print\("(.\*)"\)`
- 置換　　　　 `print("\$1 これを足します")`

## VScode で引数を渡してデバッグする

.vscode\launch.json の中に"args":["arg1", "arg2"]を追加する。これで、"arg1", "arg2"が引数として渡される。上記設定の上、uke.py を実行すると、"arg1", "arg2"がプリント出力される

```json
{
  // IntelliSense を使用して利用可能な属性を学べます。
  // 既存の属性の説明をホバーして表示します。
  // 詳細情報は次を確認してください: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "args": ["arg1", "arg2"]
    }
  ]
}
```

```py
import sys

param = sys.argv

print(param[1])
print(param[2])
```
