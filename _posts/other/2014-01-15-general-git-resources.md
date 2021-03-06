---
layout: post
title: Git
category: other
tags: Git
keywords: Git
description: 
---

> 推荐一个好的git快速教程 ：[猴子都能懂的GIT入门](http://backlogtool.com/git-guide/cn/)

## Git设置

Git的全局设置在`~/.gitconfig`中，单独设置在`project/.git/config`下。

忽略设置全局在`~/.gitignore_global`中，单独设置在`project/.gitignore`下。

### 设置 commit 的用户和邮箱

```
[user]
    name = xxx
    email = xxx@xxx.com
```


# git创建远程库

>git中一般使用 git init 创建的库不允许同一分支多个work tree直接提交，如果这么做有可能会出现以下问题：

>remote: error: refusing to update checked out branch: refs/heads/master

>要解决这个问题可以有以下四种方式

## 创建共享库（推荐）

    # 创建共享库(bare)
    $ mkdir /git/repo.git && cd /git/repo.git && git init --bare

    # 本地库
    $ mkdir ~/repo && cd ~/repo && git init
    # 创建一个文件
    $ vi foo
    # 增加新增文件到库管理
    $ git add .
    # 提交
    $ git commit
    # 增加共享库位置
    $ git remote add origin file:///git/repo.git
    # 提交更改
    $ git push origin master

## 不工作在同一库下（推荐）

    # 创建库
    $ mkdir /git/repo  && cd /git/repo && git init
    # 创建一个文件
    $ vi foo
    # 增加新增文件到库管理
    $ git add .
    # 提交
    $ git commit 
    # 新建一个分支
    $ git branch test

    # 本地库
    $ git clone file:///git/repo && cd repo
    # 切换到分支test
    $ git checkout test
    # 修改文件
    $ echo "foo">foo
    # 提交
    $ git commit 
    # 增加远程库位置
    $ git remote add origin flie:///git/repo
    # 提交更改
    $ git push origin test

## 忽略冲突1
修改远程库.git/config添加下面代码

    [receive]
        denyCurrentBranch = ignore

这种方式不能直接显示在结果的work tree上，如果要显示，需要使用

    git reset --hard才能看到

## 忽略冲突2
在远程库上

    git config -bool core.bare true


## 历史管理

### 查看历史

    git log --pretty=oneline filename // 一行显示
    git show xxxx // 查看某次修改

### 标签功能
    
    git tag // 显示所有标签
    git tag -l 'v1.4.2.*' // 显示 1.4.2 开头标签
    git tag v1.3 // 简单打标签   
    git tag -a v1.2 9fceb02 // 后期加注标签
    git tag -a v1.4 -m 'my version 1.4' // 增加标签并注释， -a 为 annotated 缩写
    git show v1.4 // 查看某一标签详情
    git push origin v1.5 // 分享某个标签
    git push origin --tags // 分享所有标签

### 回滚操作
    reset --hard v0.1
    reflog
    reset --hard v0.2

### 取消某个文件的修改
    git checkout -- <filename>

### 删除文件
    git rm <filename>   直接删除文件
    git rm --cached <filename>    删除文件暂存状态

### 移动文件
    git mv <sourcefile> <destfile>

### 查看文件更新
    git diff              查看未暂存的文件更新 
    git diff --cached     查看已暂存文件的更新 
    
### 暂存和恢复当前staging

    git stash
    git stash apply

## 分支管理

### 创建分支
    
    git branch develop // 只创建分支
    git checkout -b master develop // 创建并切换到 develop 分支

### 合并分支
    合并分支有2种方法：使用merge或rebase。

    git checkout master // 切换到主分支
    git merge --no-ff develop // 把 develop 合并到 master 分支，no-ff 选项的作用是保留原分支记录

    git rebase develop --continue    // 合并分支  修改冲突后的提交指定 --continue选项

    git branch -d develop // 删除 develop 分支

### 克隆远程分支
    git branch -r
    git checkout origin/android              //切换分支

### 修复develop上的合并错误

1. 将merge前的commit创建一个分之，保留merge后代码
2. 将develop `reset --force`到merge前，然后`push --force`
3. 在分支中rebase develop
4. 将分支push到服务器上重新merge

### 强制更新到远程分支最新版本

    git reset --hard origin/master
    git submodule update --remote -f

## Submodule使用

### 克隆带submodule的库

    git clone --recursive https://github.com/chaconinc/MainProject

### clone主库后再去clone submodule

    git clone https://github.com/chaconinc/MainProject
    git submodule init
    git submodule update
    
