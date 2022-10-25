---
tags:
  - base
---

# Google Spread Sheet を python から操作する

## 公式

- Sheets for Developers Sheets API
  https://developers.google.com/sheets/api/quickstart/python

- Create a project and enable the API
  https://developers.google.com/workspace/guides/create-project

## 動画

- Python で Google スプレッドシートの作業を一瞬で終わらせる｜プログラミングによる自動化仕事術
  https://www.youtube.com/watch?v=fFSGPciIkfI

## ライブラリ

```
pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
pip install gspread oauth2client
pip install gspread_dataframe
```

## テストコード

無事にすべて動きました!すごい

```
import gspread
from oauth2client.service_account import ServiceAccountCredentials

#jsonファイルを使って認証情報を取得
scope = ["https://spreadsheets.google.com/feeds","https://www.googleapis.com/auth/drive"]
c = ServiceAccountCredentials.from_json_keyfile_name("設定した.json", scope)

#認証情報を使ってスプレッドシートの操作権を取得
gs = gspread.authorize(c)

#共有したスプレッドシートのキー（後述）を使ってシートの情報を取得
SPREADSHEET_KEY = "urlから取得"
worksheet = gs.open_by_key(SPREADSHEET_KEY).worksheet("シート1")
print(worksheet.acell("A1").value)

import pandas as pd

workbook = gs.open_by_key(SPREADSHEET_KEY)
worksheet = workbook.worksheet("シート1")
df = pd.DataFrame(worksheet.get_all_values())
df.columns = df.iloc[0]
df = df.drop(df.index[[0]])

df_sum = df.copy()
from gspread_dataframe import set_with_dataframe
workbook.add_worksheet(title="会社別売上", rows=50, cols=10)
set_with_dataframe(workbook.worksheet("会社別売上"), df_sum, include_index=True)

```
