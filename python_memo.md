---
tags:
  - 01_チートシート
  - python
---

# python の忘備録

調べることをまとめました。都度更新です

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=2 orderedList=false} -->

<!-- code_chunk_output -->

- [python の忘備録](#python-の忘備録)
  - [python の作法](#python-の作法)
    - [アンダースコア"\_"の役割](#アンダースコア_の役割)
  - [判定](#判定)
    - [bool 値の判定](#bool-値の判定)
    - [if 文](#if-文)
  - [リスト内包表記](#リスト内包表記)
  - [辞書](#辞書)
  - [for 文](#for-文)
  - [file/folder 操作](#filefolder-操作)
  - [例外処理](#例外処理)
  - [ライブラリ](#ライブラリ)
    - [python pip](#python-pip)
    - [ライブラリのリロード、再読み込み](#ライブラリのリロード再読み込み)
    - [バイナリのライブラリ](#バイナリのライブラリ)
  - [python からフォルダやファイルを開く](#python-からフォルダやファイルを開く)
  - [クリップボード　 clipboard](#クリップボード-clipboard)
    - [クリップボード（文字列）](#クリップボード文字列)
    - [クリップボード（画像）](#クリップボード画像)
  - [画像関係](#画像関係)
    - [結合](#結合)
    - [画像を PDF に変換](#画像を-pdf-に変換)
  - [Gitpython](#gitpython)
  - [メッセージをポップアップ popup](#メッセージをポップアップ-popup)
  - [beep 音を出す　音を出す　知らせる](#beep-音を出す音を出す知らせる)
  - [ショートカットを作成](#ショートカットを作成)
  - [時間](#時間)
  - [sqlite 関係](#sqlite-関係)
  - [ポイントを時計回りに並べ替える](#ポイントを時計回りに並べ替える)
  - [文字列](#文字列)
    - [正規表現を用いた置換（マッチした一部を再利用）](#正規表現を用いた置換マッチした一部を再利用)
    - [decode](#decode)
    - [数字の表示 for CAE (浮動小数点　 e または E で表示)](#数字の表示-for-cae-浮動小数点-e-または-e-で表示)
  - [selenium](#selenium)
  - [subprocess と log](#subprocess-と-log)
  - [環境変数](#環境変数)
  - [クラスのテンプレ](#クラスのテンプレ)

<!-- /code_chunk_output -->

## python の作法

### アンダースコア"\_"の役割

- アンダースコア二つで定義される関数は外部の参照を受けないもの。この場合、アンダースコアで囲う。
- アンダースコア一つで定義される関数は参照はできるが、基本的に外部から参照しない ということを慣習化させたものらしい。

## 判定

### bool 値の判定

```bool
done = agent_pos == 0 # agent_pos = 0ならば、done = Trueとなる。
```

### if 文

```if
reward = 1 if done else -0.1 #done = True　ならば、reward=1 それ以外は reward = -0.1
```

## リスト内包表記

```list_nai.py
stocks = [i for i in os.listdir(".") if mei in i ]
stocks = [i for i in os.listdir(".") if mei in i and "csv" in i]
```

## 辞書

- 辞書への入力と出力

```dict_input_output.py
dict_test = {}
retu_mei = ["現在値","出来高","前日終値"]

for key in retu_mei:
    dict_test[key] = 10

for key in dict_test:
    print(key , dict_test[key])
```

- 辞書型一般

```dict.py
mydict = {"papa":"L", "O":"Orage", "G":"Grapes"}
mydict.keys() #keyの表示
list(mydict.items()) #リスト化
```

## for 文

- インデックスを取得して for 文を回す enumerate

```index.py
for no,data in enumerate(scaled_data):
    print(no,data)
```

- 2 つのリストを平行にループする zip

```zip.py
for a, b in zip(scaled_data, scaled_parameters):
    print(a,b)
```

## file/folder 操作

- 相対パスから絶対パスに変換

```pathlib.py
import pathlib
file_path = pathlib.Path("./agent")
a_path = file_path.resolve()#絶対パスに変換
str(a_path)#pathを文字列化
```

- フォルダの中のファイルをリストで取得する

```file_mei.py
import os
data_folder = os.path.join(os.getcwd(),"../data")
stocks = [i for i in os.listdir(data_folder) if '.csv' in i]
```

- file を読み込んで、list にする

```read.py
with open(r"C:\***.txt") as f:
    li = f.readlines()
print(li)

li_replace = [s.replace('\n', '') for s in li]
print(li_replace)
```

- csv へ書き込み

```csv_write.py
l = [[0, 1, 2], ['a\nb', 'x', 'y']]

with open('data/temp/sample_writer_linebreak.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerows(l)
```

- フォルダの操作

```folder.py
if not os.path.exists(os.path.dirname(f_path_copy)):#フォルダが無ければ作成する
    os.makedirs(os.path.dirname(f_path_copy))

shutil.rmtree("diff_env")#フォルダの削除

os.mkdir("diff_env", exist_ok=True))#フォルダの作成 diff_enbがあってもエラーにならない
```

- ファイルとフォルダのコピー

```folder.py
import shutil
import pathlib

# コピーするファイル
fromFilePath = pathlib.Path('./test.txt')
# コピー先のディレクトリ(フォルダ)
toDirPath = pathlib.Path('./copydir')

# ディレクトリが無ければ作る
#  parents=True -> 親ディレクトリが無ければ作成
#  exist_ok=True -> ディレクトリがあってもエラーにしない
toDirPath.mkdir(parents=True, exist_ok=True)

# ファイルコピー
shutil.copy(fromFilePath, toDirPath)

# フォルダのコピー（中身こみ）
shutil.copytree('./sample', './sample_backup')
```

## 例外処理

- 例外処理した際のエラーメッセージを表示させる

```try_except_trackback.py
import traceback
try:
   aaa
except:
   traceback.print_exc()
```

## ライブラリ

### python pip

インストールされているライブラリを表示する

```pip
pip freeze
```

### ライブラリのリロード、再読み込み

```reload.py
import importlib
importlib.reload(foo)
```

### バイナリのライブラリ

以下のサイトからダウンロードして、pip で OK

`https://www.lfd.uci.edu/~gohlke/pythonlibs/`

## python からフォルダやファイルを開く

```start.py
import os
from pathlib import Path
os.startfile(Path.cwd())#現在のフォルダを開く
```

## クリップボード　 clipboard

### クリップボード（文字列）

```clip.py
tex = pyperclip.paste() #クリップボードから取り出す
pyperclip.copy(tex) #クリップボードに入れる
```

### クリップボード（画像）

- 画像を取り出す

```get_image_from_clip_board.py
from PIL import ImageGrab
im = ImageGrab.grabclipboard()
im.rotate(-90,expand=True)#回転
```

- 画像を入れる

```to_clipboard.py
from io import BytesIO
import win32clipboard
from PIL import Image

def send_to_clipboard(clip_type, data):
    win32clipboard.OpenClipboard()
    win32clipboard.EmptyClipboard()
    win32clipboard.SetClipboardData(clip_type, data)s
    win32clipboard.CloseClipboard()

output = BytesIO()
im.convert("RGB").save(output, "BMP")
data = output.getvalue()[14:]
output.close()

send_to_clipboard(win32clipboard.CF_DIB, data)
```

## 画像関係

### 結合

`https://note.nkmk.me/python-pillow-concat-images/`

```merge.py
# 横方向に結合（高さを低い方に合わせて）
def get_concat_h_cut(im1, im2):
    dst = Image.new('RGB', (im1.width + im2.width, min(im1.height, im2.height)))
    dst.paste(im1, (0, 0))
    dst.paste(im2, (im1.width, 0))
    return dst

# 縦方向に結合（幅を小さい方に合わせて）
def get_concat_v_cut(im1, im2):
    dst = Image.new('RGB', (min(im1.width, im2.width), im1.height + im2.height))
    dst.paste(im1, (0, 0))
    dst.paste(im2, (0, im1.height))
    return dst
```

### 画像を PDF に変換

インストール

```pip
pip install PyMuPDF
```

リストの画像を pdf に変換

```pdf.py
import sys, fitz
imglist=[r"path.png"]

doc = fitz.open()                            # PDF with the pictures
for i, f in enumerate(imglist):
    img = fitz.open(f) # open pic as document
    rect = img[0].rect                       # pic dimension
    pdfbytes = img.convertToPDF()            # make a PDF stream
    img.close()                              # no longer needed
    imgPDF = fitz.open("pdf", pdfbytes)      # open stream as PDF
    page = doc.newPage(width = rect.width,   # new page with ...
                       height = rect.height) # pic dimension
    page.showPDFpage(rect, imgPDF, 0)
           # image fills the page
doc.save("eall-my-pics.pdf")
```

## Gitpython

```pip
pip install GitPython
```

path のフォルダに対して、initial commit する

```git_python.py
taisho_path = r"path"
rep = git.Repo.init(taisho_path)#リポジトリ作成
rep = git.Repo(taisho_path)
repo.git.add("--all")#全てをステージング
repo.index.commit("initial commit")#initial commit
```

## メッセージをポップアップ popup

`https://stackoverflow.com/questions/2963263/how-can-i-create-a-simple-message-box-in-python`

```message_popup_without_tk.py
import ctypes  # An included library with Python install.
ctypes.windll.user32.MessageBoxW(0, "Your text", "Your title", 1)
```

最前面にメッセージボックスを表示して、最前面で固定する

```message_popup_zenmen.py
import tkinter
from tkinter import messagebox

root = tkinter.Tk()
# topmost指定(最前面)
root.attributes('-topmost', True)
root.withdraw()
root.lift()
root.focus_force()

messagebox.showinfo("title", "message")# メッセージボックス（情報）
messagebox.showwarning("title", "message")# メッセージボックス（警告）
messagebox.showerror("title", "message")# メッセージボックス（エラー）
messagebox.askyesno("title", "message")# メッセージボックス（はい・いいえ）
messagebox.askquestion("title", "message")# メッセージボックス（はい・いいえ）
messagebox.askokcancel("title", "message")# メッセージボックス（OK・キャンセル）
messagebox.askretrycancel("title", "message")# メッセージボックス（再試行・キャンセル）
```

## beep 音を出す　音を出す　知らせる

```beep.py
import winsound
winsound.Beep(1000,800)
```

## ショートカットを作成

```cut.py
import win32com.client
ws = win32com.client.Dispatch("wscript.shell")
scut = ws.CreateShortcut('run_idle.lnk')
scut.TargetPath = '"c:/python27/python.exe"'
scut.Arguments = '-m idlelib.idle'
scut.Save()
```

## 時間

- string ⇨ datetime フォーマットに気をつける。

```str2datetime.py
from datetime import datetime as dt
tstr1 = '2019-01-01 00:00:00'
tdatetime = dt.strptime(tstr1, '%Y-%m-%d %H:%M:%S')
tstr2 = '2019/01/01 00:00:00'
tdatetime = dt.strptime(tstr2, '%Y/%m/%d %H:%M:%S')
```

- datetime ⇨ string

```datetime2str.py
from datetime import datetime as dt
tdatetime = dt.now()
tstr1 = tdatetime.strftime('%Y-%m-%d') # 2018-1-18
tstr2 = tdatetime.strftime('%Y/%m/%d %H:%M:%S') # 2018/1/18 12:34:56
tstr3 = tdatetime.strftime('%Y%m%d') # 20180118 ファイル名を入れる時に使う
```

- datetime の足し算引き算

```cal_time.py
now = datetime.now()
tomorrow = now + datetime.timedelta(days = 1) #今より1日後
nextweek = now + datetime.timedelta(weeks = 1) #今より一週間後
```

- date と time を結合する

```combine.py
datetime.datetime.combine(datetime.date(2011, 1, 1), datetime.time(10, 23))
```

## sqlite 関係

作成　テーブル作成　レコードを追加

```sqlite.py
import sqlite3
conn = sqlite3.connect('sample.db')

cur = conn.cursor() # Create a 'Cursor' object from 'Connection' object.
cur.execute('''CREATE TABLE memo(date TEXT, title TEXT, body TEXT)''')# Create a table データベースファイルが存在しない場合は新規に作成
cur.execute("""INSERT INTO memoVALUES('2007-01-01', 'Memo1', 'Body1')""")# Insert a record
conn.commit()# コミット
conn.close()# コネクションをクローズ
```

## ポイントを時計回りに並べ替える

```point_resample.py
pnt = [[-0.4, -1.52], [-1.8, -0.36],[-0.1, 0.8], [0.27, 0.4], [0.42, 0.28]]

def _angle_between(refvec):
    origin=[0,0]
    ang1 = np.arctan2(*origin[::-1])
    ang2 = np.arctan2(*refvec[::-1])
    return np.rad2deg((ang1 - ang2) % (2 * np.pi))

pnt = sorted(pnt, key=_angle_between)#時計回り
pnt = sorted(pnt, key=_angle_between,reverse=True)#反時計回り
```

## 文字列

### 正規表現を用いた置換（マッチした一部を再利用）

https://www.aipacommander.com/entry/2014/06/17/184220

`(.*)`の部分が再利用されます。対応は、`\\1`と`\\2`になる

下記例は、html の image のリンクを markdown に変換するときに使いました

```resub.py
import re
tex = '<img src="image/2020-11-21-11-29-29.png" alt="example">'
pattern = '<img src="(.*)" alt="(.*)">'
rep = '![\\2](\\1)'
rep_tex = re.sub(pattern,rep,tex)
```

`>> '![example](image/2020-11-21-11-29-29.png)'`

### decode

```str.py
def decodef(src):#【デコード】
    try:
        src=src.decode('utf-8')
        return src
    except:
        print("decode error")
```

### 数字の表示 for CAE (浮動小数点　 e または E で表示)

```sample.py
a=1.5/10000 #0.00015
b="{:.4e}".format(a) #'1.5000e-04'
c = b.replace("e","E") #''1.5000E-04'
d = '{:0=3}'.format(1) #0埋め '001'
```

## selenium

selenium chrome driver に path を通しておく必要あり

```selenium.py
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("http://localhost:50001/startp")
driver.quit()
```

## subprocess と log

subprocess `http://qiita.com/mokemokechicken/items/a84b0aa96b94d1931f08`

```subprocess.py
import os,subprocess
args=["C:\Program Files (x86)\MarketSpeed\MLauncher\MLauncher.exe" ,"MarketSpeed"]
p1=subprocess.Popen(args)
p1.wait()#処理待ちしない場合は、これを消す
```

引数 "7974"を渡して subupro_test.py を実行させる。実行結果はログファイル'test7974.log'に書き出す。
subprocess で実行する際は、log を付けておけば実行途中の状態も確認できる

```oya.py
import subprocess
test = subprocess.Popen("python subpro_test.py 7974")
```

```subupro_test.py
# coding: UTF-8
import sys
import time
from logging import getLogger, StreamHandler, DEBUG,FileHandler

param = sys.argv

logger = getLogger(__name__)
file_handler = FileHandler('test' +param[1] + '.log',mode="w", encoding='utf-8')#modeを指定しないと上書きしていく
file_handler.setLevel(DEBUG)
logger.addHandler(file_handler)
logger.setLevel(DEBUG)
logger.propagate = False

# handler = StreamHandler()
# handler.setLevel(DEBUG)
# logger.addHandler(handler)

try:
    for i in range(100):
        logger.debug(param[1]+str(i))
        time.sleep(1)
except:
    logger.debug("error", exc_info=True)#trackback
```

log に関して
以下のサイトを参考にテンプレート化
`https://qiita.com/amedama/items/b856b2f30c2f38665701`

上記はファイルに書き出す場合、#で消したいる部分を消せば、ターミナルと両方に出力される。

## 環境変数

```environ.py
os.environ['userprofile']#環境変数を取得
sys.path.append("/Users/username/Desktop")#ライブラリを読み込むパスを追加（一時的にpythonpathに追加）
```

## クラスのテンプレ

```class.py
#---------------------------class ------------------------------------
# -*- coding: utf-8; py-indent-offset:4 -*-
###############################################################################
#
# Copyright (C) ***
#
###############################################################################
from redminelib import Redmine

module_path = os.path.dirname(__file__)

class redmine_tanuki(object):
    '''
    自分自身が使いやすい環境を構築する
    '''
    def __init__(self,url,user_name,pass_word):
        self.redmine = Redmine(url, username=user_name, password=pass_word)

if __name__ == '__main__':
    obj=redmine_tanuki('a','b','c')
```
