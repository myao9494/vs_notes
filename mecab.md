---
tags:
  - base
---

# mecab

## mac

Mac に MeCab を利用できる環境を整える
https://qiita.com/paulxll/items/72a2bea9b1d1486ca751

```
brew install mecab
brew install mecab-ipadic
pip install mecab-python3
python -c "import MeCab"
brew install xz
git clone --depth 1 git@github.com:neologd/mecab-ipadic-neologd.git
cd mecab-ipadic-neologd
./bin/install-mecab-ipadic-neologd -n
```

なにか聞かれたら YES

テスト 通常

```
echo "インスタ映え" | mecab
```

テスト 辞書使用

```
 echo "2021年12月24日 クリスマス | "mecab -d /opt/homebrew/lib/mecab/dic/mecab-ipadic-neologd
```
