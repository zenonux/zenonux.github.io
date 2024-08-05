---
title: "git worktree的使用"
date: "2022-04-10"
categories: 
  - "front-end"
tags: 
  - "git"
---

### 需求场景

之前在开发sass版后台管理系统时，有超管后台，渠道后台以及普通客户后台。3套代码大部分内容相同，但会根据需求有各自变化的部分，当时是在git仓库中建了3个分支。通过切换分支完成对应开发，在开发过程中，有个问题就是node\_modules依赖不一致的问题，每次切换分支node\_modules就要重新安装，非常之麻烦。后面想到一个临时的解决方法。将3个分支的代码克隆到3个不同的文件夹。每个文件夹切换到对应的分支，这样就能保持开发各自的分支互不影响。不过这种方式有一个缺点，假如A，B，C3个分支对应A，B，C三个目录。如果不小心在C目录切换到A分支上，就会出现问题。没有一个校验的过程，需要人工去避免这个误操作。为了解决这个问题，git worktree就有了用武之地。

### 解决方案

```bash
git worktree add ../A -b vA
git push --set-upstream origin vA
```

通过git worktree的操作，如果在C目录切换到A分支，git会提示错误，无法切换，这样就避免了误操作。

### 参考文档

[https://zhuanlan.zhihu.com/p/41006726](https://zhuanlan.zhihu.com/p/41006726)
