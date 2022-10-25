---
tags:
  - base
---

# AWS

## 初期設定

これを参考に
https://www.youtube.com/watch?v=Yh_D3aPVnmY

### root には多要素認証をつける

MFA で多要素認証にする

### 作業ユーザの追加

root で作業するのは推奨されないので、IAM でユーザを追加する

### 予算管理

予算が超過したらアラートを出すように設定する

## spread sheet 操作 lambda で

https://qiita.com/mimimi-no-sesese/items/ffa586bdfda968d3f20d

## Serverless Framework

前半はいい感じ! https://qiita.com/yohei7328/items/e392617864f09c87aeb9

参考:https://qiita.com/masaemon/items/ef7efa7707203a3873a7

サンプル
https://github.com/serverless/examples

### 準備・環境

- serverless をインストール
  `npm install -g serverless`
- AWS IAM ユーザーの作成
- shell で AWS を使えるようにしておく
  `pip3 install awscli`

### やり方

- 作業フォルダに移動
- `sls create --template aws-python3 -p maken` で、テンプレートを作成
-
