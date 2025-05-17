+++
title = '2025 5 17 BuildRadicale'
date = 2025-05-17T13:44:57+08:00
draft = true
+++

# 一.安装dockge

```bash
sudo mkdir -p /opt/stacks /opt/dockge
cd /opt/dockge
sudo curl "https://dockge.kuma.pet/compose.yaml?port=5001&stacksPath=%2Fopt%2Fstacks" --output compose.yaml
sudo systemctl enable docker
sudo systemctl start docker
docker compose up -d
```

官方原文的compose.yaml文件如下：

```
services:
  dockge:
    image: louislam/dockge:1
    restart: unless-stopped
    ports:
      - 5001:5001
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./data:/app/data
      # Stacks Directory
      # ⚠️ READ IT CAREFULLY. If you did it wrong, your data could end up writing into a WRONG PATH.
      # ⚠️ 1. FULL path only. No relative path (MUST)
      # ⚠️ 2. Left Stacks Path === Right Stacks Path (MUST)
      - /opt/stacks:/opt/stacks
    environment:
      # Tell Dockge where to find the stacks
      - DOCKGE_STACKS_DIR=/opt/stacks
```

可以注意到是在5001:5001端口启动，所以访问[IP:5001](127.0.0.1:5001) (如果是本地点击即可访问)

打开后如下：自行设置即可

![](https://pica.zhimg.com/v2-91c04e8a2e51bf1b2a0ed618bc53e6b6_1440w.jpg)

进入后如图所示：

![](/home/yihan/.config/marktext/images/2025-05-17-14-08-55-image.png)

用了这个后，docker部署变得非常简单(虽然也不是很难就是了，上面步骤就是用docker的部署)

# 二.部署Radicale

### 步骤一：compose.yaml

```
version: '3.7'
services:
  radicale:
    image: tomsquest/docker-radicale
    container_name: radicale
    ports:
      - 5232:5232
    init: true
    read_only: true
    security_opt:
      - no-new-privileges:true
    cap_drop:
      - ALL
    cap_add:
      - SETUID
      - SETGID
      - CHOWN
      - KILL
    deploy:
      resources:
        limits:
          memory: 256M
    healthcheck:
      test: curl -f http://127.0.0.1:5232 || exit 1
      interval: 30s
      retries: 3
    restart: unless-stopped
    volumes:
      - ./data:/data
```

### 步骤二：Dockge部署

打开Dockge面板 -> 创建堆栈 -> 设置堆栈名称 -> 粘贴compose代码 -> 30秒启动成功！

![](https://pica.zhimg.com/v2-68930e3cf5ec9ac3c60ce1f9428516a6_1440w.jpg)

随后等待部署完成即可。

然后要注意到，上文.yaml文件中端口开在5232,所以访问[IP:5232]([http://127.0.0.1:5232](http://127.0.0.1:5232))
