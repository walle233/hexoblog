---
title: gitflow
---

## git基础

略

## git分支


### 分支基础

```
git branch newb // 新建分支
```

```
git checkout newb // 切换到新分支
```

```
git checkout newb -b iss91 // 新建并切换到新分支iss91
```

```
git merge newb // 合并分支
```

```
git branch newb -d // 删除分支
```

### 分支的管理

```
git branch // 查看git分支列表
```

```
git branch --merged // 查看已合并分支列表
```

```
git branch--no-merged // 查看未合并分支列表
```

### 远程分支

```
git remote add origin remote_url // 添加远程分支
```

```
git fetch origin // 同步远程服务器
```

```
git merge origin/serverfix // 合并远程分支
```

```
git push origin // 推送到远程服务器
```

```
git checkout --track origin/serverfix // 跟踪远程分支
```

```
git push origin :serverfix // 删除远程分支  git push [远程名] [本地分支]:[远程分支]
```


## git版本，标签

### git版本

```
git reset --hard HEAD // 回退到指定版本
```
