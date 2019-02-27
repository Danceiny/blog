---
date: 2017-08-25 18:49:30
status: public
title: Git超简明指南与超常用命令
keywords: 
- Git
- GitHub
- 入门
- 教程
tags: 
- Python
categories: 
- 快速入门快速实践
- 一天
- 常用
---


git fetch origin branchname:branchname

可以把远程某各分支拉去到本地的branchname下，如果没有branchname，则会在本地新建branchname

 

git checkout origin/remoteName -b localName

获取远程分支remoteName 到本地新分支localName，并跳到localName分支


git push -u origin local_branch_name

git push origin --delete <branchName>


scp username@servername:/path/filename /tmp/local_destination