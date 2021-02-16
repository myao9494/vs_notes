---
tags:
  - base
---

# mesh から surface へ

## Blender Subdivision から NURBS（IGES）まで無料で

https://blenderartists.org/t/from-blender-subdivision-to-n-u-r-b-s-iges-for-free/680688/5

## 必要ソフト

1. meshconv:https://www.patrickmin.com/meshconv/
1. FreeShip_Plus:https://github.com/markmal/freeship-plus-in-lazarus
1. gcad:http://gcad3d.org/

## 手順

1. blneder から obj で export(Z 軸を上にする)
1. meshconv で wrl に変換
   `meshconv -c wrl -vrmlver 1blender-file.obj`
1. FreeShip_Plus で読み込み、IGES へ変換
1. gcad または FREECAD で好きな形式へ変換
