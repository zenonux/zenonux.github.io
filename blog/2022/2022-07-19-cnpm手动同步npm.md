---
title: "cnpm手动同步npm"
date: "2022-07-19"
categories: 
  - "front-end"
tags: 
  - "cnpm"
  - "npm"
---

### 需求场景

在自己发布一个npm包之后，如果立即使用cnpm安装，则无法找到该安装包，因为还没有同步过来，总不能慢慢等cnpm同步。好在cnpm有个手动同步的工具。

### 解决方案

```bash
https://npm.taobao.org/sync/+ 包名
https://npmmirror.com/sync/+包名
```
