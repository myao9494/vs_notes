---
tags:
  - mac
---

# macbook_setup

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [macbook_setup](#macbook_setup)
  - [初期設定](#初期設定)
    - [コンピュータ名の変更](#コンピュータ名の変更)
    - [解像度の変更](#解像度の変更)
    - [Night Shift をオンにする](#night-shift-をオンにする)
  - [日本語入力関係](#日本語入力関係)
    - [google 日本語入力](#google-日本語入力)
  - [トラックパッドの設定](#トラックパッドの設定)
  - [fineer の設定](#fineer-の設定)
    - [表示](#表示)
    - [設定](#設定)
  - [バッテリーのパーセントを表示](#バッテリーのパーセントを表示)
  - [Dock の設定](#dock-の設定)
    - [表示位置](#表示位置)
  - [ファイアウォールをオ](#ファイアウォールをオ)
  - [git](#git)
    - [install](#install)
    - [git の初期設定](#git-の初期設定)
  - [VS code](#vs-code)
  - [anaconda](#anaconda)
  - [chrome](#chrome)
  - [homebrew](#homebrew)
    - [インストール](#インストール)
    - [zsh にパスを通す](#zsh-にパスを通す)
    - [brew で入れたソフトの場所](#brew-で入れたソフトの場所)
    - [brew でインストールしたもの](#brew-でインストールしたもの)
  - [ssh](#ssh)
    - [公開鍵の作成](#公開鍵の作成)
    - [公開鍵をサーバ側へ登録（ex github)](#公開鍵をサーバ側へ登録ex-github)
    - [config file の作成](#config-file-の作成)
  - [無料ソフト インストール](#無料ソフト-インストール)
    - [CheatSheet](#cheatsheet)
    - [Clipy](#clipy)
    - [Alfred](#alfred)
    - [AppCleaner](#appcleaner)

<!-- /code_chunk_output -->

## 初期設定

### コンピュータ名の変更

1. システム環境設定を開く
1. 共有をクリック
1. コンピュータ名を適宜変更する

### 解像度の変更

1. システム環境設定を開く
1. ディスプレイをクリック
1. 解像度の変更をクリック
1. スペースを拡大をクリック

### Night Shift をオンにする

1. システム環境設定を開く
1. ディスプレイをクリック
1. Night Shift をクリック
1. スケジュールで時間を入れるか、日の入りから日の出までにする

## 日本語入力関係

### google 日本語入力

https://www.google.co.jp/ime/　からダウンロード

1. 画面右上のあもしくは A をクリック
1. google を選択する
1. 環境設定をクリックして、入力補助の数字を半角に変更
1. スペースを半角に変更

## トラックパッドの設定

1. システム環境設定を開く
1. チェックできるところは全部チェックする
1. 軌跡の速さを調節する

## fineer の設定

### 表示

1. 何かフォルダを開く
1. 画面左上の Finder をクリック
1. 環境設定をクリック
1. 画面上のメニューから表示をクリック
1. ステータスバーを表示をクリック
1. パスバーを表示をクリック
1. サイドバーを表示
1. よく使うフォルダをサイドバーにドラッグ&ドロップして追加する

### 設定

1. Finder を開く
1. 画面左上の Finder をクリック
1. 環境設定をクリック
1. 歯車アイコンの詳細をクリック
1. 全てのファイル名拡張子を表示にチェックを入れる

## バッテリーのパーセントを表示

1. 画面右上のアップルマーク をクリック
1. システム環境設定をクリック
1. Dock とメニューバーをクリック
1. ウィンドウの左サイドバーを下にスライド
1. バッテリーをクリック
1. 割合（%）を表示にチェックを入れる

## Dock の設定

### 表示位置

1. 画面右上のアップルマーク をクリック
1. システム環境設定をクリック
1. Dock とメニューバーをクリック
1. 画面上の位置の右にチェックを入れる

## ファイアウォールをオ

1. システム環境設定を開く
1. ファイアウォールをクリック
1. ファイアウォールをオンにするをクリック

## git

### install

terminal で git と打つと、インストールできる。
OS アプデ後、`xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun`のエラーが出た場合は、下記のコマンドを実行する

```zsh
xcode-select --install
```

### git の初期設定

```zsh
git config --global user.name "First-name Family-name"
git config --global user.email "username@example.com"
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```

## VS code

m1 対応は insider しか無かったので、下記からインストール
現状、特に問題なし

https://code.visualstudio.com/insiders/#

## anaconda

m1 対応は無かったので、通常の intel mac 用を公式 HP からダウンロードしてインストール

## chrome

m1 用をインストール、問題なく快適

## homebrew

mac のパッケージ管理ソフト、これの他に macport がある。

### インストール

https://qiita.com/shira-shun/items/0f6213f4923cb5544367

mkdir でパスワードを聞かれるので、ログインパスワードを入れる
以下の場合は、usre にインストールする場合

```zsh
cd opt
mkdir homebrew
curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```

### zsh にパスを通す

`/Users/user/.zshrc`を開いて、下記を追加する

`export PATH=/Users/myao9494/opt/homebrew/bin:$PATH`

### brew で入れたソフトの場所

以下のコマンドで確認できる。homebrew のインストールフォルダに入っている模様

```zsh
brew ls パッケージ名
```

### brew でインストールしたもの

以下をインストールした。gym のため。これを入れないと gym が動かなっかたが、どうなのだろう。。。

```zsh
brew install cmake boost boost-python sdl2 swig wget
```

## ssh

github の clone ができなくなったので、ssh の設定をする。
win と同じ秘密鍵を使っても良いのかもだけれど、mac 用に設定することとする

### 公開鍵の作成

※GitHub に登録している Email アドレスを使うのが一般的のようです。

-t rsa というオプションは、RSA 暗号というタイプの暗号の鍵を生成

```zsh
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 公開鍵をサーバ側へ登録（ex github)

github の場合、複数の公開鍵を登録可能

1. id_rsa.pub を開く
1. d_rsa.pub の中の文字列 ssh-rsa〜xxxxx の終わりまでをコピーします。 （mail@mail.comは不要）
1. サーバ側へ登録
   github の場合、右上のアイコンをクリックし、settings → SSH and GPG keys をクリック

### config file の作成

```zsh
touch ~/.ssh/config
```

作成した config ファイルに下記を追加（github の場合）して保存

```config
Host github
  HostName github.com
  IdentityFile ~/.ssh/id_rsa
  User git
```

ターミナルにて下記を実行して、アクセスできることを確認。パスフレーズを設定している場合は、パスフレーズが聞かれるので注意

```zsh
ssh -T git@github.com
```

下記の応答があれば成功！

```zsh
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 無料ソフト インストール

### CheatSheet

コマンドキーを長押しするだけで、各種アプリのショートカットキーが表

https://mediaatelier.com/CheatSheet/

### Clipy

クリップボードアプリ

https://clipy-app.com/

### Alfred

https://www.alfredapp.com/

### AppCleaner

アプリ本体とそれにまつわるものも全て削除してくれる有名なアプリ

https://freemacsoft.net/appcleaner/
