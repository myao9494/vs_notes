---
tags:
  - 01_チートシート
---

# 2020-10-31 linux

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [2020-10-31 linux](#2020-10-31-linux)
  - [windows10 で linux 環境を構築する](#windows10-で-linux-環境を構築する)
    - [WSL を有効化](#wsl-を有効化)
    - [Microsoft Store で Ubuntu をインストール](#microsoft-store-で-ubuntu-をインストール)
    - [anaconda のインストール](#anaconda-のインストール)
    - [WSL のフォルダへアクセスする](#wsl-のフォルダへアクセスする)
    - [WSL から windows フォルダへアクセスする](#wsl-から-windows-フォルダへアクセスする)
    - [VcXsrv のインストール](#vcxsrv-のインストール)
    - [VcXsrv で WSL の Linux の GUI を表示させる](#vcxsrv-で-wsl-の-linux-の-gui-を表示させる)
    - [強化学習用](#強化学習用)
    - [VScode からアクセス](#vscode-からアクセス)
    - [jupyter notebook の設定](#jupyter-notebook-の設定)
  - [bush command](#bush-command)

<!-- /code_chunk_output -->

## windows10 で linux 環境を構築する

参考:

- [Windows 10 で Linux を使う](https://qiita.com/whim0321/items/093fd3bb2dd287a72fba)

- [Jupyter Notebook を WSL に構築](https://qiita.com/hiiragi1104/items/c2e9042bc6170873a859)

- [WSL と windows 間のファイル連携](https://qiita.com/quzq/items/1096c638c0d86795be13)
- [WSL+ubuntu18.04+VcXsrv+OpenAI Gym 動くまでのメモ（修正）](https://qiita.com/antimon2/items/b1611dca09edcf93db03)

### WSL を有効化

PowerShell を管理者権限(右クリックで選択）で起動して、下記コマンドを実行

```shell
cd C:\Windows\System32
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

完了すると、強制的に再起動

### Microsoft Store で Ubuntu をインストール

- Ubuntu で検索して、インストールして、起動すると CLI が現れるので、初期設定を行う

- 初期設定

  - ID と PW を設定する
  - リポジトリを日本に変更

    ```bush
    sudo sed -i -e 's%http://.*.ubuntu.com%http://ftp.jaist.ac.jp/pub/Linux%g' /etc/apt/sources.list
    ```

- update,upgrade

  ```bush
  sudo apt update
  sudo apt upgrade
  ```

### anaconda のインストール

```bash
wget https://repo.continuum.io/archive/Anaconda3-2020.02-Linux-x86_64.sh
bash Anaconda3-2020.02-Linux-x86_64.sh
```

いろいろ聞かれるけれど、全部　 yes 　でＯＫ

### WSL のフォルダへアクセスする

エクスプローラーで、`\\wsl$`でアクセスできる

ホームの場所は、`\\wsl$\Ubuntu\home\ユーザ名`

### WSL から windows フォルダへアクセスする

```bash
cd /mnt/c
```

### VcXsrv のインストール

atari の画面を見るために、必要、GUI

- ダウンロード : https://sourceforge.net/projects/vcxsrv/files/latest/download

- Linux CLI で下記を実行（bash の設定ファイルに書き込み）
  　※　`source ~/.bashrc`は再読み込み

  ```bash
  echo 'export DISPLAY=localhost:0.0' >> ~/.bashrc
  echo 'export "LIBGL_ALWAYS_INDIRECT=1"' >> ~/.bashrc
  source ~/.bashrc
  ```

### VcXsrv で WSL の Linux の GUI を表示させる

- VcXsrv を起動（設定が出てくるが、全部デフォルトでＯＫ）

### 強化学習用

`sudo apt-get install -y libglu1-mesa-dev libgl1-mesa-dev libosmesa6-dev xvfb ffmpeg curl patchelf libglfw3 libglfw3-dev cmake zlib1g zlib1g-dev swig`

### VScode からアクセス

### jupyter notebook の設定

- ログインパスワードの設定

  ```bush
  jupyter notebook --generate-config
  jupyter notebook password
  ```

  パスワードは暗号化され`~/.jupyter/jupyter_notebook_config.json`に保存されます．

- 起動ショートカットの作成

リンク先：C:\Windows\System32\wsl.exe jupyter notebook --no-browser
作業フォルダー：初期ディレクトリ(e.g. %USERPROFILE%\jupyter)

初期ディレクトリは Windows 上の表現で OK です．
ショートカットならアイコンを Jupyter のものに設定できます．

## bush command

```bush
ps ux | grep fess  "fess"を含む自分が立ち上げているプロセスを表示
kill プロセスid  プロセスを終了
kill -9 プロセスid　プロセスを強制終了
```
