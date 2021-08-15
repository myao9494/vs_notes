---
tags:
  - macbook
---

# macbook_setup

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=2 orderedList=true} -->

<!-- code_chunk_output -->

1. [システム環境設定](#システム環境設定)
2. [Finder の設定](#finder-の設定)
3. [ネットワークドライブの設定](#ネットワークドライブの設定)
4. [日本語入力関係](#日本語入力関係)
5. [git](#git)
6. [VS code](#vs-code)
7. [anaconda](#anaconda)
8. [chrome](#chrome)
9. [無料ソフト インストール](#無料ソフト-インストール)
10. [homebrew](#homebrew)
11. [ssh](#ssh)

<!-- /code_chunk_output -->

## システム環境設定

### コンピュータ名の変更

1. システム環境設定を開く
1. 共有をクリック
1. コンピュータ名を適宜変更する

### ディスプレイの設定

1. システム環境設定を開く
1. ディスプレイをクリック
1. Night Shift をクリック
1. スケジュールで時間を入れるか、日の入りから日の出までにする

### トラックパッドの設定

1. システム環境設定を開く
1. チェックできるところは全部チェックする
1. 軌跡の速さを調節する

### Dock とメニューバーの設定

1. システム環境設定をクリック
1. Dock とメニューバーをクリック
1. ウィンドウの左サイドバーを下にスライド
1. バッテリーをクリック
1. 割合（%）を表示にチェックを入れる
1. dock の位置：画面上の位置の右にチェックを入れる

### ファイアウォールの設定

1. システム環境設定を開く
1. ファイアウォールをクリック
1. ファイアウォールをオンにするをクリック

### キーボードの設定

1. システム環境変数を開く
1. キーボード
1. ショートカット
1. コントロール間のフォーカス移動をキーボードで操作 にチェック
1. スクリーン
1. ⌘⇧5 と ⌘⇧6  のチェックを外す（skitch のために）
1. もとの ⌘⇧5 を ⌘⇧7 に割り当てる(動画キャプチャのため)
1. 「キーボード」の「修飾キー」を開き、Caps Lock キーの割り当てを「Command」にする

## Finder の設定

1. 何かフォルダを開く
1. 画面左上の Finder をクリック
1. 環境設定をクリック
1. 詳細タブ
1. 全てのファイル名拡張子を表示にチェックを入れる
1. 画面上のメニューから表示をクリック
1. ステータスバーを表示をクリック
1. パスバーを表示をクリック
1. サイドバーを表示
1. よく使うフォルダをサイドバーにドラッグ&ドロップして追加する

## ネットワークドライブの設定

### nas のドライブの設定

http://ftp.tekwind.co.jp/pub/misc/Rakko/Macintosh_connect_manual.pdf

1. Finder メニューバーが表示されている状態で、「移動」 > 「サーバへ接続」
1. 「サーバへ接続」ウィザードが開いたら、「サーバアドレス」の欄に、"smb://<NAS の IP アドレス>"と入力し、「接続」をクリックします。例"smb://192.168.0.203"
   `smb://192.168.0.111/`
1. ログイン情報の入力して設定
1. システム環境設定をを開く
1. NAS をマウントしている状態で｢システム環境設定｣の｢ユーザーとグループ｣を開く
1. 「ログイン項目」のタブで"+"ボタンをクリック
1. 追加するデバイスの選択画面で、先ほど接続設定したものを指定

## 日本語入力関係

### google 日本語入力

https://www.google.co.jp/ime/　からダウンロード

1. 画面右上のあもしくは A をクリック
1. google を選択する
1. 環境設定をクリックして、入力補助の数字を半角に変更
1. スペースを半角に変更

### 辞書

1. 自分の名前を登録

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

### ssh の設定

2021.8.13 からパスワードで push できなくなった。トークンを使うか、SSH を使うかだが、私は SSH を使っている。

以下のフォルダに、`id_rsa`をコピー
`/Users/user/.ssh`
※テキストだけをコピーした場合はパーミッションエラーになるので、.ssh のフォルダに移動して、下記コマンドを実行する
`chmod 600 id_rsa`

完了したら、下記コマンドでテストして OK なら完了
`ssh -T git@github.com`

各リポジトリの.git は、下記書き方のなっている必要あり。
`url = git@github.com:ユーザ名/リポジトリ名.git`

(詳細)
https://github.com/myao9494/ssh_test

## VS code

### 設定

自分のリポジトリを落としてきて設定する

1. エクステンションや設定関係
   https://github.com/myao9494/VS_Code_setting_myao
1. vsnotes
   https://github.com/myao9494/vs_notes

### terminal から起動できるようにする

1. コマンドパレットを開き、「shell command install」を入力
1. 「シェルコマンド: PATH 内に ‘code’ コマンドをインストールします」と表示されるので選択
1. 右下に「シェルコマンド ‘code’ が PATH に正常にインストールされました。」と表示されれば成功。

## anaconda

### インストール

https://www.anaconda.com/products/individual#Downloads

m1 対応は無かったので、通常の intel mac 用を公式 HP からダウンロードしてインストール

### アンインストール

https://code-graffiti.com/how-to-unistall-anaconda-on-mac/

1. 下記にコマンドを実行

   ```zsh
   conda install anaconda-clean
   anaconda-clean
   ```

1. Anaconda を Home ディレクトリから手動で削除
   `/Users/myao9494/opt/homebrew`の下にある
1. shell の Anaconda への PATH を削除

## chrome

m1 用をインストール、問題なく快適

### 表示設定

1. ツールバーの表示で、全画面表示でもツールバーを表示する設定にする

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
設定で、web bookmarks で各ブラウザのブックマークを追加する

https://freemacsoft.net/appcleaner/

### skitch

appstore からインストールする

### MindNode

appstore からインストール

### BackgroundMusic

画面動画キャプチャで音声を入れるために必要

下記リポジトリのリリースから最新版をインストール

https://github.com/kyleneideck/BackgroundMusic

### Scroll Reverser

トラックパッドとマウスのスクロール方向を逆に

https://pc-karuma.net/mac-app-scroll-reverser/

## homebrew

mac のパッケージ管理ソフト、これの他に macport がある。

https://zenn.dev/ress/articles/069baf1c305523dfca3d

m1 と x64 の両方を入れる（サポートされていないことが未だ多いので）
前提として Rosetta をインストールしている（ここまで来る間に、どこかでインストールされるはず）

### ｘ 64 インストール

arch コマンドは Rosetta がインストールされれば  使えるようになるらしい

```zsh
arch -arch x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### M1 版をインストール

https://docs.brew.sh/Installation

mkdir でパスワードを聞かれるので、ログインパスワードを入れる
以下の場合は、usre にインストールする場合

```zsh
cd opt
mkdir homebrew
curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew

```

### zsh にパスを通す

`/Users/user/.zshrc`を開いて、下記を追加する

```text
setopt no_global_rcs   # ignore /etc/z*
typeset -U path PATH
path=(
    /opt/homebrew/bin(N-/)
    /usr/local/bin(N-/)
    $path
)

if [[ "${(L)$( uname -s )}" == darwin ]] && (( $+commands[arch] )); then
	alias brew="arch -arch x86_64 /usr/local/bin/brew"
	alias x64='exec arch -arch x86_64 "$SHELL"'
	alias a64='exec arch -arch arm64e "$SHELL"'
	switch-arch() {
		if  [[ "$(uname -m)" == arm64 ]]; then
			arch=x86_64
		elif [[ "$(uname -m)" == x86_64 ]]; then
			arch=arm64e
		fi
		exec arch -arch $arch "$SHELL"
	}
fi

setopt magic_equal_subst
```

### 使い方

brew は Rosetta を使う、ARM 版は =brew のように =をつける!

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
