---
tags:
  - python
---

# Dash

## テーブル表示のテスト

```
import dash
import dash_table
import pandas as pd
import dash_html_components as html
import dash_core_components as dcc
from dash.dependencies import Input, Output

df = pd.read_csv('data/iris.csv')

for i in range(2):
    df = pd.concat([df, df])

app = dash.Dash(__name__)
common_style = {'position': 'relative', 'width': '100%',
                'font-family': 'Dosis', 'text-align': 'center'}

app.layout = html.Div(
    children=[
        html.H1("Dash app with export csv", style={'margin-bottom': '1%'}),
        dcc.Dropdown(
            id='my-dropdown',
            options=[
                {'label': 'setosa',
                 'value': 'setosa'},
                {'label': 'versicolor',
                 'value': 'versicolor'},
                {'label': 'virginica',
                 'value': 'virginica'}
            ],
            value='setosa',
            style={'margin-bottom': '1%'}
        ),
        dcc.Loading(id="loading-1",
                    children=[
                        html.Div(id='output-container',
                                 )
                    ],
                    style={"hight": "80%"},
                    # style={"margin": "1%"},
                    type="default"),
    ],
    style=common_style
)


@app.callback(
    Output('output-container', 'children'),
    [Input('my-dropdown', 'value')])
def input_triggers_spinner(value):
    df_filtered = df[df["species"] == value]
    output_table = dash_table.DataTable(
        id='table',
        columns=[{"name": i, "id": i} for i in df.columns],
        data=df_filtered.to_dict('records'),
        style_header={
            'fontWeight': 'bold',
            'border': 'thin lightgrey solid',
            'backgroundColor': 'rgb(100, 100, 100)',
            'color': 'white'
        },
        style_cell={
            'fontFamily': 'Open Sans',
            'textAlign': 'left',
            'width': '150px',
            'minWidth': '180px',
            'maxWidth': '180px',
            'whiteSpace': 'no-wrap',
            'overflow': 'hidden',
            'textOverflow': 'ellipsis',
            'backgroundColor': 'Rgb(230,230,250)'
        },
        style_data_conditional=[
            {
                'if': {'row_index': 'odd'},
                'backgroundColor': 'rgb(248, 248, 248)'
            },
            {
                'if': {'column_id': 'country'},
                'backgroundColor': 'rgb(255, 255, 255)',
                'color': 'black',
                'fontWeight': 'bold',
                'textAlign': 'center'
            }
        ],
        # style_table={'minWidth': '100%'},
        style_table={
            'maxHeight': '1500px', 'overflowY': 'scroll'
        },
        # tooltip_header={
        #     col: "Select columns with the checkbox to include them in the hover info of the image."
        #     for col in df_filtered.columns
        # },
        # style_header={
        #     "textDecoration": "underline",
        #     "textDecorationStyle": "dotted",
        # },
        # tooltip_delay=0,
        # tooltip_duration=None,
        # filter_action="native",
        # row_deletable=True,
        # column_selectable="multi",
        # selected_columns=initial_columns,
        # style_table={"overflowY": "scroll"},
        fixed_rows={"headers": True, "data": 0},
        fixed_columns={'headers': True, 'data': 1}
        # style_cell={"width": "85px"},

        # リスト表示にします
        # style_as_list_view=True,
        # headerを固定してスクロールできるようにします
        # fixed_rows={'headers': True, 'data': 0},
        # exportするフォーマットを指定(csv or xlsx)
        # export_format='xlsx',
    )
    return output_table


if __name__ == '__main__':
    app.run_server(debug=True)

```

## 差分

### 差分比較用データの作成

```
import pandas as pd
import numpy as np
df_moto = pd.DataFrame(
                [["A001",31,12,13,14],
                 ["B002",21,22,23,24],
                 ["C003",31,32,33,34],
                 ["E005",31,32,33,34],
                 ["F006",31,32,33,34]],
                  columns=["no","a","b","c","d"])
df_mod= pd.DataFrame(
                [["A001",11,12,444,14],
                 ["C003",31,32,45,34],
                 ["D004",52,27,21,2],
                 ["E005",31,32,45,34],
                 ["F006",2224,222,33,34]],
                columns=["no","a","b","c","d"])

df_moto = df_moto.set_index("no")
df_mod = df_mod.set_index("no")

moto = set(list(df_moto.index))
mod = set(list(df_mod.index))

com_list = list(moto.intersection(mod))
add_list = list(mod - moto)
del_list = list(moto  - mod)

df_moto_i = df_moto.loc[com_list]
df_mod_i = df_mod.loc[com_list]

# df_moto_i.compare(df_mod_i)
# df_moto_i.compare(df_mod_i,align_axis=0)#行方向に表示
# df_moto_i.compare(df_mod_i, keep_shape=True)#もとの行列を保持
```

