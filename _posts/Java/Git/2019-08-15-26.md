---
layout: post
title: Git冲突：commit your changes or stash them before you can merge.
category: Git
tags: [Git]
excerpt: Git冲突：commit your changes or stash them before you can merge.
---

## 问题一 ##


Git冲突：commit your changes or stash them before you can merge.

解决方式：

stash：

	git stash
	git pull
	git stash pop
	接下来diff一下此文件看看自动合并的情况，并作出相应的修改。
	git stash：备份当前的工作区，从最近一次提交中读取相关内容，让工作区保持和上一次提交的内容一致。同时，将工作区的内容保存到git栈中。
	git stash pop：从git栈中读取最近一次保存的内容，恢复工作区的相关内容。由于可能存在多个stash的内容，所以用栈来管理，pop会从最近一个stash中读取内容并恢复到工作区。
	git stash list：显示git栈内的所有备份，可以利用这个列表来决定从那个地方恢复。
	git stash clear：情况git栈。