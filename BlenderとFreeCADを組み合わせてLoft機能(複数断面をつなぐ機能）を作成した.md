---
tags:
  - 02_設計ツール
---

# Blender と FreeCAD を組み合わせて Loft 機能(複数断面をつなぐ機能）を作成した

## モチベーション

会社で使用している有料 CAD の Loft 機能が、イケなさすぎたので、Blender と FreeCAD を組み合わせて自作しました。FreeCAD だけでもできるのだけれど、残念ながら形状やポイント数によって上手く繋がらなかった為、断面をつなぐ機能は Blender にお任せしました。

## 環境作成(windows10)

anaconda をインストールして、TBD の

## やりたいこと

座標(x,y,z)で定義された断面を繋いで、CAD 形状を作りたい。
※CAE で解析するためには、CAD 形状が便利なので。。。STL を上手くリメッシュして解析できればよいのになぁ

## やったこと

- 断面座標を pandas dataframe で定義（会社では excel から読み込んでます）

```sectiondata.py
import pandas as pd
df1 = pd.DataFrame([[0.0, -0.16, -1.61],
                     [0.0, -1.86, -1.26],
                     [0.0, -1.67, 0.77],
                     [0.0, -0.14, 1.29],
                     [0.0, 1.08, 1.58],
                     [0.0, -0.16, -1.61]],columns=["x","y","z"])

df2 = pd.DataFrame([[1.0, -0.76, -1.38],
                     [1.0, -1.77, -0.12],
                     [1.0, -1.1, 1.02],
                     [1.0, 0.14, 1.9],
                     [1.0, 0.9, 1.87],
                     [1.0, 1.31, 2.22],
                     [1.0, 0.99, -0.54],
                     [1.0, -0.17, -0.84],
                     [1.0, -0.76, -1.38]],columns=["x","y","z"])

lim=(-3,3)
df1.plot(x="y",y="z",xlim=lim,ylim=lim,linestyle='-',marker='.',title="section1")
df2.plot(x="y",y="z",xlim=lim,ylim=lim,linestyle='-',marker='.',title="section2")
```

【実行結果】
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/274127/d492c4c6-34c8-b1dd-65dc-6b80affe5ce9.png)

- blender で上記座標点を作成し、辺ループのブリッジで 3D 形状を作成、blnder 形式と stl 形式でアウトプットする

```blender.py
import bpy
#立ち上げ時に存在するオブジェクト（立方体）を削除
bpy.ops.object.select_all(action="SELECT")
bpy.ops.object.delete(use_global=True)

#前処理
n1,n2 = len(df1),len(df2)#座標点の数を取得
verts = pd.concat([df1,df2]).values.tolist()#blenderで認識できるように座標点をリスト化する
faces = [[i for i in range(n1)], [i for i in range(n1,n1+n2)]]#各々の面を定義するリストを作成

#Loftの作成
mesh = bpy.data.meshes.new(name="test")
mesh.from_pydata(verts,[],faces)#点と面を作成
mesh.update
obj = bpy.data.objects.new(name="test",object_data=mesh)
scene =bpy.context.scene
bpy.context.scene.collection.objects.link(obj)
bpy.context.view_layer.objects.active = obj

bpy.ops.object.mode_set(mode = "EDIT")
bpy.ops.mesh.bridge_edge_loops()#辺ループのブリッジ->ここでLoft形状が作成される
bpy.ops.object.mode_set(mode = "OBJECT")

```

【実行結果】
test.blender と test.stl が吐き出されます。下図の通り、見事に Loft してくれます。Blender はとっても優秀です！！！
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/274127/74961ff4-7648-39b9-ac2f-3973484c54df.png)

- 上記の stl を FreeCAD で読み込み、stl から CAD 形状を起こし、iges 形式で吐き出す

