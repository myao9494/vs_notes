---
tags:
  - base
---

# mysql

## setup

### インストール

`brew install mysql`

### バージョン確認

`mysql --version`
mysql Ver 8.0.12 for osx10.13 on x86_64 (Homebrew)

### mysql サーバを立ち上げる。

`mysql.server start`
Starting MySQL
.. SUCCESS!

### mysql_secure_installation を実行

`mysql_secure_installation`

```
Securing the MySQL server deployment.
Connecting to MySQL using a blank password.
VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?
Press y|Y for Yes, any other key for No: y
```

VALIDATE PASSWORD というコンポーネントをインストールするか。
ゆるいパスワード（abc/passwd など）を登録したい場合はｎ
