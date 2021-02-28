---
tags:
  - macbook
---

# macbook 使い方

⌘ = command
⌥ = option
⇧ = shifR
⌃ = control

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
