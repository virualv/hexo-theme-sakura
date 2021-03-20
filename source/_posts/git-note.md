---
title: git使用手记
date: 2019-09-15 23:14:35
tags: git
categories: Version Control
photos: https://i.loli.net/2021/03/20/mNKCQt7Geqsbcpv.jpg
---
Git 手记 （持续更新）

## git 提交后，撤销提交

原因：

- 由于之前Ubuntu系统备份在NTFS文件系统的缘故，导致昨晚git提交时没有注意到权限，从而更改了整个handbook项目的文件权限。

- 今天在提交时突然误按了回车，致使提交内容不完整。

事故 预防和解决方案：

- 在每次`git push`之前先`git status`查看之前的commit有没有出问题

- 发现问题时利用`git reset`来撤销提交，具体方式如下：

  > `git reset --soft HEAD^` 撤销了前一次提交
  >
  > **仅仅撤销了commit，而代码的改动并没有撤销**
  >
  > ```bash
  > HEAD^   表示上一个版本
  > 其与HEAD~1等价
  > 
  > HEAD~2   表示上两个版本
  > ```

  > ```shell
  > git reset --mixed
  >               不删除工作空间的代码改动，撤销 git commit和 git add
  >           --soft
  >               不删除空间代码，只撤销 git commit，不撤销 git add
  >           --hard
  >               删除空间代码，并撤销 git commit 和 git add ，完全恢复到上一次commit状态
  > ```
