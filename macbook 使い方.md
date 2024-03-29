---
tags:
  - macbook
---

# macbook 使い方

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=2 orderedList=false} -->

<!-- code_chunk_output -->

- [macbook 使い方](#macbook-使い方)
  - [環境変数の設定](#環境変数の設定)
  - [キーの対応表](#キーの対応表)
  - [finder](#finder)
    - [ファイルを移動させる(win の ctrl + v)](#ファイルを移動させるwin-の-ctrl--v)
    - [戻る、進む](#戻る進む)
  - [キー](#キー)
  - [ショートカット](#ショートカット)
  - [terminal](#terminal)
  - [git が使えなくなったとき](#git-が使えなくなったとき)
  - [zsh の注意！](#zsh-の注意)

<!-- /code_chunk_output -->

## 環境変数の設定

直接編集
`/Users/username/.zshrc`

## キーの対応表

⌘ = command
⌥ = option
⇧ = shifR
⌃ = control

## finder

### ファイルを移動させる(win の ctrl + v)

⌘Command+⌥Option+V

### 戻る、進む

Command+[ で戻る
Command+] で進む

## キー

| 一般          | macbook              |
| :------------ | :------------------- |
| Home キー     | command ＋ ←         |
| End キー      | command ＋ →         |
| PageUp キー   | command ＋ ↑         |
| PageDown キー | command ＋ ↓         |
| delete        | fn + delete or ⌃ + D |
| \             | √ + ¥                |

## ショートカット

| キー          | 効果                                  |
| :------------ | :------------------------------------ |
| ⌘ + M         | ウィンドウを Dock に格納              |
| ⌘ + Tab       | アプリ切り替え                        |
| ⌘ + ⇧ + 3     | スクリーンショット（全画面）          |
| ⌘ + ⇧ + 4     | スクリーンショット（範囲指定）        |
| ⌘ + ^ + F     | フルスクリーン オン/オフ              |
| ⌘ + Z         | もどる                                |
| ⌘ + ⇧ + Z     | 進む                                  |
| ⌘ + ⇧ + .     | finder で隠しファイルとフォルダを表示 |
| ⌘ + ⌥ + space | finder を起動                         |

## terminal

- finder を開く

```zsh
open ~ #home
open . #currenr dir
```

- vscode を開く

vscode でコマンドパレットを開き、shell と売って、パスをターミナルに登録する

```zsh
code ~ #home
code . #currenr dir
```

## git が使えなくなったとき

アプデすると、使えなくなる場合がある。そのときは、下記コマンドを実行すれば OK

```zsh
xcode-select --install
```

## zsh の注意！

pip を実行した再に、`zsh: 1.14.0 not found`が出る場合がある。これは予約語と干渉するためらしい。対策として、`pip install 'tensorflow==1.14.0'`のように ''で囲みましょう！