```freecad.py
import freecad
import Part, DraftGeomUtils
FreeCAD = freecad.app
import bpy


def camera_position(matrix):

    """ From 4x4 matrix, calculate camera location """

    # https://stackoverflow.com/questions/9028398/change-viewport-angle-in-blender-using-python

    t = (matrix[0][3], matrix[1][3], matrix[2][3])
    r = (
      (matrix[0][0], matrix[0][1], matrix[0][2]),
      (matrix[1][0], matrix[1][1], matrix[1][2]),
      (matrix[2][0], matrix[2][1], matrix[2][2])
    )
    rp = (
      (-r[0][0], -r[1][0], -r[2][0]),
      (-r[0][1], -r[1][1], -r[2][1]),
      (-r[0][2], -r[1][2], -r[2][2])
    )
    output = (
      rp[0][0] * t[0] + rp[0][1] * t[1] + rp[0][2] * t[2],
      rp[1][0] * t[0] + rp[1][1] * t[1] + rp[1][2] * t[2],
      rp[2][0] * t[0] + rp[2][1] * t[1] + rp[2][2] * t[2],
    )
    return output

    import sys, bpy, xml.sax, zipfile, os, mathutils

import time

#from bpy_extras.node_shader_utils import PrincipledBSDFWrapper

SKIP_REGIONS_MAX = 100 # the max number of faces in a n object for region finding

scene = bpy.context.scene
objects = [obj for obj in scene.objects if obj.type == 'MESH']

doc = FreeCAD.newDocument("test")

obj = objects[0]
name = obj.name

depsgraph = bpy.context.evaluated_depsgraph_get()
objeval = obj.evaluated_get(depsgraph)
mesh = bpy.data.meshes.new_from_object(objeval)

mat = mathutils.Matrix()
s0,s1,s2 = obj.matrix_world.to_scale()
mat[0][0] = abs(s0)
mat[1][1] = abs(s1)
mat[2][2] = abs(s2)
mesh.transform(mat)

regions = []
faces = list(mesh.polygons)
if len(faces) <= SKIP_REGIONS_MAX:
    while faces:
        if not regions:
            regions.append([faces.pop()])
        for region in regions:
            found = False
            for regface in region:
                regedges = regface.edge_keys
                for face in faces:
                    for edge in face.edge_keys:
                        if (edge in regedges) or (edge[::-1] in regedges):
                            # this face shares an edge with a face already in regions
                            if face.normal == regface.normal:
                                if face.material_index == regface.material_index:
                                    # these two faces are part of a same region
                                    region.append(face)
                                    faces.remove(face)
                                    found = True
                                    # modifying a list while looping in it is dangerous, so we better break now
                                    break
            if found:
                break
        else:
            if faces:
                # no face found to add to existing regions, starting a new region
                regions.append([faces.pop()])
else:
    # too many faces... Leave them alone
    regions = [[face] for face in faces]


# build FreeCAD faces from regions
scale=1
faces = []
for region in regions:
    # build list of border edges
    edges = {}
    for face in region:
        for edge in face.edge_keys:
            if (edge in edges):
                edges[edge] = edges[edge] + 1
            elif (edge[::-1] in edges):
                edges[edge[::-1]] = edges[edge[::-1]] + 1
            else:
                edges[edge] = 1
    borders = []
    for key,val in edges.items():
        if val == 1:
            borders.append(key)
    # build FreeCAD edges
    fedges = []
    for border in borders:
        p1 = FreeCAD.Vector(list(mesh.vertices[border[0]].co))
        p2 = FreeCAD.Vector(list(mesh.vertices[border[1]].co))
        if scale != 1:
            p1.multiply(scale)
            p2.multiply(scale)
        if p1 != p2:
            fedges.append(Part.makeLine(p1,p2))
    # sort by wires
    wires = DraftGeomUtils.findWires(fedges)
    print(wires)
    if wires:
        for wire in wires:
            if not wire.isClosed():
                print("Open wires in",name)
                break
        else:
            # TODO do this better
#             try:
            faces.append(Part.Face(wires))
#             except:
#                 print("FIXME: Unable to form face from wire in",name)
    else:
        print("Unable to build border wires for",name)

if faces:
    try:
        shape = Part.Shell(faces)
        if shape.isClosed():
            try:
                shape = Part.Solid(shape)
            except Part.OCCError:
                pass
    except Part.OCCError:
        shape = Part.makeCompound(faces)

# edge-only object
else:
    edges = []
    for edge in mesh.edges:
        p1 = FreeCAD.Vector(list(mesh.vertices[edge.vertices[0]].co))
        p2 = FreeCAD.Vector(list(mesh.vertices[edge.vertices[1]].co))
        if scale != 1:
            p1.multiply(scale)
            p2.multiply(scale)
        if p1 != p2:
            edges.append(Part.makeLine(p1,p2))
    if edges:
        shape = Part.makeCompound(edges)

fobj = doc.addObject("Part::Feature",name)
fobj.Shape = shape
mod = obj.rotation_mode
# need to switch otherwise quaternion is not properly set...
obj.rotation_mode = "QUATERNION"
rot = obj.rotation_quaternion
obj.rotation_mode = mod
# FreeCAD Quaternion is XYZW while Blender is WXYZ
rot = FreeCAD.Rotation(rot[1],rot[2],rot[3],rot[0])
loc = obj.location
loc = FreeCAD.Vector(loc[0],loc[1],loc[2])
if scale != 1:
    loc.multiply(scale)
fobj.Placement = FreeCAD.Placement(loc,rot)

# build color data
if faces:
    coldata = []
    for region in regions:
        i = region[0].material_index
        if i < len(obj.data.materials):
            if hasattr(obj.data.materials[i],"diffuse_color"):
                coldata.append(tuple(list(obj.data.materials[i].diffuse_color)[:3]))
                continue
        # no material
        coldata.append(tuple(list(obj.color)[:3]))
#     colors[name] = coldata
    #print(name,len(coldata),"colors,",len(shape.Faces),"faces")
    # TODO the OfflineRenderingUtils module doesn't support face colors yet.. So for now each object will have only one color

# clean up the blender mesh
bpy.data.meshes.remove(mesh)

pc = "PerspectiveCamera {&#10;  viewportMapping ADJUST_CAMERA&#10;  position --pos--&#10;  orientation --rot--  1.0&#10;  nearDistance 0.0001&#10;  farDistance 1000000&#10;  aspectRatio 1&#10;  focalDistance 15.0&#10;  heightAngle 30.0&#10;&#10;}&#10;"
oc = "OrthographicCamera {&#10;  viewportMapping ADJUST_CAMERA&#10;  position --pos--&#10;  orientation --rot--  1.0&#10;  nearDistance 0.0001&#10;  farDistance 1000000&#10;  aspectRatio 1&#10;  focalDistance 15.0&#10;  height 30.0&#10;&#10;}&#10;"
camera = None
# find the first available 3D window
for window in bpy.context.window_manager.windows:
    for area in window.screen.areas:
        if area.type == "VIEW_3D":
            for space in area.spaces:
                if space.type == "VIEW_3D":
                    if space.region_3d.view_perspective == "PERSP":
                        camera = pc
                    else:
                        camera = oc
                    pos = camera_position(space.region_3d.view_matrix)
                    pos = str(pos[0])+" "+str(pos[1])+" "+str(pos[2])
                    camera = camera.replace("--pos--",pos)
                    rot = space.region_3d.view_rotation
                    rot = FreeCAD.Rotation(rot[1],rot[2],rot[3],rot[0])
                    rot = rot.multVec(FreeCAD.Vector(0,0,1))
                    rot = str(rot[0])+" "+str(rot[1])+" "+str(rot[2])
                    camera = camera.replace("--rot--",rot)
#print("camera:",camera)

import OfflineRenderingUtils
filename = "test_loft.FCStd"
OfflineRenderingUtils.save(doc,filename,guidata=None,camera=camera)

FreeCAD.closeDocument(doc.Name)
```

【実行結果】
test.FCStd と test.iges が吐き出されます。CAD の Solid となりました！
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/274127/aa784522-4b0d-878d-0c99-1b8b6995cfd0.png)

## ソースコード

下記サイトの Loft.ipynb にあります。
https://github.com/myao9494/Loft_feature_python

## ひとりごと

- 計算結果を 3D プリンタで出力したりも出来るようになります
- 地図データの等高線を CAD 化したりするときも助かるはず（富士山を CAD 化など）
- 3D スキャナの結果を CAD 化して CAE に掛けることも出来るようになるはず（リバースエンジニアリング）

ポイントクラウドを CAD 化する有料ソフト等を使えれば、苦労しなくても良いのかも。。。良いのがあれば、教えてください。
（まぁ、良いものでも、簡単に買って貰えない会社なんですけどね。。。でもおかげ様で、OpenSource にドンドン詳しくなっていく）
