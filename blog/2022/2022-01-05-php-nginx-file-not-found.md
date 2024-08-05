---
title: "php nginx File not found"
date: "2022-01-05"
categories: 
  - "back-end"
tags: 
  - "nginx"
  - "php"
---

### 需求场景

最近在腾讯云重新部署php，nginx环境遇到一个非常坑的问题，两台服务器同样的配置，刚部署的服务器出现File not found.

### 排查

通过\`tail -f /var/log/nginx/error.log\`在日志中发现Permission denied，Primary script unknown 等报错，查找资料说是权限问题。一般都是让检查nginx的默认用户www-data和php-fpm的默认用户www-data是不是一致。因为默认都是www-data不去改动的话，肯定都是一样的。或者是项目目录权限改为777等，实测都是无效的。

### 最终解决方案

以为腾讯云默认用户为ubuntu，一般不推荐root直接登录。所以我是在ubuntu用户下登录部署的，把项目部署在了/home/ubuntu/projects下面。因为默认的/var/www/html是可以访问的，而我部署在/home/ubuntu/projects就是不可访问的，当我把项目移动至/home/projects下面就可以了。。。回想起来，之前的一台腾讯云服务器一直用root登录，项目部署在/home/projects也是没有问题的。

### 问题思考

所以这个问题的根本原因还是权限问题，只不过这个权限问题相当坑，777也解决不了。
