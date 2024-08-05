---
title: "ubuntu完全卸载mysql/mariadb"
date: "2022-01-05"
tags: 
  - "mysql"
---

```bash
sudo apt-get remove mysql-*
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```
