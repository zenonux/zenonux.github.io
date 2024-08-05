---
title: "vscode配置eslint"
date: "2022-06-16"
---

### 步骤一

安装eslint插件

### 步骤二

打开全局配置,添加如下配置

```json
 "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "eslint.autoFixOnSave" : true,
  },
```
