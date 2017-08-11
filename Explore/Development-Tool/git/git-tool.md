---
tags: ['命令手册']
---
# Git工具

## git stash

### 场景
当你正在进行某一部分的工作，内容处在一个比较杂乱的状态。但此时想要转到其他分支上进行工作，又不想提交进行了一半的工作时，可以使用`git stash`来暂存当前状态

### 状态
`git stash`  暂存


## 其他特殊命令

### 合并某个分支上的单个commit
`git cherry-pick [commit hash]`
将其他分支上的提交commmit hash的内容合并到当前分支，当前分支中会多一个新的commit。
如果git不能合并代码改动，比如遇上合并冲突，需要自己解决冲突并手动添加commit

### 合并某个分支上的一系列commit
加入要合并commit hashA到hashB到master

`git checkout -bnewbranch hashB`
建立一个新的分支newbranch，指明了该分支到commit hashB
`git rebase --ontomaster hashA`
将从hashA到hashB的commit都提交到master分支

