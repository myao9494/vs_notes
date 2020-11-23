---
tags:
  - 強化学習
---

# 2020-11-23 gym_anytrading

【jupyter 起動】

```jupyter
conda activate openai_gym
cd 000_work/gym-anytrading
jupyter notebook
```

## 概要把握

### github readme

- EX と Stock をサポート
- gym で強化学習できる
- TradingEnv は、あらゆる種類の取引環境をサポートできるように設計（TradingEnv を継承することによって）

### TradingEnv

- TradingEnv は gym.Env の継承クラス
- あらゆる種類の取引市場に汎用環境を提供することを目的

#### プロパティ

- df:['Open', 'High', 'Low', 'Close', 'Adj Close', 'Volume']の dataframe
- window_size:いくつのティック（値動き単位の最小値）を使うか
- frame_bound：(開始,終了)を指定するタプル　※開始>=window_sizeとすること
- unit_side

### example a2c_quantstats

#### import libraly

quantstats:株の分析のためのライブラリ



## 確認事項

- [ ] df で最低限必要な列を確認 Adj Close は必要か？たぶん不必要
- [ ] 開始が必ずshortになっているのはなぜ？
- [ ] rewardとprofitの計算はどうなっている？
- [ ] 
