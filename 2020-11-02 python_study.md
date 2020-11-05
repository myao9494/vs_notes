---
tags:
  - memo
  - ライブラリ
  - python
---

# 2020-11-02 python_memo

- fire : コマンドラインツールを簡単に作れる

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

## デコレータ
