+++
title = 'Tailscale 与 DERP中继'
date = 2025-06-19
draft = false
+++



# Tailscale 与 DERP中继

## 零.安装docker

这里不再赘述，详情看这个链接

https://docs.docker.com/engine/install/



## 一.Tailscale

1.一键部署脚本

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

2.等待安装完成输入

```bash
tailscale login
```

然后进行登录



## 二.Derper

使用docker进行部署

新建一个文件，命名为：<u>**compose.yaml**</u>

在compose.yaml文件中输入

```yaml
services:
  derper:
    image: ghcr.nju.edu.cn/yangchuansheng/ip_derper:latest
    container_name: derper
    restart: always
    ports:
      - "12345:12345" # 这里的12345请改成你自己想要的10000以上的高位端口
      - "3478:3478/udp" # 3478 为stun端口，如果不冲突请勿修改
    volumes:
      - /var/run/tailscale/tailscaled.sock:/var/run/tailscale/tailscaled.sock # 映射本地 tailscale 客户端验证连接，用来验证是否被偷
    environment:
      - DERP_ADDR=:12345 # 此处需要与上面的同步修改
      - DERP_CERTS=/app/certs
      - DERP_VERIFY_CLIENTS=true # 启动客户端验证，这是防偷的最重要的参数

```

在该文件夹内，`docker compose up -d` 即可启动该 docker



## 三.修改Tailscale中的ACL

1.进入ACL界面：[Tailscale](https://login.tailscale.com/admin/acls/file) 进入后进行登录即可

2.加入配置文件：

    "derpMap": {
        "OmitDefaultRegions": false, // 可以设置为 true，这样不会下发官方的 derper 节点，测试或者实际使用都可以考虑打开
        "Regions": {
    		    "900": {
    			    "RegionID":   900, // tailscale 900-999 是保留给自定义 derper 的
    				"RegionCode": "abc1",
    				"RegionName": "abcc1",// 这俩随便命名
    				"Nodes": [
    					{
    						"Name":             "fff",
    						"RegionID":         900,
    						"IPv4":             "1.1.1.1", // 你的VPS 公网IP地址
    						"DERPPort":         12345, //上面 12345 你自定义的端口
    						"InsecureForTests": true, // 因为是自签名证书，所以客户端不做校验
    					},
    				],
    		    },
        },
    },



## 四.测试是否成功

#### 使用网络连接测试

1. 找到一个在用 tailscale 的客户端

2. 进入终端

3. 输入 `tailscale netcheck`

4. 检验是否有下图回应

#### 使用 ping 测试连通性

1. 找到一个在用 tailscale 的客户端

2. 进入终端

3. 输入 `tailscale ping 你的另一个主机地址`

4. 检验是否联通 (例如出现 `via DER (xxx)`) 即为成功


