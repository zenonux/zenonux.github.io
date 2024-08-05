---
title: "树莓派4b更换清华源（buster）"
date: "2021-11-03"
categories: 
  - "system"
tags: 
  - "raspberrypi"
---

### 解决方案

修改\`/etc/apt/sources.list.d/raspi.list\`

```bash
deb http://mirrors.tuna.tsinghua.edu.cn/raspberry-pi-os/raspbian/ buster main non-free contrib rpi 
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspberry-pi-os/raspbian/ buster main non-free contrib rpi
```

修改之后更新\`sudo apt update\`
