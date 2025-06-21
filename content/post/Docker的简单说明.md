---
title: docker简单使用教程
description: docker的简单使用及其模板
date: 2024-11-17 17:00:00+0000
categories:
  - linux
tags:
  - docker
---
# docker简略使用教程

## 直接启动

### 拉取镜像

```bash
docker pull xhofe/alist:latest
```

### 运行容器

```bash 
docker run -it xhofe/alist:latest # 进容器  
docker run -d xhofe/alist:latest # 后台运行容器  
docker run -d --name=test xhofe/alist:latest # 指定容器名字为 test  
docker run -d --restart=unless-stopped --name=test xhofe/alist:latest # 指定容器一直重启-p 5244:5244  
docker run -d -p 5244:5244 xhofe/alist:latest # 指定容器端口, 主机端口:容器端口  
docker run -d -v /etc/alist:/opt/alist/data -v /etc/alisttest:/opt/alist/datatest xhofe/alist:latest # 指定存储卷 主机路径:容器路径  
docker run -d -e PUID=0 -e PGID=0 -e UMASK=022 xhofe/alist:latest # 添加环境变量  
```

## docker-compose启动

```docker-compose  
version: '3'  
services:  
    alist1:  
        image: 'xhofe/alist:latest'  
        container_name: alistsdfjdskfjk  
        volumes:  
            - '/etc/alist:/opt/alist/data'  
        ports:  
            - '5244:5244'  
        environment:  
            - PUID=0  
            - PGID=0  
            - UMASK=022  
        restart: unless-stopped  
```

进入到`docker-compose.yaml`的那个目录  

执行  

```bash
docker-compose up -d # 后台运行容器编排  
```

如果要关掉容器，执行

```bash
docker-compose down # 关掉容器编排
```
