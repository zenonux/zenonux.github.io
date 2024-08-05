---
title: "docker常用命令"
date: "2021-10-15"
categories: 
  - "back-end"
tags: 
  - "docker"
  - "long-term"
---

### docker常用命令

```docker
#列出镜像
docker images
#删除镜像
docker rmi 
#删除全部镜像
docker rmi $(docker images -q)
#列出全部容器
docker ps -a
#重启容器
docker restart 
#删除容器docker rm 
#查看容器日志
docker logs 
#删除所有停止的容器
docker container prune
#删除所有容器
docker rm $(docker ps -aq)
#进入容器
docker exec -it 775c7c9ee1e1 /bin/bash  
```

### docker-compose常用命令

```docker
#启动docker并加入后台进程
docker-compose up -d
#更新容器镜像
docker-compose pull
#关闭所有容器
docker-compose stop 
#重启nginx
docker-compose restart nginx
#启动nginx
docker-compose start nginx
#关闭nginx
docker-compose stop nginx
#查看全部container
docker-compose ps
#删除全部停止的container
docker-compose rm
```
