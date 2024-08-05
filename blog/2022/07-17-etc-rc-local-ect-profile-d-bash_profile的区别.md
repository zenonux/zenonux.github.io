---
title: "/etc/rc.local,/ect/profile.d/,.bash_profile的区别"
date: "2022-07-17"
categories: 
  - "back-end"
tags: 
  - "shell"
---

### 主要区别

- /etc/rc.local

最先执行，在登录之前执行

设置开机启动任务，应该放在rc.local中执行，它只会在系统启动时执行一次。

- /etc/profile.d/

其次执行，需要登录，针对所有用户

设置环境变量的脚本，可以放在profile.d目录下面，但开机执行任务不应该放在profile.d目录下，因为每次登陆都会执行profile.d目录下的文件，会导致重复执行

- .bash\_profile

最后执行，需要登录，只针对当前用户

### 开机脚本执行顺序

1. 通过/boot/vm进行启动 vmlinuz
2. init /etc/inittab
3. 启动相应的脚本，并且打开终端
4. rc.sysinit
5. rc.d(里面的脚本）
6. rc.local
7. 启动login登录界面 login
8. 在用户登录的时候执行sh脚本的顺序，每次登录的时候都会完全执行的
9. /etc/profile.d/file
10. /etc/profile
11. /etc/bashrc
12. /root/.bashrc
13. /root/.bash\_profile
