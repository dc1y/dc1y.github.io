---
title: Git 入门练习
date: 2018-03-14 08:59:37
updated: 2018-03-14 08:59:37
tags: Git
categories:
- 实用工具
- Git
keywords: Git, 入门
---
本文并非完整的 Git 教程，而是从 [廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) 中提炼出来的练习，便于集中进行快速的回顾和练习。

通读上述教程并了解 Git 的基本知识后，建议按一定的时间间隔参照本文进行重复练习，以便强化记忆并牢固掌握 Git 的用法。你可以在读完教程后先做一遍，然后在第二天、一周后及一个月后再做一遍。若练习过程中碰到不理解的内容，可重新阅读教程的相关章节。

手快的话，估计20分钟搞定。
<!--more-->

# Git 简介

## 配置用户信息：

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 创建 Git 仓库

```bash
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

更简明的做法，是在创建文件夹的同时初始化仓库：

```bash
$ git init learngit
Initialized empty Git repository in D:/temp/learngit/.git/
$ cd learngit
```

## 添加文件并提交变更

readme.txt 文件内容：

```txt
Git is a version control system.
Git is free software.
```

添加文件并提交变更：

```bash
$ git add readme.txt
$ git commit -m "wrote a readme.txt file"
[master (root-commit) d4f717e] wrote a readme.txt file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

# 时光机穿梭

修改 readme.txt 文件：

```txt
Git is a distributed version control system.
Git is free software。
```

## 查看状态

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

## 对比差异

```bash
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index 9f7547c..b18bfcc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.^M
 Git is free software.
\ No newline at end of file
```

暂存变更后再查看状态：

```bash
$ git add readme.txt
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

提交变更后查看状态：

```bash
$ git commit -m "add distributeed"
[master d8833bc] add distributeed
 1 file changed, 1 insertion(+), 1 deletion(-)

dc1y@dc1y-X450L MINGW64 /d/temp/learngit (master)
$ git status
On branch master
nothing to commit, working tree clean
```

## 在版本间导航

修改 readme.txt 文件：

```txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

暂存并提交变更：

```bash
$ git add readme.txt
$ git commit -m "append GPL"
[master b6a39d7] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
```

查看历史记录：

```bash
$ git log
commit b6a39d75891e09320f99d950fcf3bfc9d772e087 (HEAD -> master)
Author: dc1y <dc1y@163.com>
Date:   Fri Mar 16 18:03:44 2018 +0800

    append GPL

commit ...
```

显示单行记录：

```bash
$ git log --pretty=oneline
b6a39d75891e09320f99d950fcf3bfc9d772e087 (HEAD -> master) append GPL
d8833bc12a58a413e7a8f3fad264e78cb83b94e6 add distributeed
d4f717ee18a742d030334960f4fac79a43081c49 wrote a readme.txt file
```

退回前一个版本“add distributed”：

```bash
$ git reset --hard HEAD^
HEAD is now at d8833bc add distributeed
```

查看文件内容及历史记录：

```bash
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
$ git log --pretty=oneline
d8833bc12a58a413e7a8f3fad264e78cb83b94e6 (HEAD -> master) add distributeed
d4f717ee18a742d030334960f4fac79a43081c49 wrote a readme.txt file
```

前进到最新版本（指定 commit id 的前几位），再查看文件内容：

```bash
$ git reset --hard b6a39d7
HEAD is now at b6a39d7 append GPL
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

查看命令记录及 commit id：

```bash
$ git reflog
b6a39d7 (HEAD -> master) HEAD@{0}: reset: moving to b6a39d7
d8833bc HEAD@{1}: reset: moving to HEAD^
b6a39d7 (HEAD -> master) HEAD@{2}: commit: append GPL
d8833bc HEAD@{3}: commit: add distributeed
d4f717e HEAD@{4}: commit (initial): wrote a readme.txt file
```

## 工作区和暂存区

修改 readme.txt 文件；再增加 LICENSE，内容随便：

```txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

查看状态（readme.txt 为 modified，LICENSE 为Untracked）：

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```

加入暂存区后，再查看状态：

```bash
$ git add readme.txt LICENSE

dc1y@dc1y-X450L MINGW64 /d/temp/learngit (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   LICENSE
        modified:   readme.txt
```

提交后查看状态（工作区是“干净”的）：

```bash
$ git commit -m "understand how stage works"
[master 8782d88] understand how stage works
 2 files changed, 3 insertions(+), 1 deletion(-)
 create mode 100644 LICENSE
$ git status
On branch master
nothing to commit, working tree clean
```

## 管理修改

commit提交的是已add到暂存区的内容，不包括工作区内容：

修改 readme.txt 文件：

```txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
```

add到暂存区后查看状态：

```bash
$ git add readme.txt
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

再修改 readme.txt 文件：

```txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
```

提交后查看状态（readme仍然是modified，提交的只是stage的内容）：

```bash
$ git commit -m "git track changes"
[master 62300d5] git track changes
 1 file changed, 1 insertion(+)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

查看工作区与版本库中最新版本的区别（第二次修改仍在工作区，没有提交到版本库）：

```bash
$ git diff HEAD -- readme.txt
diff --git a/readme.txt b/readme.txt
index 4c82836..ba3de77 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.^M
```

再add后commit：

```bash
$ git add readme.txt
$ git commit -m "commit act on stage only"
[master 2197a31] commit act on stage only
 1 file changed, 1 insertion(+), 1 deletion(-)
```

## 撤消修改

修改 readme.txt 文件（不慎出问题了）：

```txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.
```

查看状态；丢弃工作区修改，代之以暂存区或版本库的最后版本（stupid boss没了）：

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
$ git checkout -- readme.txt
```

继续加stupid boss，并add但未commit：

```bash
$ git add readme.txt
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

撤消暂存（HEAD表示最新版本），并查看状态（工作区有未暂存的修改）：

```bash
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

再一次丢弃工作区（工作区也没有stupid boss了）：

```bash
$ git checkout -- readme.txt
$ git status
On branch master
nothing to commit, working tree clean
```

## 删除文件

新增text.txt，add后commit：

```bash
$ git add test.txt
$ git commit -m "add test.txt"
[master fdabff1] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

删除test.txt后查看状态：

```bash
$ rm test.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

确实要删除，则移除跟踪并commit：

```bash
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
[master e4d858f] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

如果是误删有用文件，可如前以`git checkout -- test.txt`从版本库恢复。

# 远程仓库

先得在GitHub.com注册，上传SSH Key，创建learngit仓库。

把本地仓库与远程仓库关联（首次需要-u来关联master分支），然后刷新仓库，查看推送结果：

```bash
$ git remote add origin git@github.com:dc1y/learngit
$ git push -u origin master
Counting objects: 23, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (18/18), done.
Writing objects: 100% (23/23), 1.87 KiB | 319.00 KiB/s, done.
Total 23 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:dc1y/learngit
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

克隆远程仓库——在GitHub新建gitskill仓库：

```bash
$ cd ..
$ git clone git@github.com:dc1y/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

# 分支管理

# 标签管理

如果能够明白命令的作用及输出结果，恭喜，你已掌握 Git 了。