### 変更のある列を取得

```
df_com = df_moto_i.compare(df_mod_i,align_axis=0)#行方向に表示
df_com.index = df_com.index.droplevel(1)
# df_com

out_list = []
col_list = list(df_com.columns)
for col in col_list:
    ds = df_com[col].dropna()
    row_list = list(ds.index.drop_duplicates())
    temp = [[i,col] for i in row_list]
    out_list.extend(temp)

df_color = pd.DataFrame(out_list,columns=["row","col"])
df_color
```

### テーブルを描画

```
def trans_row_no(df,df_color):
    df_index = df.reset_index()[["no"]].reset_index().set_index("no")
    map_dict = dict(df_index["index"])
    df_c = df_color.copy()
    df_c["row"]=df_c["row"].map(map_dict)
    style_data_conditional=[{'if': {'row_index': df_c.iloc[i,0], 'column_id': df_c.iloc[i,1]},
                             'background-color': "#e377c2"} for i in range(df_c.shape[0])]
    return style_data_conditional,map_dict
```

#### 表示するデータとスタイルを設定

```
style_data_conditional_moto,map_dict_del = trans_row_no(df_moto,df_color)
if len(del_list) != 0:
    del_row = [map_dict_del[i] for i in del_list]
    style_data_conditional_del = [{'if': {'row_index': i}, 'background-color': "#1f77b4"} for i in del_row]
    style_data_conditional_moto.extend(style_data_conditional_del)

style_data_conditional_mod,map_dict_add  = trans_row_no(df_mod,df_color)
df = df_mod.copy()
if len(add_list) != 0:
    add_row = [map_dict_add[i] for i in add_list]
    style_data_conditional_add = [{'if': {'row_index': i},'background-color': "#d62728"} for i in add_row]
    style_data_conditional_mod.extend(style_data_conditional_add)
```

#### 表示

```
from jupyter_dash import JupyterDash
import dash
import dash_table
import dash_html_components as html
import pandas as pd

# df = pd.DataFrame(data=dict(COLOR=['#1f77b4', '#d62728', '#e377c2', '#17becf', '#bcbd22'],
#                             VALUE=[1, 2, 3, 4, 5]))

# app = dash.Dash(__name__)

def create_html_div(id_name,df,style_data_conditional):
    df = df.reset_index()
    out = html.Div([
            dash_table.DataTable(
            id= id_name,
            columns=[{'name': i, 'id': i} for i in df.columns],
            data=df.to_dict('records'),
            editable=True,
    #         row_selectable="multi",
    #         selected_rows=[0],
            style_header={'backgroundColor': 'rgb(167, 100, 100)'},
#             style_cell={
#                 'backgroundColor': 'rgb(50, 50, 50)',
#                 'color': 'white',
#                 "fontFamily": "Arial",
#                  "size": 10, 'textAlign': 'center'},
            style_table={'overflowX': 'auto'},
            style_cell={
                'height': 'auto',
                # all three widths are needed
                'minWidth': '20px', 'width': '20px', 'maxWidth': '20px',
                'whiteSpace': 'normal',
                 'textAlign': 'center'},
            style_data_conditional=style_data_conditional)
        ])
    return out

# 背景色と文字色を事前に設定しておく。
colors = {
    'background': '#111111',
    'text': '#7FDBFF'
}

app = JupyterDash(__name__)

moto = create_html_div("table_moto",df_moto,style_data_conditional_moto)
mod = create_html_div("table_mod",df_mod,style_data_conditional_mod)

app.layout = html.Div([
    html.H1(
        children='変更後',
        style={
            'textAlign': 'center',
            'color': colors['text']
        }
    ),
    mod,
    html.H1(
        children='変更前',
        style={
            'textAlign': 'center',
            'color': colors['text']
        }
    ),
    moto])
app.run_server(mode="inline")
# app.run_server(debug=True)

```
