---
title: "windows开机运行frpc（bat脚本）"
date: "2021-09-18"
categories:
  - "system"
tags:
  - "frp"
  - "windows"
---

**步骤一：在 frp 安装目录下新建 frpc.bat 启动脚本，脚本内容如下**

```
@echo off
:home
frpc -c frpc.ini
goto home
```

点击开始菜单，输入 “任务计划程序” 并打开，点击右侧的 “创建任务”

**步骤二：新建计划任务**

**常规：**名称随意填写，安全选项选择 “不管用户是否登录都要运行”，勾选“使用最高权限运行”

**触发器:**点击新建，选择 “启动时”

**操作:**点击新建，选择 “启动程序,在程序或脚本一栏选择第一步创建的 **frpc** .bat，下面的 “起始于” 填写 **frpc** .bat 的路径（不要包含 **frpc**.bat）
