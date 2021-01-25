---
tags:
  - 01_チートシート
---

# 2020-10-31 git

## 用語

| 用語       | 説明                                                   |
| ---------- | ------------------------------------------------------ |
| 作業ツリー | Git で管理されたディレクトリ(と含まれるファイル)のこと |

## git commit をなかったことに(一人 git の場合)

```zsh
git reset --soft "HEAD^"
git push -f origin HEAD
```

## git commit をなかったことに(共有プロの場合)

### プッシュ前

- 直前の Commit だけを修正する場合： amend
- Commit を消したい場合： reset
- 古い Commit を修正する場合： rebase

### プッシュ後

```zsh
git revert <commit id>
git revert "HEAD^"

git push
```

## リモートに強制的に合わせる

```zsh
git fetch origin
git reset --hard origin/master
```

## issue とリンクしたコミット

コミットメッセージに以下を加えれば OK

- "README.md #2 修正 " :#issue 番号があれば、紐づく
- "README.md create close #1":cloae #issue 番号 でクローズする

## git command

```git
git show HEAD^:presentation.pptx > temp.pptx #ひとつ前のコミットを別ファイルとして取りだし
git add -A 全ての変更をステージング
git commit -m "コメント"　ステージングした変更をコミット
git push リモートに反映

git reset --soft "HEAD^"　　コミットの削除　--softは変更はそのままにするという意味
git clean -f 追跡されていないすべてのファイルを削除します。
git clean -df 追跡されていないすべてのファイルとディレクトリを削除します。
git checkout . 作業ツリーを戻す（すべて）
git checkout branch_name  既存のブランチに切り替えます。

git checkout -b ブランチ名 　ブランチを作成して作成したブランチを現在にする
git branch  どのブランチが現在かを確認
git branch -d ブランチ名　　ブランチを削除する
git branch -m new_name 現在のブランチの名前を変更します。
git push origin :branch_name リモートブランチを削除します。
```
