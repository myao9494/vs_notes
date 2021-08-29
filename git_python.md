---
tags:
  - python
---

# git_python

## status を一覧表で取得する

```
import git
import pandas as pd
repo = git.Repo(git_folder_path)
li = repo.git.status("-s").split("¥n")
li_s = [[i[0:2],i[3:]] for i in li]
df = pd.DataFrame(li_s,columns=["code","file_name"])
```
