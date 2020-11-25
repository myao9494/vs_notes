---
tags:
  - study
  - python
---

# 2020-11-02 python_memo

- fire : コマンドラインツールを簡単に作れる

## デコレータ

TBD

## Enum

enum は enumeration の略で列挙型
※　 Enum(列挙型)とは、複数の定数をひとつにまとめておくことができる型

【メリット】

「使用可能な定数を明確化できる」「定数を複数のクラスで使い回せる」といったメリットが挙げられます。

【サンプル】

```python
from enum import Enum

class Ordinal(Enum):
    NORTH = "北"
    SOUTH = "南"
    EAST = "東"
    WEST = "西"

def show_ordinal(ordinal):
    if ordinal == Ordinal.NORTH:
        print("北です")
        print(f"{Ordinal.NORTH.value}です")
    elif ordinal == Ordinal.SOUTH:
        print("南です")
        print(f"{Ordinal.SOUTH.value}です")
    elif ordinal == Ordinal.EAST:
        print("東です")
        print(f"{Ordinal.EAST.value}です")
    elif ordinal == Ordinal.WEST:
        print("西です")
        print(f"{Ordinal.WEST.value}です")
    else:
        print("方角が選択されていません")

show_ordinal(Ordinal.NORTH) #北です
```

## Python の可変長引数（\*args, \*\*kwargs）の使い方

- `*args`: 複数の引数をタプルとして受け取る
- `**kwargs`: 複数のキーワード引数を辞書として受け取る

## コールバック

コールバック関数とは、プログラム中で、呼び出し先の関数の実行中に実行されるように、あらかじめ指定しておく関数。他の関数に引数として渡す関数のこと。

```call_back.py
def handler(func,*args):
    return func(*args)

def say_hello(name):
    print("Hello!!")
    print(name)

if __name__ == "__main__":
    callback = say_hello
    #callbackにsay_helloのオブジェクトIDを格納
　　handler(callback, "moroku0519")
```

## クロージャー

https://qiita.com/kangetsu121/items/2fd0c6ec2729fc711340

関数が第一級オブジェクトであるため、変数に関数を格納すると その関数定義自体と共にその環境 が格納されることを利用する、関数を状態ごと保持したオブジェクト

```example.py
def createCounter():
    cnt = [0]
    print("running createCounter")

    def inner():
        cnt[0] += 1  # cnt[0] = cnt[0] + 1
        print(cnt)
        print("running inner")
    return inner


counter = createCounter()  # ちなみにここで "running createCounter" が printされる

```

`counter()`を実行する度に`cnt[0]`が 1 づつ増える

ちなみに、`counter()()`とすると、関数内関数`inner`が実行される
